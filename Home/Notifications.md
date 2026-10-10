# Notifications and Reminders

The Notifications screen UX design is complete. This document defines the behavior, copy, device appearance, and permission states.

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

Free and Premium get the same notifications. The only difference is the daily reminder copy: Free users and Premium users without personalization consent get Today's Verse. Premium users with personalization consent get the check-in nudge for their personal pick.

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

## Device notification appearance

- Use the standard Android and iOS system notification layouts and system text styling; no custom font.
- Use the Stay Positive logo for app identity. Android uses a suitable monochrome small notification icon derived from the logo; iOS uses the app icon.
- Content consists of the title and body only. No attached images or action buttons.
- Tapping opens the destination in the Destinations table.
- Device mockups are illustrative; appearance varies by operating-system version, device, and user settings.

## Notification permission invitation

Device notification permission is separate from personalization consent. Enabling notifications must not enable personalization.

### Copy

**A gentle reminder for your day**

Would you like Stay Positive to remind you to take a moment for your heart?

**Enable notifications**

Maybe later

### Timing and behavior

- New users: offer the invitation at the end of onboarding, after the first mood check-in and verse experience, before Home. It is a separate optional step; skipping it still finishes onboarding.
- Existing users: offer it when they first open the updated Reminders tab, if notification permission has not been requested.
- Users with notifications already enabled do not see the invitation.
- Show the automatic invitation once per installation and remember dismissal. Users can still enable notifications through Reminders.
- **Enable notifications** requests native permission when the OS permits a request. Android and iOS supply the device permission popup.
- **Maybe later** dismisses the invitation without requesting permission or blocking app access.
- If permission was denied and a native request is unavailable, use **Open Settings** instead of attempting another popup.
- Reminder defaults represent saved preferences; they do not grant device permission.

## Notifications disabled state

When device settings prevent app notifications, show a banner at the top of the Reminders tab.

### Copy

**Notifications are turned off**

Enable notifications in your device settings to receive reminders.

**Open Settings**

Your reminder preferences are saved.

### Behavior

- **Open Settings** opens the app's device notification settings, or app settings if a direct notification-settings destination is unavailable.
- If permission has not been requested and a native request remains available, provide the invitation/enable action so users can grant permission in the app.
- Recheck authorization when returning from Settings and when opening Reminders. Remove the banner when notifications are enabled.
- Keep reminder switches and times saved and editable while device notifications are disabled.
- Clearly indicate that reminders cannot be delivered until device notifications are enabled.
- The Updates tab remains available.

## Copy

Titles under ~40 characters, bodies under ~90.

### Daily reminder

| Case | Title | Body |
|---|---|---|
| Free, or Premium without personalization consent | Today's verse | "{verse}" {reference} |
| Premium with personalization consent | How is your heart today? | Check in to see what's chosen for you. |

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

## Implementation issues

- [Kotlin Notifications screen #413](https://github.com/Stay-Positive-Organization/Stay-Positive-Kotlin-App/issues/413)
- [iOS Notifications screen #52](https://github.com/Stay-Positive-Organization/StayPositive-IOS/issues/52)
