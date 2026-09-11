# Meditation Home

**Last Updated:** September 11, 2026
**Status:** Planned Redesign
**Feature Area:** Meditation

## Overview

The **Meditation Home** screen is the main entry point to the Meditation experience in Stay Positive.

The redesigned screen helps users quickly find a meditation based on what they need in the moment while providing access to Stay Positive's meditation collections, Scripture-based meditations, personalized recommendations, and personal meditation content.

Rather than functioning only as a library of meditation tracks, Meditation Home should prioritize **intent, personalization, continuation, faith integration, and discovery**.

---

## Goal

Help users answer:

> What do I need right now?

and quickly find a meditation that supports that need.

The screen should make it easy to:

* Find meditation based on a current need.
* Continue an unfinished meditation.
* Discover personalized recommendations.
* Meditate on Scripture.
* Browse meditation collections.
* Discover featured meditation experiences.
* Access saved and personal meditations.

---

# Screen Structure

The recommended Meditation Home hierarchy is:

```text
Meditation
│
├── What Do You Need Right Now?
│
├── Continue Listening
│
├── Recommended for You
│
├── Meditate with Scripture
│   ├── Psalms
│   ├── Peace
│   ├── Trusting God
│   ├── Rest
│   ├── Gratitude
│   └── God's Promises
│
├── Meditation Collections
│   ├── Relieve Stress
│   ├── Find Focus
│   ├── Sleep Well
│   └── Learn to Meditate
│
├── Featured Meditation
│
└── Your Space
    ├── Favorites
    └── My Meditations
```

Personalized sections that do not have relevant content, such as **Continue Listening**, should be hidden rather than displayed empty.

---

# Header

The screen should retain the standard Stay Positive header and navigation.

### Title

**Meditation**

The title should remain the primary page heading.

---

# What Do You Need Right Now?

This section helps users discover meditation based on their immediate needs rather than requiring them to know which collection to browse.

### Heading

**What do you need right now?**

Initial options may include:

* 🌿 Relax
* 🧘 Stress Relief
* 🎯 Focus
* 🌙 Sleep
* 🕊️ Peace
* ⚡ Energy

The options should use compact chips, pills, icons, or small cards to avoid taking excessive vertical space.

---

## Selecting a Need

When the user selects an option, Stay Positive should surface relevant meditation experiences.

Recommendations can include both traditional meditation and faith-based content when appropriate.

Example:

### I need peace

Stay Positive may recommend:

> 🧘 **Relaxation**
> 5 min
>
> 📖 **Psalm 46 — Be Still**
> Scripture Meditation · 8 min
>
> 🙏 **Prayer for Peace**
> Guided Prayer · 5 min

This allows Stay Positive to recommend the practice most relevant to the user's need rather than limiting recommendations to one type of content.

The user should be able to change their selection easily.

---

# Continue Listening

If the user has an unfinished meditation, a **Continue Listening** section should appear near the top of the screen.

### Example

**Continue Listening**

> **Relaxation**
> 8 min remaining
> ━━━━━━━○━━━━
> ▶ Continue

The card may display:

* Meditation artwork
* Meditation title
* Playback progress
* Remaining duration
* Continue/play button

Selecting the card should resume the meditation from the user's previous position.

---

## Visibility

If the user does not have an unfinished meditation, the section should not appear.

---

# Recommended for You

The **Recommended for You** section provides a small selection of meditation experiences relevant to the user.

Recommendations may initially use simple signals such as:

* Current selected need
* Recently played meditations
* Favorite meditation categories
* Saved meditations
* Time of day
* Previously completed meditations

Advanced AI personalization is not required for the initial implementation.

---

## Recommendation Layout

Approximately 2–3 recommendations should be visible at a time.

Example:

```text
Recommended for You                    See All →

[ Relaxation ]  [ Psalm 23 ]  [ Morning Peace ]
    5 min           8 min          10 min
```

Recommendations may include both standard and Scripture-based meditation.

---

# Meditate with Scripture

**Meditate with Scripture** is a faith-based meditation collection centered on slowing down, reflecting on God's Word, and using Scripture as the foundation for meditation and prayer.

This section helps differentiate Stay Positive's Meditation experience from a traditional meditation library.

### Heading

**Meditate with Scripture**

Supporting text may read:

> Slow down, reflect, and spend time with God's Word.

---

## Scripture Categories

Scripture meditation can be organized around books, passages, and spiritual needs.

Initial categories may include:

* Psalms
* Peace
* Trusting God
* Rest
* Gratitude
* God's Promises

