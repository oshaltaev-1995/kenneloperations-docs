# Workload and activity

## Canonical record structure

`ActivitySession` is the event/session header: date/time, activity type, source, distance/program context, notes, and removal/correction state. `DogActivityRecord` links participating dogs to that session and stores their per-dog result.

`Worklog` remains a compatibility history for older and mirrored workflows. It must not be summed independently with matching `DogActivityRecord` rows as though the two were separate work ledgers. Services select a canonical meaningful-work projection and exclude removed records and zero-work chronology rows where appropriate.

## Actual and projected workload

- **Current/actual workload** comes from completed authoritative activity.
- **Projected workload** adds saved or candidate assignments without creating Actual work.
- Same-day planning evaluates existing assignments and candidate occupancy together.
- Critical workload excludes a dog from automatic generation. Elevated and High produce increasingly strong warnings; hard lifecycle/availability blocks are separate and stronger.

## Verified runtime thresholds

| Signal | Normal | Elevated | High | Critical |
| --- | --- | --- | --- | --- |
| Daily or short starts | 0–3 | 4–5 | 6+ | — |
| Long starts | 0–2 | — | 3 | 4+ |
| Daily distance | <25 km | 25–<35 km | 35–<45 km | 45+ km |
| Starts over 3 days | 0–9 | 10–13 | 14–17 | 18+ |
| Starts over 7 days | 0–20 | 21–27 | 28–34 | 35+ |
| Distance over 7 days | <90 km | 90–<120 km | 120–<150 km | 150+ km |

Recovery is insufficient below 30 minutes, adequate from 30 to under 45 minutes, and excellent from 45 minutes. These signals feed a multi-axis risk result; they are not a substitute for health or lifecycle eligibility.

The legacy hard-day count remains a reporting field and commonly uses a 10 km or 15 km caller threshold. It does not redefine the canonical risk classification above.
