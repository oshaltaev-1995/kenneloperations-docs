# Housing and Kennel Map

## Housing model

Housing is date-effective history, not merely the current tuple stored on `Dog` for convenient reads. A housing identity consists of kennel side, kennel row, and home slot. `DogHousingAssignment` records authoritative effective intervals with `starts_on` inclusive and `ends_on` exclusive.

The current `Dog.kennel_side`, `kennel_row`, and `home_slot` fields are a current cache/projection. Historical reads resolve the assignment covering the requested reference date. If a dog has housing history but no interval for that date, the API returns no housing rather than leaking the current tuple into a historical view.

A current housing move closes the previous open assignment on the move date, creates the new interval, and updates the current tuple. Batch moves are validated and persisted by the backend; changing a visual map layer never writes housing.

Housing history and layout history are different:

- **Housing history** records which dog lived in which housing identity over time.
- **Layout history** defines which physical pen identities and geometry existed on a date.

The Kennel Map combines the effective housing assignment with the effective physical layout to render a dated view.

## Kennel Map

Kennel Map is a full-screen operational visual canvas for the kennel ground. “Canvas” describes its workspace role: the implementation is Angular-rendered HTML/DOM and CSS, not an HTML `<canvas>`. Small inline SVG paths are used only for operational-status icons.

Two projections are available:

- **Ground layout** uses fixed physical group coordinates, non-uniform pen rectangles, corridor spacing, and a zoom/pan camera. Fit and zoom transform the view; they do not reflow or rewrite canonical geometry.
- **Row table** presents the same dated dogs and pens in a responsive grid organized by kennel area and row.

The workspace can focus on all kennel areas, Vanha, Uusi, or Special areas. Search matches a dog name, focuses the relevant area when possible, and highlights the dog and pen. Dog chips link to Dog Detail. Archived and Deceased records are not rendered as current map occupants.

On a current view, **Move dogs** supports staged drag-and-drop between pens and an explicit move dialog. An occupied target requires a deliberate place-together or swap decision. Pending moves can be undone or discarded before one backend batch save. The map does not expose a separate unassigned-dog strip: dogs without a complete, valid physical home are not placed in a pen.

Current housing moves are available to Admin, Manager, Planner, and Staff. Staff permission applies only to current housing movement; it does not grant general Dog-profile editing, status/lifecycle management, Front Yard changes, or housing-history rewriting. Viewer is read-only.

Front Yard is a date-effective operational assignment, not a housing location. A Front Yard dog remains in its physical housing cell and can be outlined by the Front Yard layer.

The ground view supports 35–100% zoom, Fit, pointer panning, wheel zoom, and drag-edge scrolling. At narrower widths the toolbar wraps and the Row table changes from multiple columns to one; Fit scales the fixed ground geometry without changing pen relationships.

## Map layers

The operator-facing layer order is defined by `KennelMapPageComponent`:

| Operator label | What it visualizes | Technical/domain source and marker |
| --- | --- | --- |
| **Default** | Physical occupancy without an additional colour classification | Effective dog housing; the normal dog chip treatment remains |
| **Class** | Operational/work class | `operational_class`, falling back to `work_class`; Puppy is pink, Junior purple, Training green, Standard yellow, Retired brown, and unresolved review state uses a dashed amber treatment |
| **Gender** | Recorded sex | `Dog.sex`; blue male symbol, pink female symbol, or grey unknown marker |
| **Neuter** | Recorded neuter state | `Dog.is_neutered`; `N`, `I`, or `?` marker |
| **VOM feeding** | Pens on the configured feeding route | Static physical-pen configuration: rows C1, D2, and F2, excluding C1-07; included pens are green and other pens are muted |
| **Front Yard** | Effective Front Yard assignment on the reference date | Date-effective `DogOperationalAssignment`; a dark-blue dog-chip border while the dog stays in its housing pen |
| **Readiness** | Current workload attention severity in the map summary | Canonical summary `workload_severity`; Elevated is yellow, High orange, and Critical red. The separate Unavailable overlay continues to show lifecycle/operational blocks |
| **Previous day work** | Meaningful work on the day before the reference date | Backend `worked_on_previous_day`, derived from canonical activity rows; a green dog-chip treatment |
| **7d workload** | Workload attention marker supplied with the map summary | Canonical summary severity rendered as `E`, `H`, or `C` |
| **14d workload** | Workload attention marker supplied with the map summary | Canonical summary severity rendered as `E`, `H`, or `C` |