Additional categories can be introduced as the Scripture meditation library grows.

---

# Psalms

**Psalms** should be one of the primary Scripture meditation categories.

Psalms naturally support meditation around themes such as peace, trust, protection, gratitude, worship, and surrender.

Examples:

### Psalm 23 — The Lord Is My Shepherd

**Scripture Meditation · 10 min**

A guided meditation centered on God's presence, guidance, and care.

### Psalm 46 — Be Still

**Scripture Meditation · 8 min**

A guided meditation about becoming still and trusting God during uncertainty.

### Psalm 91 — Rest in His Protection

**Scripture Meditation · 12 min**

A guided meditation centered on God's protection and refuge.

---

# Scripture Meditation Experience

Scripture meditations should be more than audio readings of Bible passages.

A guided Scripture meditation may follow this structure:

```text
Settle
   ↓
Scripture
   ↓
Reflection
   ↓
Silence
   ↓
Prayer
```

### Settle

Help the user become physically and mentally still.

### Scripture

Read or present the selected Bible passage.

### Reflection

Guide the user toward reflecting on the meaning of the passage and how it relates to their current circumstances.

### Silence

Provide intentional quiet time for personal reflection.

### Prayer

Conclude with an optional guided prayer related to the Scripture.

---

# Relationship with Prayer

**Meditate with Scripture** should complement rather than replace the dedicated Prayer feature.

The distinction should remain:

**Prayer**

> A space specifically designed for talking with God, accessing prayers, and engaging in prayer practices.

**Scripture Meditation**

> A guided practice centered on slowing down and reflecting deeply on God's Word.

Meditation Home may recommend a prayer when it is relevant to the user's selected need, but the complete Prayer experience remains within the Prayer feature.

---

# Meditation Collections

Existing meditation collections should remain available below the personalized and Scripture-focused sections.

They provide a browsing experience for users who already know the type of meditation they want.

---

## Relieve Stress

Meditations intended to help users slow down, relax, and manage stress.

Current examples:

* Relaxation
* Relaxation II
* Work Stress

---

## Find Focus

Meditations intended to support concentration, communication, and productivity.

Current examples:

* Communication
* Focus
* Productivity

---

## Sleep Well

Meditation and relaxation experiences designed to help users wind down and prepare for sleep.

Current example:

* Rain Fall

Additional sleep-focused meditations can be introduced over time.

---

## Learn to Meditate

Beginner-friendly meditation sessions designed to introduce meditation progressively.

Current examples:

* Foundations
* Foundations II
* Foundations III
* Foundations IV

Where possible, numbered sessions should also contain descriptive titles.

Example:

> **Foundations II**
> Breath Awareness

---

# Collection Layout

Meditation collections should preferably use **horizontal scrolling** rather than displaying every meditation vertically.

Example:

```text
Relieve Stress                         See All →

┌──────────┐ ┌──────────┐ ┌──────────┐
│          │ │          │ │          │
│ Artwork  │ │ Artwork  │ │ Artwork  │
│          │ │          │ │          │
└──────────┘ └──────────┘ └──────────┘
Relaxation   Work Stress   Relaxation II
5 min        10 min        8 min
```

This reduces the overall length of Meditation Home while allowing the meditation library to grow.

---

# Meditation Cards

Each meditation card should give users enough information to decide whether they want to begin the session.

Cards should display:

* Artwork
* Meditation title
* Duration
* Meditation type, when useful
* Premium status, if applicable

A favorite control may also be included.

Example:

> **Psalm 46 — Be Still** ♡
> Scripture Meditation · 8 min

or:

> **Relaxation** ♡
> Meditation · 5 min

The entire card should be tappable.

---

# Featured Meditation

A larger card can highlight a specific meditation experience.

### Heading

**Featured**

### Example

**Pineal Gland Awakening**

> Activate your third eye through deep visualization and breathwork.

**Guided · 20 min**

▶ **Begin Meditation**

The Featured Meditation should be visually distinct from regular meditation cards.

Only one featured meditation should normally appear at a time.

Featured content may eventually change based on:

* Time of day
* Season
* User interests
* Current needs
* New content

---

# Your Space

Personal meditation features should be grouped together under **Your Space**.

### Heading

**Your Space**

Initial options:

* ♡ Favorites
* ＋ My Meditations

Example:

```text
YOUR SPACE

┌─────────────────────────────────┐
│ ♡  Favorites                 → │
├─────────────────────────────────┤
│ ＋  My Meditations   PREMIUM  → │
└─────────────────────────────────┘
```

