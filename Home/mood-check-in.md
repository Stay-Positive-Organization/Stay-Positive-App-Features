# Mood Check-In

Shared by Free and Premium.

## Layout

Visual details (fonts, sizes, spacing, exact colors) are in Figma.

```text
How is your heart today?                      [🔥5] [🔔]
Take a moment to check in with God and yourself.   ← hidden after check-in

[ Anxious ]  [ Discouraged ]  [ Overwhelmed ]
[ Okay    ]  [ Peaceful    ]  [ Grateful    ]
[             ?  I don't know                ]
```

| Element | Spec |
|---|---|
| Title | "How is your heart today?" |
| Supporting line | "Take a moment to check in with God and yourself." **Shown only until the user checks in today**, then removed. Same for Free and Premium. |
| Right icons | Streak (flame + count) and bell. See streaks.md, notifications.md. |
| Grid | 3 × 2 grid of moods, icon over label |
| `I don't know` | Full-width tile below the grid |

## Tile colors

| State | Tiles |
|---|---|
| Before check-in today | All tiles sand (`surface`), icons and labels in forest |
| After check-in | All tiles switch to their pastel mood color (Figma "When selected" frames) |

Pastel colors (exact hex from Figma):

| Mood | Tile tone |
|---|---|
| Anxious | soft pink, red-brown icon |
| Discouraged | soft blue, slate icon |
| Overwhelmed | soft peach, amber icon |
| Okay | soft green, green icon |
| Peaceful | soft yellow, amber icon |
| Grateful | soft pink, rose icon |
| I don't know | warm grey |

### Selected tile

Not drawn in Figma, so specified here:

- The selected tile keeps its pastel fill and gets a **1.5dp outline in the mood's icon color**.
- Its label switches to semibold.
- The other tiles keep their pastel fill with no outline.
- Expose it as selected for screen readers ("Anxious, selected").

### Selection rules

- One mood is selected at a time.
- Once picked, the mood **stays selected for the rest of the day**. Tapping it again does nothing.
- Tapping a different mood changes the selection.
- The next day, the grid starts unselected (sand tiles) again.

## Options

| Label | Enum |
|---|---|
| Anxious | `ANXIOUS` |
| Discouraged | `DISCOURAGED` |
| Overwhelmed | `OVERWHELMED` |
| Okay | `OKAY` |
| Peaceful | `PEACEFUL` |
| Grateful | `GRATEFUL` |
| I don't know | `UNKNOWN` |

## Behavior

1. Show the selected state immediately.
2. Persist the check-in with a timestamp. A check-in counts as streak activity.
3. Restore the same-day selection on reopening Home.
4. Hide the supporting line.
5. Premium with consent: request today's pick (see daily-content-module.md).
6. Free: persist only; Home content does not change.
7. Changing the mood later: saves a new check-in (`mood_changed`), keeping the earlier one in the history. Premium pick is replaced only if it wasn't opened yet.

Save failure: keep the selection, show "Couldn't save. Retry" under the grid. Never show an unsaved check-in as saved.

## Data

```json
{ "userId": "USER_ID", "mood": "ANXIOUS", "checkedInAt": "2026-09-25T08:15:00Z", "source": "HOME" }
```

`source` is `HOME` or `JOURNAL`. Picking a mood in the journal editor counts as the day's check-in and shows as selected on Home.

## Acceptance criteria

- [ ] All seven options selectable, including `I don't know`.
- [ ] Tiles are sand before check-in and pastel after.
- [ ] Selected tile is visually distinct and announced as selected.
- [ ] Supporting line disappears after check-in and stays hidden that day.
- [ ] Check-in persists, restores the same day, and counts toward the streak.
- [ ] Free: no content change.