# Start Affirmation Session

**Last Updated:** September 2, 2026
**Status:** Planned
**Feature Area:** Affirmations

## Overview

The Start Affirmation Session feature guides users through a short sequence of affirmations displayed one at a time.

Instead of only browsing or reading affirmations from a list, users can intentionally pause, focus, and repeat each affirmation before moving to the next one.

---

## Goal

Turn affirmations into a simple, focused wellness practice that users can complete whenever they need encouragement, calm, confidence, or spiritual grounding.

---

## Feature Name

The primary call-to-action should be labeled:

**Start a Session**

The feature may be called **Affirmation Session** elsewhere in the interface and technical documentation.

---

## Placement

The **Start a Session** button should appear on the Affirmations home page.

Recommended placement:

1. Today's Affirmation
2. Start a Session
3. Explore Categories
4. Scripture Affirmations
5. Your Space
6. My Affirmations

The option may also appear on individual category pages.

---

## Initial Session Experience

The initial version should provide a short, text-based session containing five affirmations.

Each affirmation should appear individually on the screen so the user can focus on it without additional distractions.

The initial session should include:

* Five affirmations
* One affirmation displayed at a time
* Previous and Next controls
* Progress indicator
* Favorite button
* Exit option
* Completion screen

Audio playback and automatic timing can be added in a future version.

---

## User Flow

### Starting a Session

1. The user taps **Start a Session**.
2. The app opens the session setup screen.
3. The user chooses an affirmation source or category.
4. The user taps **Begin Session**.
5. The session displays the first affirmation.
6. The user reads or repeats the affirmation.
7. The user taps **Next** to continue.
8. After the final affirmation, the completion screen appears.

---

## Session Setup

Before beginning, users should be able to choose what type of affirmations they want to practice.

### Select a Focus

Available options may include:

* All Affirmations
* Self-Esteem
* Health & Well-Being
* Success
* Relationships
* Scripture Affirmations
* Favorites

**All Affirmations** should be selected by default.

The initial version should use a fixed session length of five affirmations to keep the setup simple.

### Setup Screen Example

**Choose your focus**

> Select the affirmations you need today.

* All Affirmations
* Self-Esteem
* Health & Well-Being
* Success
* Relationships
* Scripture Affirmations
* Favorites

**Begin Session**

---

## Favorites Requirement

The Favorites option should only be available when the user has saved at least five affirmations.

If the user has fewer than five Favorites, the option may:

* Use all available Favorites without duplicates, or
* Be disabled until the user has saved five affirmations.

Recommended behavior:

Use all available Favorites if the user has saved at least one. Clearly display the number of affirmations that will be included.

Example:

> Favorites · 3 affirmations

If the user has no Favorites, display:

> Save affirmations you love, and you can practice them together here.

**Explore Affirmations →**

---

## Session Screen

Each session screen should display:

* Exit button
* Session progress
* Affirmation text
* Favorite button
* Previous button
* Next button

Example:

**× Exit**
**2 of 5**

> “I trust myself to make decisions that support my growth.”

♡ Save

**Previous**  **Next**

The final affirmation should display **Finish** instead of **Next**.

---

## Progress Indicator

The session should clearly show the user's progress.

Example:

**2 of 5**

A visual progress bar may also be used.

The progress indicator should update immediately when the user moves forward or backward.

---

## Session Navigation

Users should be able to:

* Tap **Next** to move to the following affirmation.
* Tap **Previous** to return to the preceding affirmation.
* Tap **Finish** after reaching the final affirmation.
* Tap the exit button to leave before completing the session.

The Previous button should be disabled or hidden on the first affirmation.

---

## Saving an Affirmation

Users can tap the heart icon during a session to save an affirmation to Favorites.

**Default state:**
♡ Not saved

**Saved state:**
♥ Saved

When saved:

* The affirmation is added to Favorites.
* The heart changes to its active state.
* The saved state persists across sessions.
* The saved state updates everywhere the affirmation appears.

If the user is not signed in, tapping the heart should prompt them to sign in or create an account.

---

## Exiting a Session

If the user attempts to leave before completing the session, the app should display a confirmation message.

### Exit session?

> Your current session will end if you leave.

**Continue Session**
**Exit Session**

The confirmation should prevent users from accidentally losing their progress.

The initial version does not need to save incomplete session progress.

---

## Completion Screen

After the final affirmation, the user should see a calm and encouraging completion screen.

### Session Complete

> You took a moment to speak encouragement, truth, and kindness over yourself.

**Done**

Optional secondary action:

**Start Another Session**

The completion screen may also display:

* Number of affirmations completed
* Session focus
* Short encouraging message

Example:

> You completed 5 affirmations for Self-Esteem.

---

## Affirmation Selection

The session should select affirmations based on the user's chosen focus.

The selection process should:

* Use active and approved affirmations.
* Match the selected category or source.
* Avoid duplicate affirmations within the same session.
* Randomize the order when appropriate.
* Return the correct number of affirmations.
* Avoid immediately repeating the user's most recent session when possible.

If a category contains fewer than five affirmations, the session should use all available affirmations without duplicates.

---

## Session History

The initial version only needs to record completed sessions.

A completed session record may include:

* User ID, when authenticated
* Completion date and time
* Selected focus
* Number of affirmations completed
* Session completion status

The complete text of each affirmation does not need to be duplicated in the session record.

---

## Authentication

Users should be able to begin and complete a standard affirmation session without signing in.

Authentication is required for:

* Starting a session using Favorites
* Saving affirmations to Favorites
* Synchronizing session history across devices

If session history is stored only on the device in the initial version, authentication is not required to record completion locally.

---

## Loading State

While the affirmations are being prepared, the app should display a loading state.

Example:

**Preparing your session…**

The loading experience should feel calm and should not display an empty or broken session screen.

---

## Error Handling

If the session cannot be loaded:

* Keep the user on the setup screen.
* Explain that the session could not be prepared.
* Allow the user to try again.
* Do not begin an incomplete session.

Example:

> We couldn't prepare your affirmation session. Please try again.

**Try Again**

If the connection is lost after a session begins, the user should still be able to complete affirmations that have already been loaded.

---

## Offline Behavior

If the user is offline:

* Use locally cached affirmations when available.
* Allow the user to complete the session normally.
* Save completion data locally until it can be synchronized.
* Hide or disable sources that are not available offline.

If no affirmations are available offline, display:

> Connect to the internet to prepare your affirmation session.

---

## Functional Requirements

* Users can start an affirmation session from the Affirmations home page.
* Users can select a category or affirmation source.
* All Affirmations is selected by default.
* The initial session contains five affirmations when enough content is available.
* Affirmations appear one at a time.
* Users can move forward and backward within the session.
* The session displays the user's progress.
* Duplicate affirmations do not appear within the same session.
* Users can save and remove affirmations from Favorites.
* Users can exit the session.
* Early exits require confirmation.
* A completion screen appears after the final affirmation.
* Completed sessions may be recorded.
* Loaded sessions remain usable during a temporary network interruption.

---

## Suggested Data Structure

```text
Affirmation Session
├── Session ID
├── User ID, if available
├── Selected focus
├── Affirmation IDs
├── Current position
├── Number completed
├── Completion status
├── Started timestamp
└── Completed timestamp
```

The session should reference existing affirmation records rather than duplicate their content.

Example relationship:

```text
Affirmation Session
└── Affirmation IDs
    ├── Affirmation ID
    ├── Affirmation ID
    ├── Affirmation ID
    ├── Affirmation ID
    └── Affirmation ID
```

---

## Accessibility

* Affirmation text should support screen readers.
* The progress indicator should announce the current position.
* Navigation controls should have descriptive labels.
* The heart button should announce:

  * **Save affirmation**
  * **Remove affirmation from Favorites**
* The session should support larger text sizes.
* Controls should have accessible touch targets.
* Progress should not be communicated through color alone.
* Animations should respect reduced-motion settings.

---

## Analytics

The following events may be tracked:

* Session setup opened
* Session focus selected
* Session started
* Affirmation viewed
* Affirmation saved
* Session exited early
* Session completed
* Another session started

Analytics should not collect private custom affirmation text.

---

## Acceptance Criteria

The feature is complete when:

* The user can open the session setup screen.
* The user can select an affirmation focus.
* The user can begin a five-affirmation session.
* One affirmation appears at a time.
* The user can navigate forward and backward.
* The session shows accurate progress.
* No affirmation is repeated within the same session.
* The user can save affirmations to Favorites.
* The user receives a confirmation before exiting early.
* The completion screen appears after the final affirmation.
* The session remains usable if the connection is temporarily interrupted.

---

## Future Enhancements

Possible future additions include:

* Audio narration
* Background music
* Automatic affirmation progression
* Adjustable session length
* Timed breathing between affirmations
* Repeat-after-me mode
* Personalized affirmation recommendations
* Custom sessions built from Favorites
* Sessions using custom affirmations
* Morning and evening sessions
* Daily session reminders
* Session streaks
* Practice history
* Reflection prompt after completion
* Voice recording for custom affirmations