---

# Favorites

**Favorites** provides access to meditation experiences the user has saved.

Favorites may eventually contain:

* Standard meditations
* Scripture meditations
* Guided meditations

The detailed saving and removal behavior should be documented separately under **Favorites / Saved Meditations**.

---

# My Meditations

**My Meditations** provides a personal meditation library where users can add supported external meditation content.

If My Meditations requires Premium, its Premium status should be visible without preventing the user from understanding what the feature does.

---

# Premium Presentation

Premium indicators should remain subtle and consistent.

Examples:

**PREMIUM**

or:

🔒 **Premium**

The Meditation Home screen should communicate the value of Premium features without interrupting normal meditation discovery with excessive upgrade prompts.

---

# Conditional Home Screen

Not every section should appear for every user.

The screen should adapt based on available content and user activity.

### New User

```text
Meditation

What do you need right now?
        ↓
Recommended Meditations
        ↓
Meditate with Scripture
        ↓
Meditation Collections
        ↓
Featured Meditation
        ↓
Your Space
```

### Returning User

```text
Meditation

What do you need right now?
        ↓
Continue Listening
        ↓
Recommended for You
        ↓
Meditate with Scripture
        ↓
Meditation Collections
        ↓
Featured Meditation
        ↓
Your Space
```

---

# Recommended UI Hierarchy

```text
┌──────────────────────────────────────┐
│              Meditation              │
├──────────────────────────────────────┤
│                                      │
│ What do you need right now?          │
│ [Relax] [Stress] [Focus] [Sleep] →   │
│                                      │
├──────────────────────────────────────┤
│ Continue Listening                   │
│ ┌──────────────────────────────────┐ │
│ │ Relaxation                  ▶   │ │
│ │ 8 min remaining                 │ │
│ │ ━━━━━━━━━○━━━━━━                 │ │
│ └──────────────────────────────────┘ │
│                                      │
├──────────────────────────────────────┤
│ Recommended for You          See All │
│ [ Card ] [ Card ] [ Card ] →         │
│                                      │
├──────────────────────────────────────┤
│ Meditate with Scripture      See All │
│ [Psalms] [Peace] [Trust God] →       │
│                                      │
├──────────────────────────────────────┤
│ Relieve Stress               See All │
│ [ Card ] [ Card ] [ Card ] →         │
│                                      │
│ Find Focus                   See All │
│ [ Card ] [ Card ] [ Card ] →         │
│                                      │
│ Sleep Well                   See All │
│ [ Card ] [ Card ] [ Card ] →         │
│                                      │
│ Learn to Meditate            See All │
│ [ Card ] [ Card ] [ Card ] →         │
│                                      │
├──────────────────────────────────────┤
│ FEATURED                             │
│ ┌──────────────────────────────────┐ │
│ │ Pineal Gland Awakening           │ │
│ │ Guided · 20 min              ▶  │ │
│ └──────────────────────────────────┘ │
│                                      │
├──────────────────────────────────────┤
│ Your Space                           │
│ ♡ Favorites                       → │
│ ＋ My Meditations       PREMIUM   → │
│                                      │
└──────────────────────────────────────┘
```

---

# UX Principles

The Meditation Home screen should follow these principles:

* **Need before library:** Help users identify what they need before requiring them to browse.
* **Faith integrated, not separated:** Scripture meditation should feel like a natural part of the Meditation experience.
* **Resume before restart:** Returning users should easily continue unfinished sessions.
* **Personal before generic:** Relevant recommendations should appear before the complete meditation catalog.
* **Purpose before title:** Users should understand what a meditation can help them with.
* **Progressive disclosure:** Avoid displaying the entire meditation library simultaneously.
* **Clear duration:** Users should know the expected time commitment before starting.
* **Consistent navigation:** Meditation collections should follow a predictable interaction pattern.
* **Minimal Premium interruption:** Premium indicators should communicate value without disrupting discovery.

---

# Future Enhancements

Future versions of Meditation Home may include:

* Recently Played
* Meditation history
* Daily meditation
* Meditation streaks
* Search
* Filters
* Advanced personalization
* Mood-based recommendations
* Time-of-day recommendations
* Scripture recommendations based on current needs
* Meditation reminders
* Morning and evening routines
* Cross-feature recommendations involving Prayer, Affirmations, Journaling, and the Bible

The Meditation Home screen should remain focused on **helping the user choose what to do next**, even as additional meditation capabilities are introduced.
