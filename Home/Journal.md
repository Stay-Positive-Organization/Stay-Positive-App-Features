# Journal

Journal is a bottom-navigation tab. It is **not** a section on Home (Figma has no Journal section on Home). Journaling from the Home card is covered in [pick-destinations.md](pick-destinations.md#4-journaling).

## Journal tab

| Area | Spec |
|---|---|
| Header | "Journal" with a lock line "Only you can see your entries", calendar icon on the right |
| New entry | Large forest button at the top: "New entry" / "Write whatever is on your heart" |
| Ways to start | Two cards side by side under New entry: **Explore prompts** (Free and Premium) and **Talk it through** (Premium). Free users see a 🔒 PREMIUM badge on Talk it through; tapping it opens the upgrade screen. |
| Gratitude journey | The 30 Days of Gratitude card, full size, under the two cards |
| List | Entries grouped by month (gold label). Row: day number, weekday, a small gold label, two-line preview, mood if set. The label is the prompt's topic for Explore entries ("TRAVEL AND ADVENTURE"), "TALK IT THROUGH · GUIDED" or "· WITH ALEX" for Talk it through entries, and "ENTRY" otherwise. |
| Ad banner | Free only, above the bottom navigation, with "Remove ads" above it (same banner as Home) |
| Empty state | Journal illustration, "Your page is ready", short reassuring line, "Write your first entry" |

One Journal tab for everyone; Free and Premium differ only in the badge and the ad banner. Design: [Figma › Journaling V3 › Journal tab](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=3134-829).

## Editor

Same editor as journaling from the Home card, without the "For your heart today" label:
- Free-text page with ruled lines and the "Today, I…" placeholder. No prompts.
- Mood chip from today's check-in (removable), or the optional mood grid if there's no check-in.
- Picking a mood in the editor **counts as today's check-in**: it is saved like a Home check-in (`source: "JOURNAL"`), Home shows it as selected, and for consented Premium users it triggers today's personal pick.
- Mic for dictation; footer "Saved privately. Voice isn't recorded."
- Draft saves automatically. Done saves; empty entries are discarded.

## Entry view

Full text with date, time and mood. Overflow menu: Edit, Delete. Any entry can be edited, including entries from earlier days; edits keep the original date. Delete confirms in a bottom sheet: "Delete this entry?" / "It will be removed from your journal and can't be recovered." [Delete entry] [Keep it].

## Guided gratitude journey

The Journaling screen also includes **30 Days of Gratitude**, a guided journey with 30 prompts, private saved reflections, and persistent completion progress. See the [30 Days of Gratitude specification](../Journaling/30-days-of-gratitude.md) for the entry card, overview, editor behavior, exact prompts, and acceptance criteria.

The no-prompts editor behavior above applies to regular free-writing. Gratitude entries display their assigned prompt while reusing the same journal storage, privacy, and editing behavior.

## Explore prompts

An optional **Explore prompts** browser shows one reviewed prompt at a time, with unlimited skipping and a topic filter, then opens the editor with the prompt attached. Free and Premium. See [Explore prompts](../Journaling/explore-prompts.md) and the shared [prompt collection](../Journaling/prompt-collection.md).

## Talk it through (Premium)

Conversational journaling: the person writes or speaks, and a Guided listener or Alex replies with one gentle question. The conversation is saved as one private entry. See [Talk it through](../Journaling/talk-it-through.md).

## Privacy

- Entries are readable only by their owner (Firestore security rules).
- Entry text never appears on Home, in notifications, or in analytics.
- Entries are not used for personalization unless the user explicitly agrees.

## Acceptance criteria

- [ ] New entry, edit and delete work; empty entries are not saved.
- [ ] Mood chip or grid appears correctly.
- [ ] Dictation works and stores no audio.
- [ ] Another signed-in user cannot read the entries.