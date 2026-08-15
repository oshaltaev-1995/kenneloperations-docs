# Housing and kennel map

Housing is date-effective history, not merely the current tuple stored for convenient reads. A housing identity consists of kennel side, kennel row, and home slot. `DogHousingAssignment` records effective intervals; historical features resolve the assignment for their reference date.

The kennel map supports current and historical layouts. Current move/create selectors accept only current pens. A former code may remain visible in historical context but must be explicitly remapped before a current edit is saved.

## D1 layout eras

| Effective dates | D1 layout |
| --- | --- |
| Before 2026-07-29 | Eight cells, D1-01 through D1-08 |
| 2026-07-29 through 2026-08-13 | Seven cells, D1-01 through D1-07 |
| From 2026-08-14 | Five cells, D1-01 through D1-05 |

The five-cell cutover structurally mapped the preceding seven-cell identities:

| Legacy source | Current pen |
| --- | --- |
| D1-01 and D1-02 | D1-01 |
| D1-03 | D1-02 |
| D1-04 and D1-05 | D1-03 |
| D1-06 | D1-04 |
| D1-07 | D1-05 |

Historical assignments and maps preserve the layout valid on their date. Current selectors and the current map expose five cells only. The documentation intentionally does not publish real occupancy.

## Consumers

- Dog Detail presents current and historical housing.
- Kennel Map resolves layout and occupancy for its reference date.
- Daily Entry resolves which dogs belonged to a row on the selected date.
- TULOSTE uses the selected Daily Entry date as `housing_as_of`.
- Winter exact-home pairing uses the exact current housing identity; it is not based on adjacent pens.
- Autumn proximity suggestions use physical pen rectangles for the selected layout era.
