# Daily Card: Today's Verse and For your heart today

The forest-green card under the mood check-in.

| Plan | Before check-in | After check-in |
|---|---|---|
| Free | Today's Verse | Today's Verse |
| Premium (consented) | Today's Verse | For your heart today |
| Premium (no consent) | Today's Verse | Today's Verse |

## Shared frame

Visual details are in Figma.

| Property | Value |
|---|---|
| Background | `forest` |
| Label | Gold line + "Today's verse" or "For your heart today" |
| Primary button | warmWhite pill, forest text, "›" |
| Inner panel (pick only) | Lighter forest panel |

## Today's Verse (`DailyContentCard`)

Verse, reference in `goldOnForest`, button "Read full chapter ›", sprig illustration on the right. Editorially scheduled, morning/night rotation, never described as chosen for the user. Opening it counts as streak activity.

**Read full chapter** opens the existing in-app Bible reader at the verse's chapter, scrolled to and highlighting the verse. The prayer end screen uses the same reader.

## For your heart today (`HeartPickCard`)

```text
— For your heart today
Chosen for you                          ("Your page is ready" for journaling)
Based on how you've been feeling today.
✦ {Type}
┌───────────────────────────────┐
│ type-specific content          │
│ [ CTA › ]                      │
└───────────────────────────────┘
```

The line "Based on how you've been feeling today." never names the mood. It always shows, because a pick only appears after today's check-in.

### Pick types

| Type | `contentType` | Inner panel | CTA | Opens | In Figma |
|---|---|---|---|---|---|
| Meditation | `MEDITATION` | Thumbnail, "A moment of peace", one-line description | Start meditation › | Meditation player | Yes |
| Affirmation | `AFFIRMATION` | One affirmation, heart below | None (heart saves to Affirmations favorites) | — | Yes |
| Prayer | `PRAYER` | First lines of the prayer, italic, ending "…" | Pray now › | Guided prayer | Yes |
| Talk with Alex | `ALEX` | "A" avatar + message bubble from Alex | Reply to Alex › | Talk with Alex | Yes |
| Journaling | `JOURNALING` | Page box "Today, I…" | Start writing | Journaling | Yes |

Rules:
- One affirmation, never a list. Viewing it counts as streak activity; the heart saves it.
- Journaling never shows a prompt question.
- The Alex message appears only inside this card; Alex never sends notifications.

### How the pick is chosen (Phase 1: rules)

Phase 1 uses simple rules. Move to a learned model only once there's enough analytics per user.

**1. Each mood has an ordered list of pick types.**

| Mood | Types, in order of preference |
|---|---|
| Anxious | Meditation, Prayer, Affirmation, Talk with Alex |
| Discouraged | Affirmation, Prayer, Talk with Alex, Journaling |
| Overwhelmed | Meditation, Journaling, Prayer, Talk with Alex |
| Okay | Journaling, Affirmation, Meditation, Prayer |
| Peaceful | Meditation, Journaling, Prayer, Affirmation |
| Grateful | Journaling, Prayer, Affirmation, Meditation |
| I don't know | Journaling, Prayer, Meditation, Talk with Alex |

**2. Pick the type.** Go down the mood's list and take the first type that:
- isn't the same type the user got yesterday, and
- has at least one eligible item.

**3. Pick the item within the type.** Choose content tagged with the mood that the user hasn't been shown in the last 14 days, preferring items they've never opened. Journaling and Talk with Alex have no items; they just open the editor or chat.

**4. Fallback.** If nothing qualifies, show Today's Verse.

Content tagging: every meditation, prayer and affirmation item needs one or more mood tags (`ANXIOUS`, `DISCOURAGED`, …) so the rules can find it. Store the chosen pick per user per day so it stays stable.

### After the pick is finished

No completed state. The card stays as it is for the rest of the day.

### Changing mood the same day

| Today's pick | New mood selected |
|---|---|
| Not opened | Request a new pick |
| Opened or finished | Keep the pick |

## Loading and fallback

| Case | Behavior |
|---|---|
| Waiting | Skeleton bars inside the forest card |
| Pick available | `HeartPickCard` |
| Error / timeout / content removed | `DailyContentCard` |

The card is never empty.

## Analytics

```json
// heart_pick_viewed / heart_pick_opened / heart_pick_completed
{ "pickId": "PICK_ID", "contentType": "MEDITATION", "mood": "ANXIOUS", "rule": "MOOD_LIST_V1" }
```

## Acceptance criteria

- [ ] Free always sees Today's Verse.
- [ ] Premium sees Today's Verse before check-in and the pick after (with consent).
- [ ] Each type matches Figma and opens the right destination.
- [ ] Mood change replaces only an unopened pick.
- [ ] Error falls back to Today's Verse.
- [ ] The card never names the mood.