# Collections

**Last Updated:** September 11, 2026
**Status:** Existing / Improvements Planned
**Feature Area:** Meditation

## Overview

The Meditation Main Page is the primary entry point for meditation within Stay Positive.

It allows users to discover guided meditations organized into collections based on common needs and goals, such as relieving stress, improving focus, sleeping better, and learning how to meditate.

The page should make meditation content easy to discover without overwhelming users with a large library of individual sessions.

---

## Goal

Give users a simple and organized way to find a meditation that matches what they need.

Users should be able to quickly:

* Understand the available meditation collections.
* Browse individual meditations.
* Identify what each meditation is designed to support.
* Select a meditation and begin a session.
* Discover additional Meditation features available to them.

---

## Page Header

The page header should display:

**Meditation**

The standard Stay Positive navigation controls should remain accessible from the page.

---

## Meditation Collections

Meditations should be organized into collections based on their purpose.

Each collection should include:

* Collection name
* Meditation cards belonging to that collection

The collection name should clearly communicate what the meditations are intended to help with.

---

## Relieve Stress

The **Relieve Stress** collection contains meditations designed to help users slow down, relax, and manage everyday stress.

Current meditations include:

* Relaxation
* Relaxation II
* Work Stress

Example:

### Relieve Stress

**Relaxation**
**Relaxation II**
**Work Stress**

---

## Find Focus

The **Find Focus** collection contains meditations designed to support concentration, communication, and productivity.

Current meditations include:

* Communication
* Focus
* Productivity

Example:

### Find Focus

**Communication**
**Focus**
**Productivity**

---

## Sleep Well

The **Sleep Well** collection contains meditation and relaxation experiences intended to help users wind down and prepare for sleep.

Current meditation:

* Rain Fall

Additional sleep-focused meditations can be added to this collection over time.

---

## Learn to Meditate

The **Learn to Meditate** collection provides beginner-friendly meditation sessions designed to introduce meditation progressively.

Current meditations include:

* Foundations
* Foundations II
* Foundations III
* Foundations IV

Users should be able to follow these meditations as a sequence, but they should not be required to complete one meditation before accessing another unless progression is intentionally introduced later.

---

## Meditation Cards

Each meditation should appear as an interactive card within its collection.

Each card should display:

* Meditation icon or artwork
* Meditation title
* Duration, when available
* Premium indicator, if applicable

Example:

> **Relaxation**
> 5 min

The entire card should be tappable.

Selecting a meditation should open the appropriate meditation player or meditation details experience.

---

## Meditation Naming

Meditation names should help users understand what they are about before starting them.

Names such as **Relaxation**, **Focus**, and **Work Stress** already communicate their purpose clearly.

Numbered meditation series may include an additional descriptive title.

For example:

> **Foundations II**
> Breath Awareness

Instead of displaying only:

> Foundations II

This allows the meditation to remain part of a series while giving users more information about the session.

---

## Collection Layout

Collections should be visually separated so users can easily understand where one group ends and another begins.

Each collection should include:

1. A collection label.
2. A collection title.
3. Its meditation cards.

Example:

**COLLECTION**

### Relieve Stress

`[Relaxation] [Relaxation II] [Work Stress]`

The layout should remain consistent across collections.

---

## Selecting a Meditation

When a user taps a meditation card:

1. The selected meditation is identified.
2. The appropriate meditation experience opens.
3. The user can view or begin the meditation.
4. Playback and progress are handled by the **Meditation Player** feature.

The Main Page should not be responsible for implementing playback behavior.

---

## Premium Content

If certain meditations require Premium, the meditation card should clearly communicate this before the user selects it.

Premium status should not prevent users from understanding what the meditation offers.

A Premium meditation may display:

**PREMIUM**

or:

🔒 **Premium**

If a free user selects Premium content, the app should display the appropriate Premium access experience.

---

## Loading State

While meditation content is loading, the page should display a loading state rather than appearing empty.

The loading state should preserve the approximate structure of the Meditation page where possible.

---

## Empty Collection

If a collection exists but temporarily contains no available meditations, the app should avoid displaying an empty collection unless there is useful information to communicate.

The collection can either:

* Be hidden until content becomes available, or
* Display an intentional coming-soon state.

Example:

> More Sleep Well meditations are coming soon.

---

## Error Handling

If meditation content cannot be loaded:

> We couldn't load your meditations. Please try again.

**Try Again**

Previously available content may remain visible if it can safely be loaded from local or cached data.

---

## Functional Requirements

* Users can access the Meditation Main Page.
* Meditation content is organized into collections.
* Each collection has a clear title.
* Each meditation belongs to the appropriate collection.
* Meditation cards display the meditation title.
* Meditation cards can display duration.
* Meditation cards can display Premium status.
* The entire meditation card is tappable.
* Selecting a meditation opens the appropriate meditation experience.
* Premium content is visually distinguishable.
* Empty collections are handled appropriately.
* Loading states are displayed while content is being retrieved.
* Errors do not leave the page in an unusable state.

---

## Accessibility

* Every meditation card should have a descriptive accessibility label.
* Collection headings should be identifiable as headings by assistive technologies.
* Interactive cards should have accessible touch targets.
* Premium content should not be identified through color alone.
* Text should maintain sufficient contrast against the background.
* Meditation icons should not be required to understand the purpose of a meditation.
* Screen readers should announce the meditation title, duration, and Premium status when applicable.

Example accessibility label:

> Relaxation meditation, 5 minutes. Double tap to open.

For Premium content:

> Relaxation meditation, 5 minutes, Premium. Double tap to open.

---

## Future Enhancements

Possible future improvements to the Meditation Main Page include:

* Horizontal scrolling collections
* Additional meditation collections
* Search
* Filtering by duration
* Filtering by meditation goal
* Personalized collection ordering
* Recommended meditations
* Recently played meditations
* Continue Listening
* Favorites
* Meditation history
* Dynamic collections based on time of day
