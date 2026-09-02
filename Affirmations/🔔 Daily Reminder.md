# Daily Affirmation Reminder

**Last Updated:** September 2, 2026
**Status:** Planned
**Feature Area:** Affirmations

## Overview

The Daily Affirmation Reminder feature allows users to choose a time to receive a notification encouraging them to practice affirmations.

The reminder helps users build a consistent affirmation habit and provides a direct path back to the Affirmations experience.

---

## Goal

Help users practice affirmations consistently by sending one gentle reminder at a time they select.

---

## Feature Name

The feature should be labeled:

**Daily Reminder**

Supporting text:

> Choose when you would like to receive your daily affirmation reminder.

---

## Placement

The Daily Reminder option should be available from:

* The Affirmations home page
* The Affirmation Session completion screen
* Notification settings

Recommended Affirmations page placement:

1. Today's Affirmation
2. Start a Session
3. Daily Reminder
4. Explore Categories
5. Scripture Affirmations
6. Your Space
7. My Affirmations

---

## Initial Reminder Experience

The initial version should allow users to:

* Turn the daily reminder on or off
* Select one reminder time
* Receive one notification each day
* Tap the notification to open Today's Affirmation
* Change the reminder time
* Disable the reminder

Multiple reminders and day-specific schedules can be introduced later.

---

## User Flow

### Enabling the Reminder

1. The user selects **Daily Reminder**.
2. The reminder setup screen opens.
3. The user turns on the Daily Reminder toggle.
4. The user selects a reminder time.
5. The app requests notification permission if it has not already been granted.
6. The user grants permission.
7. The reminder is scheduled.
8. A confirmation message appears.

Example confirmation:

> Daily reminder set for 7:00 AM.

---

## Reminder Setup Screen

The setup screen should display:

* Daily Reminder toggle
* Selected time
* Time picker
* Notification permission status, when applicable
* Confirmation or Save button

Example:

### Daily Reminder

> Take a moment each day to speak encouragement and truth over yourself.

**Daily Reminder**
On

**Reminder Time**
7:00 AM

**Save Reminder**

---

## Default State

The Daily Reminder should be turned off by default.

The app should not send affirmation notifications until the user intentionally enables the feature and grants notification permission.

The time picker may display a suggested time, but the reminder should not be scheduled until the user confirms it.

Recommended suggested time:

**8:00 AM**

---

## Reminder Time

Users should be able to choose a specific time using the device's native time picker.

The selected time should:

* Use the user's local timezone
* Follow the device's 12-hour or 24-hour time format
* Remain saved after the app is closed
* Update when the user changes it
* Adjust appropriately for daylight saving time
* Continue following the user's local time when they travel

Example:

If the reminder is set for 8:00 AM, it should continue arriving at 8:00 AM in the user's current timezone.

---

## Notification Content

The notification should be warm, brief, and supportive.

### Recommended Notification

**Title:** Your daily affirmation is ready

**Message:**

> Take a moment to speak something positive over yourself today.

Alternative messages may include:

* A gentle moment for you: your daily affirmation is ready.
* Begin today with encouragement and intention.
* Pause, breathe, and affirm something good over yourself.
* Take a moment to strengthen your thoughts today.

The initial notification should use general language rather than displaying the full affirmation on the lock screen.

This protects the user's privacy and encourages them to open the app for the complete experience.

---

## Notification Destination

When the user taps the notification, the app should:

1. Open the app.
2. Navigate directly to the Affirmations page.
3. Display Today's Affirmation.
4. Preserve the user's existing sign-in state.

If Today's Affirmation cannot be loaded, the app should display a locally stored fallback affirmation.

---

## Notification Permission

The app should request notification permission only after the user enables Daily Reminder.

Before displaying the system permission request, the app may show a short explanation.

Example:

### Allow affirmation reminders?

> Turn on notifications so Stay Positive can remind you at the time you selected.

**Continue**
**Not Now**

Selecting **Continue** should open the device's notification permission prompt.

---

## Permission Denied

If the user denies notification permission:

* Do not schedule the reminder.
* Explain that permission is required.
* Provide an option to open the device settings.
* Keep the rest of the Affirmations experience available.

Example:

### Notifications are turned off

> Enable notifications in your device settings to receive your daily affirmation reminder.

**Open Settings**
**Not Now**

