# System overview

Kennel Operations turns kennel records and daily schedules into safe, traceable work plans.

The current production application reference is `500c8be9ea24c4a7f66e8a0b1c7aec797f23a29f`, deployed on 16 August 2026. Its post-release update added narrow Staff Daily Entry/current-housing execution permissions and read-only full-size Dog Detail photo viewing; the schema head remains `a7c3d9e1f502`.

Dashboard is the date-selectable operational landing view. It summarizes current population, eligibility, completed work, training distance and Carousel exposure, workload distribution, workload-review dogs, and planning blockers. Its links open the filtered Dogs views or Kennel Map without making the Dashboard a second activity ledger.

The dog registry owns identity, work class, lifecycle, capabilities, status, housing, and historical presentation. Date-effective assignments allow the map, Daily Entry, and historical views to resolve housing for the relevant date. Kennel Map projects those records onto the physical ground geometry and provides current relocation controls while keeping historical layouts read-only.

Operations Plans represent customer-facing Winter work. Departures originate in Explores or manual entry, are reviewed, assigned to Vanha or Uusi, populated by the Winter solver, saved, printed, and reconciled to Actual work.

Training is a separate manual workspace. Saved Groups organize dogs; Daily Plans are independent snapshots that enforce readiness. Autumn uses explicit manual Lead/Team/Wheel rows. Carousel records duration and prints names only.

Daily Entry records manual row-based work against the housing layout effective on the chosen date. TULOSTE sheets live in Daily Entry. Analytics summarizes full authoritative activity history and can export XLSX, PDF, and CSV.

Archive and Deceased profiles are historical rather than operational. Permanent deletion is an exceptional management action for archived, unreferenced erroneous records only.

## Architectural boundaries

| Concern | Owner |
| --- | --- |
| Winter automatic solver | Operations only |
| Autumn and Carousel | Manual Training workflows |
| Saved Group | Organizational membership |
| Daily Plan Ready | Operational safety validation |
| TULOSTE | Daily Entry |
| Current Housing Summary | Full-period work grouped by current housing, not historical utilization |
| Archive | Historical lifecycle |
