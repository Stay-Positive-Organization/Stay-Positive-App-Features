# Favorites / Saved Affirmations

**Last Updated:** September 2, 2026
**Status:** Planned
**Feature Area:** Affirmations

## Overview

The Favorites feature allows users to save affirmations that resonate with them so they can easily return to them later.

Instead of searching through affirmation categories each time, users can build a personal collection of affirmations they find meaningful.

---

## Goal

Give users a simple way to create a personalized collection of affirmations they want to revisit regularly.

---

## User Flow

### Saving an Affirmation

When viewing an affirmation, the user can tap a heart icon to save it.

**Default state:**
♡ Not saved

**Saved state:**
♥ Saved

When the user taps the heart:

1. The affirmation is added to Favorites.
2. The heart changes to the active saved state.
3. The saved state persists across sessions.

If the user taps the active heart again, the affirmation is removed from Favorites.

---

## Favorites Section

A **Favorites** option should appear within the user's personalized affirmation area.

Example:

### Your Space

* ♡ Favorites
* ＋ Write Your Own

When the user selects **Favorites**, they are taken to a page containing all the affirmations they have saved.

---

## Favorites Page

### Header

**Favorites**

Supporting text:

> Affirmations you've saved for whenever you need them.

### Affirmation List

Each saved affirmation should display:

* Affirmation text
* Heart or saved indicator
* Category, if applicable
* More/options menu, if needed

Example:

> “I am worthy of love and belonging.”

♥ Saved

---

## Removing a Favorite

Users can remove an affirmation from Favorites by tapping its active heart icon.

After removal:

* The affirmation disappears from the Favorites collection.
* Its heart returns to the unsaved state everywhere else in the app.
* The user interface updates immediately.

---

## Empty State

If the user has not saved any affirmations, the Favorites page should display:

### No favorites yet

> Save the affirmations that speak to you, and they'll appear here.

**Explore Affirmations →**

The call-to-action should return the user to the affirmation categories.

---

## Supported Affirmation Types

Users should be able to favorite:

* Standard affirmations
* Scripture affirmations

Custom affirmations created by the user do not need to be favorited because they already appear under **My Affirmations**.

---

## Functional Requirements

* Users can save an affirmation.
* Users can remove a saved affirmation.
* Saved affirmations persist between app sessions.
* Saved affirmations are associated with the user's account.
* The saved state is synchronized everywhere the affirmation appears.
* Users can view all saved affirmations in one location.
* Duplicate favorites cannot be created.
* Removing a favorite updates the user interface immediately.
* Removing a favorite from one screen updates its status on all other affirmation screens.

---

## Authentication and Data

Favorites should be associated with the user's account so they remain available after the user closes the app or signs in again.

Each saved favorite should reference the original affirmation rather than creating a duplicate copy.

### Suggested Data Relationship

```text
User
└── Favorites
    ├── Affirmation ID
    ├── Affirmation ID
    └── Affirmation ID
```

Each favorite record may include:

* User ID
* Affirmation ID
* Date saved
* Affirmation type

---

## Error Handling

If an affirmation cannot be saved because of a network or system error:

* Return the heart to its previous state.
* Inform the user that the affirmation could not be saved.
* Allow the user to try again.

Example message:

> We couldn't save this affirmation. Please try again.

---

## Accessibility

* The heart button should have a descriptive accessibility label.
* The label should change based on the current state:

  * **Save affirmation**
  * **Remove affirmation from Favorites**
* Saved and unsaved states should not rely only on color.
* The heart control should have an accessible touch target.

---

## Future Enhancements

The initial Favorites feature should remain simple.

Possible future additions include:

* Play all favorite affirmations as a session
* Shuffle favorite affirmations
* Listen to favorites using audio
* Create custom affirmation collections
* Set a favorite affirmation as a daily reminder
* Share saved affirmations
* Filter favorites by category
* Search within saved affirmations
