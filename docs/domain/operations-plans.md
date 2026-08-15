# Operations Plans

An Operations Plan holds one operational date and its departures. A departure owns authoritative context: scheduled time, program, distance, PAX, operational area, target team count, status, planned teams, persisted harness rows, and optional Actual.

## Workflow

```text
Explores Preview/Apply or manual departure
  -> review program, PAX, area, and target teams
  -> Build teams
  -> save planned rosters and harness rows
  -> print Vanha/Uusi daily team sheets
  -> confirm or correct Actual
```

Explores supplies external schedule identity and customer context. Manual operational-area overrides remain local. An unresolved area prevents unsafe side-specific planning/printing until an operator assigns Vanha or Uusi.

The Winter automatic solver is entered from an Operations departure. Generated output is only a proposal; saved teams and `PlannedTeamHarnessRow` records are the persisted plan. Editing uses optimistic revision checks to prevent stale overwrites.

## Review teams

Once a departure has saved teams, the same entry point becomes **Review teams**. It opens the compact saved lineup in persisted Lead/Team/Wheel rows and re-evaluates projected workload for the plan date and departure. Operator-facing Normal, Elevated, High, Critical, confirmation, and hard-blocker messages are shown without exposing internal ranking-penalty numbers.

Warnings remain review evidence, not silent mutations. Human-readable Explores differences show saved and incoming values while protecting existing operator-owned lineup, Actual, and area decisions. Temporal conflicts or incomplete workload projections remain visible for deliberate review before a team is changed or saved.

## Print families

Winter and Autumn use the accepted Model-style card family, but their geometry comes from different persisted sources: generated/saved Winter harness rows versus manual Autumn rows. Guide notes remain with their team/group. Carousel print is deliberately names-only and has no housing, statuses, or fabricated pairs.
