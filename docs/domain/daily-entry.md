# Daily Entry

Daily Entry records manual work by kennel row for a selected date and activity. It resolves housing effective on that date, so a historical entry shows dogs who occupied the selected row then rather than today's occupants.

Existing canonical entries hydrate persisted work values and notes. The Find dog workflow can locate a dog outside the initially selected row without rewriting housing history. Saving uses the canonical `daily_entry` source contract.

## Corrections

Authorized managers can correct/remove a manual Daily Entry session only when its source and canonical reference identify Daily Entry. Operations, Training, Actual, and import sessions are protected from this correction path. Corrections update the authoritative activity representation and its compatibility projection consistently; they do not erase unrelated work.

## Work tally sheets (TULOSTE)

TULOSTE lives under **Daily Entry → Work tally sheets**, not Analytics. Vanha and Uusi exports use the selected Daily Entry date as `housing_as_of`, preserving historical D1 layouts and date-effective housing in the sheet.
