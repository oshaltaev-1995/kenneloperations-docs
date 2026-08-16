# Daily Entry

Daily Entry records manual work by kennel row for a selected date and activity. It resolves housing effective on that date, so a historical entry shows dogs who occupied the selected row then rather than today's occupants.

Existing canonical entries hydrate persisted work values and notes. The Find dog workflow can locate a dog outside the initially selected row without rewriting housing history. Saving uses the canonical `daily_entry` source contract.

## Permissions

Admin, Manager, Planner, and Staff can create or save ordinary manual Daily Entry work. Staff authority is limited to the canonical Daily Entry upsert workflow: it does not permit generic activity-session creation, another source such as Operations, Training, Actual, or import, or historical correction/delete. Viewer is read-only.

## Corrections

Admin and Manager can correct/remove a manual Daily Entry session only when its source and canonical reference identify Daily Entry. Planner and Staff can save ordinary work but cannot use this historical correction/delete authority. Operations, Training, Actual, and import sessions are protected from this correction path. Corrections update the authoritative activity representation and its compatibility projection consistently; they do not erase unrelated work.

## Work tally sheets (TULOSTE)

TULOSTE lives under **Daily Entry → Work tally sheets**, not Analytics. Vanha and Uusi exports use the selected Daily Entry date as `housing_as_of`, preserving historical D1 layouts and date-effective housing in the sheet.