The Daily Reminder toggle should remain off unless the app can schedule and deliver the notification.

---

## Changing the Reminder Time

Users should be able to change their selected reminder time at any point.

When the time changes:

* Cancel the previously scheduled notification.
* Schedule the reminder at the new time.
* Save the new time.
* Display a confirmation message.

Example:

> Daily reminder updated to 9:30 PM.

Only one active daily affirmation reminder should exist in the initial version.

---

## Disabling the Reminder

When the user turns the Daily Reminder toggle off:

* Cancel the scheduled notification.
* Preserve the previously selected time for convenience.
* Stop sending daily affirmation reminders.
* Update the user interface immediately.

Example confirmation:

> Daily reminder turned off.

If the user enables it again, the previously selected time may be restored.

---

## Device Restart and App Updates

The reminder should remain scheduled after:

* The app is closed
* The device is restarted
* The app is updated
* The user signs out, if reminders are stored locally

The implementation should recreate scheduled reminders when required by the operating system.

---

## Authentication

Users should not be required to sign in to set a Daily Reminder.

The reminder schedule may be stored locally on the device.

If reminder preferences are synchronized across devices in the future, authentication will be required for synchronization.

---

## Offline Behavior

The reminder should still be delivered when the device is offline because it should be scheduled locally.

When the notification is opened without an internet connection:

* Display the cached daily affirmation, if available.
* Otherwise, display a locally stored fallback affirmation.
* Keep the rest of the available Affirmations page functional.

---

## Functional Requirements

* Daily Reminder is turned off by default.
* Users can intentionally enable the reminder.
* Users can select one reminder time.
* The app requests notification permission when needed.
* The reminder is scheduled only after permission is granted.
* Users receive one notification each day.
* The notification follows the user's local timezone.
* Tapping the notification opens Today's Affirmation.
* Users can change the reminder time.
* Changing the time replaces the existing schedule.
* Users can disable the reminder.
* Disabling the reminder cancels future notifications.
* Only one active daily affirmation reminder exists.
* The reminder remains scheduled after the app is closed.
* The notification can be delivered while the device is offline.

---

## Suggested Data Structure

```text
Daily Reminder
├── Reminder ID
├── User ID, if available
├── Enabled status
├── Reminder time
├── Timezone
├── Notification permission status
├── Created timestamp
└── Updated timestamp
```

For the initial version, this information may be stored locally on the user's device.

---

## Error Handling

If the reminder cannot be scheduled:

* Keep the Daily Reminder toggle off.
* Explain that the reminder could not be created.
* Allow the user to try again.

Example:

> We couldn't set your reminder. Please try again.

**Try Again**

If the device does not allow notifications, direct the user to the device settings instead of repeatedly requesting permission.

---

## Accessibility

* The Daily Reminder toggle should have a descriptive label.
* The selected time should be announced clearly by screen readers.
* The time picker should support assistive technologies.
* Permission instructions should use clear language.
* The feature should not rely only on color to communicate whether it is enabled.
* Buttons and controls should have accessible touch targets.
* Text should remain readable at larger device font sizes.

---

## Analytics

The following events may be tracked:

* Reminder setup opened
* Reminder enabled
* Notification permission granted
* Notification permission denied
* Reminder time selected
* Reminder time changed
* Reminder disabled
* Reminder notification delivered
* Reminder notification opened

Analytics should not collect private affirmation content.

---

## Acceptance Criteria

The feature is complete when:

* The user can open the Daily Reminder setup screen.
* The user can select a reminder time.
* Notification permission is requested only after the user enables the feature.
* A reminder is scheduled after permission is granted.
* The user receives one notification at the selected local time.
* Tapping the notification opens Today's Affirmation.
* The user can change the reminder time.
* The previous schedule is canceled when the time changes.
* The user can disable the reminder.
* No reminder is delivered after the feature is disabled.
* The reminder remains scheduled after the app is closed or the device restarts.
* A permission-denied state directs the user to device settings.

---

## Future Enhancements

Possible future additions include:

* Multiple reminders per day
* Different schedules for different days
* Morning and evening reminder presets
* Reminder message customization
* Full affirmation text in notifications
* Scripture affirmation reminders
* Affirmation Session reminders
* Reminders connected to specific Favorites
* Personalized notification content
* Snooze option
* Notification action to save the affirmation
* Reminder history
* Cross-device preference synchronization
