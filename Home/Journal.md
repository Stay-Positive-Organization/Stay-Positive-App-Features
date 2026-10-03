# Journal

Journal is a bottom-navigation tab. It is **not** a section on Home (Figma has no Journal section on Home). Journaling from the Home card is covered in [pick-destinations.md](pick-destinations.md#4-journaling).

## Journal tab

| Area | Spec |
|---|---|
| Header | "Journal" with a lock line "Only you can see your entries" |
| New entry | Large forest button at the top: "New entry" / "Write whatever is on your heart" |
| List | Entries grouped by month (gold label). Row: day number, weekday, two-line preview, mood if set. |
| Empty state | Journal illustration, "Your page is ready", short reassuring line, "Write your first entry" |

## Editor

Same editor as journaling from the Home card, without the "For your heart today" label:
- Free-text page with ruled lines and the "Today, I…" placeholder. No prompts.
- Mood chip from today's check-in (removable), or the optional mood grid if there's no check-in.
- Picking a mood in the editor **counts as today's check-in**: it is saved like a Home check-in (`source: "JOURNAL"`), Home shows it as selected, and for consented Premium users it triggers today's personal pick.
- Mic for dictation; footer "Saved privately. Voice isn't recorded."
- Draft saves automatically. Done saves; empty entries are discarded.

## Entry view

Full text with date, time and mood. Overflow menu: Edit, Delete. Any entry can be edited, including entries from earlier days; edits keep the original date. Delete confirms in a bottom sheet: "Delete this entry?" / "It will be removed from your journal and can't be recovered." [Delete entry] [Keep it].

## Privacy

- Entries are readable only by their owner (Firestore security rules).
- Entry text never appears on Home, in notifications, or in analytics.
- Entries are not used for personalization unless the user explicitly agrees.

## Acceptance criteria

- [ ] New entry, edit and delete work; empty entries are not saved.
- [ ] Mood chip or grid appears correctly.
- [ ] Dictation works and stores no audio.
- [ ] Another signed-in user cannot read the entries.