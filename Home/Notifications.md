# Notifications and Reminders

The Notifications screen is still being finished in Figma (the current frames use placeholder rows). This doc defines the behavior and copy.

## Home bell

Bell in the check-in title row. Gold dot when there are unread updates. Content description "Notifications, {n} unread". Minimum 44 × 44dp tap area.

## Notifications screen

Top bar: Back, "Mark all as read". Title "Notifications". Tabs: **Updates** and **Reminders**.

**Updates:** grouped Today / Yesterday / Earlier this week. Row: icon circle, title, body, time. Unread rows have a gold dot. Tapping marks read and opens the destination. Empty state: "You're all caught up."

**Reminders:** intro "Choose when Stay Positive gently reminds you. You can change these any time."

| Setting | Default | Time |
|---|---|---|
| Daily reminder | On | 8:00 AM |
| Evening prayer | Off | 9:00 PM |
| Streak reminder ("Only sent if you haven't done anything yet that day.") | Off until the user's first 3-day streak, then on | 7:00 PM |
| New stories | On | — |
| Quiet hours | On | 10:00 PM – 7:00 AM |

Each row: icon, label, description, time chip (disabled when off), switch. Footer: "We'll never send more than two notifications a day, and never during a meditation or prayer."

## Destinations

| Notification | Opens |
|---|---|
| Daily reminder | Home |
| Evening prayer | Prayer tab |
| Streak reminder | Home |
| Streak milestone | Your streak |
| New Story | That Story |

## Who gets what

Free and Premium get the same notifications. The only difference is the daily reminder copy: Premium users who consented get the check-in nudge for their personal pick; Free users get Today's Verse.

## Updates history

The Updates tab keeps the last **30 days**. Older items are deleted automatically.

## Delivery rules

- Maximum two per user per day.
- Nothing during quiet hours; deferred pushes are dropped.
- Nothing while meditation, prayer or journaling is open.
- Daily reminder skipped once the user has opened today's card. Streak reminder skipped once the user has any activity that day.
- Alex never sends notifications.
- Never include journal or prayer text.
- Android channels: Reminders, Stories.

## Copy

Titles under ~40 characters, bodies under ~90.

### Daily reminder

| Case | Title | Body |
|---|---|---|
| Free, or Premium not checked in | Today's verse | "{verse}" {reference} |
| Premium, nudge to check in | How is your heart today? | Check in to see what's chosen for you. |

Personalized content depends on a check-in, so the morning notification can't name a pick before the user checks in.

### Streak

| Case | Title | Body |
|---|---|---|
| Reminder (7 PM, nothing yet today) | A moment for your heart | Even a quick check-in keeps your streak going. |
| 3 days | 3 days in a row | You've made space for your heart three days running. |
| 7 days | A full week | Seven days of showing up for yourself and for God. That matters. |
| 30 days | 30 days in a row | A month of quiet moments. Thank you for making this time. |

Milestones go out once, the morning after. No notification when a streak breaks.

### Other

| Case | Title | Body |
|---|---|---|
| Evening prayer | Evening prayer | Close your day with a short prayer before bed. |
| New Story | A new story | "{title}" by {authorName} (or "from Stay Positive" if no author) |

## Analytics

```text
notifications_opened
notification_tapped       { type }
notifications_mark_all_read
reminder_toggled          { reminder, enabled }
reminder_time_changed     { reminder }
push_sent / push_opened   { type }
```