The current client does not calculate separate workload windows when switching between **7d workload** and **14d workload**; both selectors render the canonical severity returned in the dog-summary payload. This is an honest description of the current implementation, not a claim that layer selection recomputes workload.

**Unavailable** is an independent overlay rather than a layer. It uses the effective status projection for the reference date, mutes an unavailable dog name, and shows the highest-priority dated marker for Injury, Illness, Pregnant, Rest / recovery, Retired, or Manual exclusion. Tooltips retain the status reason and Front Yard planning context.

Layer switching is visual only. It changes CSS treatments and markers, and preserves the selected layer in the URL. It does **not** move dogs, create status periods, change Front Yard, alter workload, change lifecycle, edit housing history, or affect planning eligibility.

## Physical layout and pen geometry

The ground layout is a fixed operational representation of Vanha, Uusi, and the special areas Pukukammi, Yläkammi, Pentuhäkki, and Hoitokontti. Rows are grouped at canonical coordinates; Uusi rows with descending physical order are rendered in that order rather than assuming numeric slot distance equals physical distance.

An ordinary pen rectangle is one configured cell. Large/combined cells use the same identity fields but span twice the ordinary height in the ground projection. The current static geometry marks B2-06, B2-07, C1-06, C1-07, C2-06, and C2-07 as these larger cells. Their codes remain distinct housing identities; the current source contains no date-effective B/C remapping table comparable to D1.

The repository history proves that the B2/C1/C2 large-cell representation was present when the standalone Kennel Map was introduced. It does not prove the date of the physical kennel cutover, so no B/C historical date is asserted here.

### Shared geometry with Autumn suggestions

`buildPhysicalPenRectangles(referenceDate)` derives rectangles from the same ground groups, row order, pen sizes, merged-cell rules, corridor gaps, and D1 era used by Kennel Map. Autumn's housing-proximity suggestion consumes those rectangles and ranks pen groups by centre-to-centre physical distance.

This is architectural reuse, not a map-layer effect. The suggestion is advisory selection logic: it does not move a dog, assign a harness role, or invent a pair. See [Training](training.md#housing-proximity-suggestion).

## Current and historical layouts

The map receives an optional `as_of_date` and requests the effective dog summary for that date. The same reference date selects D1 cell count, spans, corridor position, housing, Front Yard membership, status markers, previous-day work, and workload context.

A view for a date other than today is read-only for every role. **Move dogs** is disabled, drag/drop and the move dialog are guarded, and no housing batch can be saved. Current move selectors expose only current valid pens. A former identity can remain visible in historical context but must be explicitly remapped before a current edit is saved.

### Layout evolution

D1 is one concrete date-effective layout transition handled by the broader housing and map model; combined/non-uniform pen geometry is not specific to D1.

#### D1 layout history

| Effective dates | D1 layout |
| --- | --- |
| Before 2026-07-29 | Eight cells, D1-01 through D1-08 |
| 2026-07-29 through 2026-08-13 | Seven cells, D1-01 through D1-07 |
| From 2026-08-14 | Five cells, D1-01 through D1-05 |

The current five-cell structure has the size pattern **large, ordinary, large, large, large**. Its corridor begins before D1-04. The preceding seven-cell identities were structurally mapped as follows:

| Legacy source | Current pen |
| --- | --- |
| D1-01 and D1-02 | D1-01 |
| D1-03 | D1-02 |
| D1-04 and D1-05 | D1-03 |
| D1-06 | D1-04 |
| D1-07 | D1-05 |

Historical assignments and maps preserve the layout valid on their date. Current selectors and the current map expose five D1 cells only. No real dog occupancy is published here.

## Related workflows

- [Dogs and lifecycle](dogs-and-lifecycle.md#dog-detail) presents current housing, former housing, co-residents, and the full assignment history where applicable.
- [Daily Entry](daily-entry.md) resolves row membership using housing effective on its selected date; **Find dog** reports when no assignment exists on that date.
- [TULOSTE](daily-entry.md#work-tally-sheets-tuloste) passes the selected Daily Entry date as `housing_as_of`, so sheet placement and D1 structure are historical when required.
- [Training](training.md#housing-proximity-suggestion) reuses canonical physical rectangles for the separate P8 Autumn proximity suggestion.
- [Winter Team Builder](winter-team-builder.md#exact-home-pairing) uses exact current housing identity for exact-home pairing; adjacency on the visual map is not an exact-home pair.
