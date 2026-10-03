# Streaks

## Definition

A streak is the number of consecutive days, ending today or yesterday, with **at least one activity**. Same rule for Free and Premium. Days use the user's local time zone. Opening or viewing something counts.

| Activity | Counts when |
|---|---|
| Mood check-in | Saved (including `I don't know`) |
| Today's Verse | Opened |
| For your heart today | Opened |
| Meditation | Opened |
| Prayer | Opened |
| Affirmation | Viewed |
| Journal | An entry is saved |
| Story | Opened |
| Quote | "See more" tapped, saved or shared (seeing the card on Home doesn't count) |
| Talk with Alex (Premium) | A message is sent |
| Reset Routine (Premium) | Opened |

One activity is enough; several on the same day still count as one day. If there's no activity yet today, the streak shows yesterday's count until midnight.

Grace days (a missed day that doesn't break the streak) are Phase 2.

## Home icon

Flame + count on the right of the check-in title row, next to the bell. Opens Your streak. Content description "{n}-day streak". At 0, show the flame without a number. Minimum 44 × 44dp tap area.

## Your streak screen (as in Figma)

Visual details are in Figma.

| Section | Spec |
|---|---|
| Title | "Your streak" |
| Hero card | Flame, count, "days in a row", supporting line: "You've made time for your heart every day since {weekday}." for streaks under 7 days; "… every day since {Month day}." from 7 days on. |
| Date picker | Year, month and day; scrolling changes the calendar month. Range: from the user's first day in the app up to today. No future dates. |
| Calendar | Sun–Sat. Adjacent-month days faded. Days with activity highlighted; today marked. |

Not in MVP: longest streak, totals, milestones, reminder link.

## Tone

- Missed days are blank, never red.
- No notification when a streak breaks.
- No guilt language.

## Data

```json
{ "userId": "USER_ID", "date": "2026-04-16", "activity": "JOURNAL_ENTRY", "at": "2026-04-16T09:52:00Z" }
```

`activity`: `MOOD_CHECKIN`, `DAILY_VERSE`, `HEART_PICK`, `MEDITATION`, `PRAYER`, `AFFIRMATION`, `JOURNAL_ENTRY`, `STORY`, `QUOTE`, `ALEX_MESSAGE`, `RESET_ROUTINE`. Store only type and time, never content. Compute the streak server-side so it matches across devices.

## Analytics

```text
streak_opened      { currentStreak }
streak_milestone   { milestone }   // 3, 7, 30 — used for milestone notifications
```