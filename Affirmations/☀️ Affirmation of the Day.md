# Affirmation of the Day

**Last Updated:** September 2, 2026
**Status:** Planned
**Feature Area:** Affirmations

## Overview

The Affirmation of the Day feature presents users with one featured affirmation each day.

It gives users an immediate affirmation to read and reflect on without requiring them to browse through categories. The daily affirmation also gives users a reason to return to the Affirmations page regularly.

---

## Goal

Encourage users to build a consistent affirmation practice by providing one meaningful affirmation each day.

---

## Feature Name

The feature should be labeled:

**Today's Affirmation**

This title feels more personal and natural within the user interface than “Affirmation of the Day.”

“Affirmation of the Day” may still be used internally as the feature name.

---

## Placement

Today's Affirmation should appear near the top of the Affirmations home page, before **Explore Categories**.

Recommended page order:

1. Today's Affirmation
2. Explore Categories
3. Scripture Affirmations
4. Your Space
5. My Affirmations

This placement ensures users immediately see an affirmation when opening the page.

---

## User Flow

When the user opens the Affirmations page:

1. The app retrieves the affirmation assigned to the current day.
2. The affirmation appears inside the Today's Affirmation card.
3. The user can read, save, or share the affirmation.
4. The same affirmation remains available for the entire day.
5. A new affirmation appears on the following calendar day.

---

## Today's Affirmation Card

The card should display:

* **Today's Affirmation** label
* Affirmation text
* Category, if applicable
* Favorite button
* Share button

Example:

### Today's Affirmation

> “I am capable of handling whatever today brings.”

**Confidence**

♡ Save  ↗ Share

---

## Daily Affirmation Behavior

* One affirmation should be assigned to each calendar day.
* The affirmation should remain the same throughout that day.
* Closing and reopening the app should not change it.
* Refreshing the page should not generate another affirmation.
* A new affirmation should appear when the next calendar day begins.
* The date should follow the user's local timezone.
* Users should not receive the same affirmation on consecutive days when avoidable.

---

## Affirmation Selection

For the initial version, the daily affirmation should be selected from the existing standard affirmation library.

The selection process should:

* Use only active and approved affirmations.
* Avoid repeating the previous day's affirmation.
* Distribute affirmations across different categories.
* Avoid displaying duplicate affirmation records.
* Return the same assigned affirmation for the entire day.

Scripture affirmations may be added to the daily rotation in a future version.

---

## Saving the Daily Affirmation

Users can tap the heart icon to save the daily affirmation to Favorites.

**Default state:**
♡ Not saved

**Saved state:**
♥ Saved

When saved:

* The affirmation is added to Favorites.
* The heart changes to its active state.
* The saved state persists across sessions.
* The state updates everywhere the affirmation appears.

Tapping the active heart again removes the affirmation from Favorites.

---

## Sharing the Daily Affirmation

Users can tap the share button to share the affirmation using the device's available sharing options.

The shared content should include:

* Affirmation text
* Stay Positive attribution or branding
* App link, when available

Example:

> “I am capable of handling whatever today brings.”
>
> Stay Positive

---

## Loading State

While the daily affirmation is being retrieved, the app should display a loading placeholder that matches the approximate shape of the card.

The page should not appear broken or display an empty card during loading.

---

## Error State

If the daily affirmation cannot be retrieved:

* Display a fallback affirmation stored within the app.
* Allow the user to continue using the rest of the Affirmations page.
* Attempt to retrieve the assigned affirmation again when appropriate.

Example fallback affirmation:

> “I am worthy of patience, peace, and compassion today.”

The error should not prevent the entire Affirmations page from loading.

---

## Offline Behavior

If the user opens the app without an internet connection:

* Display the previously loaded daily affirmation, if available.
* Otherwise, display a locally stored fallback affirmation.
* Do not leave the daily affirmation section empty.

---

## Authentication

Users should be able to view Today's Affirmation without signing in.

Authentication is required when the user wants to save the affirmation to Favorites and Favorites are connected to a user account.

If an unauthenticated user taps the heart button, the app should prompt them to sign in or create an account.

Sharing does not require authentication.

---

## Functional Requirements

* The Affirmations page displays one featured affirmation each day.
* The same affirmation remains visible for the entire calendar day.
* A new affirmation becomes available on the following day.
* The feature uses the user's local date and timezone.
* Refreshing or reopening the page does not change the affirmation.
* The daily affirmation is selected from approved content.
* Consecutive repeats should be avoided.
* Users can save the affirmation to Favorites.
* Users can remove it from Favorites.
* Users can share the affirmation.
* The affirmation remains available during temporary network failures.
* The rest of the page remains usable if the daily affirmation fails to load.

---

## Suggested Data Structure

Each daily affirmation assignment may include:

```text
Daily Affirmation
├── Date
├── Affirmation ID
├── Affirmation text
├── Category
├── Content status
└── Created or assigned timestamp
```

The assigned affirmation should reference an existing affirmation record instead of creating a duplicate.

Example relationship:

```text
Daily Affirmation
└── Affirmation ID
    └── Original Affirmation
```

---

## Accessibility

* The affirmation text should support screen readers.
* The heart button should use a descriptive accessibility label:

  * **Save affirmation**
  * **Remove affirmation from Favorites**
* The share button should be labeled:

  * **Share today's affirmation**
* Saved and unsaved states should not rely only on color.
* Buttons should have accessible touch targets.
* Text should remain readable when the device's font size is increased.

---

## Analytics

The following events may be tracked:

* Daily affirmation viewed
* Daily affirmation saved
* Daily affirmation removed from Favorites
* Daily affirmation shared
* Sign-in prompt opened from the daily affirmation

Analytics should not collect the user's private affirmation content.

---

## Acceptance Criteria

The feature is complete when:

* Today's Affirmation appears above Explore Categories.
* The user sees one approved affirmation for the current day.
* The affirmation does not change when the page is refreshed.
* The affirmation does not change when the app is reopened on the same day.
* A new affirmation appears on the following day.
* The user can save and remove the affirmation from Favorites.
* The user can share the affirmation.
* A fallback affirmation appears if the daily content cannot be retrieved.
* The feature works for authenticated and unauthenticated users.

---

## Future Enhancements

Possible future additions include:

* Personalized daily affirmations based on selected interests
* Scripture affirmation of the day
* Daily affirmation notifications
* Audio playback
* Reflection or journaling prompt
* Affirmation history
* Calendar of previous daily affirmations
* Mood-based affirmation recommendations
* Custom reminder times
* Shareable branded affirmation images
