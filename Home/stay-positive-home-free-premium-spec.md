# Home Screen --- Free vs. Premium Personalization

## Purpose

This document defines the Home screen behavior for **Free** and
**Premium** users.

> **Free collects signals. Premium uses eligible signals for
> personalized recommendations.**

Both plans should feel useful and complete. Premium should differ
primarily through adaptive content, not by making the Free Home screen
look disabled.

## 1. Shared Home Screen

Both Free and Premium users see:

1.  Welcome/header
2.  Daily mood check-in
3.  Daily content area
4.  Explore More
5.  Bottom navigation

### Daily Mood Check-In

Prompt: **How is your heart today?**

Supporting copy: *Take a moment to check in with God and yourself.*

Options:

-   Anxious
-   Discouraged
-   Overwhelmed
-   Okay
-   Peaceful
-   Grateful
-   I don't know

The first six appear in a 3 × 2 grid. **I don't know** appears as a
full-width neutral option because it represents uncertainty rather than
a specific mood.

When a mood is selected:

1.  Show the selected state immediately.
2.  Save the check-in with a timestamp.
3.  Restore the same-day selection when appropriate.
4.  Make the signal available to personalization only when the user is
    eligible and any required privacy/consent conditions are satisfied.

The check-in itself is **not** a Premium feature.

------------------------------------------------------------------------

## 2. Free Experience

### Goal

Provide immediate value while collecting structured signals that can
help understand product usage.

The Free Home screen does **not** generate or rank Home recommendations
using AI/ML.

### After check-in

If a Free user selects `Anxious`, the UI may show that `Anxious` is
selected and persist the event. It should **not** immediately present an
AI-generated recommendation because of that selection.

### Daily content

Free users see general content, for example:

**Today's Verse**

> "Be still, and know that I am God."\
> Psalm 46:10

CTA: **Read Full Chapter**

This content can be editorially scheduled, rotated, or selected by
another deterministic/non-personalized mechanism. Do not describe it as
being selected because of the user's mood or behavior.

### Free Home structure

``` text
WELCOME BACK
Hello, Eve
Thursday, April 16

[ Mood Check-In ]
Anxious | Discouraged | Overwhelmed
Okay    | Peaceful    | Grateful
[ I don't know ]

TODAY'S VERSE
[ General daily content ]
[ Read Full Chapter ]

EXPLORE MORE
Guided Meditations | Affirmations
Journaling         | Prayer
Talk with Alex     | Virtual Library
```

------------------------------------------------------------------------

## 3. Premium Experience

### Goal

Use eligible user signals to make Stay Positive increasingly relevant to
the individual.

Premium uses the same mood check-in and overall Home structure as Free.
The primary Home difference is the **Personalized Reset** module.

### Personalized Reset

Instead of the generic `Today's Verse` module, Premium may show:

**Your Personalized Reset**

Supporting copy: *Based on how you've been feeling lately.*

The module can recommend existing content such as:

-   Meditation
-   Prayer
-   Affirmation
-   Journaling prompt
-   Scripture/reflection
-   Other supported wellness content

Example:

``` text
YOUR PERSONALIZED RESET

A Moment of Peace for You
5-minute meditation
Personalized for you

[ Start Now ]
```

### Potential recommendation signals

Subject to the final implementation and privacy requirements,
personalization may use eligible signals such as:

-   Mood check-in history
-   Content opened
-   Content completed
-   Feature usage
-   Repeated preferences
-   Explicit preferences supplied by the user
-   Appropriate contextual patterns

The recommendation implementation may evolve from rules-based
personalization to ML without requiring a major Home UI redesign.

------------------------------------------------------------------------

## 4. Free vs. Premium Summary

  -----------------------------------------------------------------------
  Capability              Free                    Premium
  ----------------------- ----------------------- -----------------------
  Mood check-in           Yes                     Yes

  Store mood history      Yes                     Yes

  Shared Home structure   Yes                     Yes

  Explore More            Yes                     Yes

  General daily content   Yes                     Fallback

  AI/ML Home              **No**                  **Yes**
  recommendation                                  

  Behavioral              Signals may be          Used when permitted
  personalization         collected when          
                          permitted, but are not  
                          used for Free Home      
                          recommendations         

  Personalized Reset      No                      Yes
  -----------------------------------------------------------------------

> This specification does not redefine existing entitlement/paywall
> rules for individual Explore More features. Existing product rules
> remain authoritative unless changed separately.

------------------------------------------------------------------------

## 5. UX Logic

### Free

``` text
Mood Check-In
      ↓
Persist signal
      ↓
Today's Verse
(morning/night scheduled rotation)
```

### Premium

``` text
Mood Check-In
      ↓
Persist signal
      ↓
Combine eligible history/preferences/behavior
      ↓
Personalization layer
      ↓
Personalized Reset
```

**Free = Check in + general experience**

**Premium = Check in + adaptive/personalized experience**

------------------------------------------------------------------------

## 6. Suggested Data Model

Example only; adapt to the existing backend.

``` json
{
  "userId": "USER_ID",
  "mood": "ANXIOUS",
  "checkedInAt": "2026-09-25T08:15:00Z",
  "source": "HOME"
}
```

Suggested stable enum:

``` text
ANXIOUS
DISCOURAGED
OVERWHELMED
OKAY
PEACEFUL
GRATEFUL
UNKNOWN
```

Use `UNKNOWN` as the canonical value for **I don't know** and localize
the UI label separately.

------------------------------------------------------------------------

## 7. Home State Logic

``` text
Load Home
    |
    +-- Load today's mood check-in
    |
    +-- Render Mood Check-In
    |
    +-- Is Premium personalization enabled/eligible?
            |
            +-- NO
            |    +-- Render Today's Verse for the current morning/night rotation
            |
            +-- YES
                 +-- Request personalized recommendation
                        |
                        +-- Available
                        |    +-- Render Personalized Reset
                        |
                        +-- Missing/error
                             +-- Render Today's Verse for the current morning/night rotation
```

A recommendation failure must never leave an empty Home section.

------------------------------------------------------------------------

## 8. Recommended Component Structure

``` text
HomeScreen
├── WelcomeHeader
├── MoodCheckInCard
│   ├── MoodOption × 6
│   └── UnknownMoodOption
├── HomeContentModule
│   ├── DailyContentCard
│   └── PersonalizedResetCard
├── ExploreMoreSection
│   ├── GuidedMeditationsCard
│   ├── AffirmationsCard
│   ├── JournalingCard
│   ├── PrayerCard
│   ├── TalkWithAlexCard
│   └── VirtualLibraryCard
└── BottomNavigation
```

Prefer **one Home implementation with conditional content** rather than
separate Free and Premium Home screens.

------------------------------------------------------------------------

## 9. Analytics

Recommended events:

``` text
home_viewed
mood_checkin_viewed
mood_selected
mood_changed
daily_content_viewed
daily_content_opened
personalized_reset_viewed
personalized_reset_opened
explore_feature_opened
```

Example mood event properties:

``` json
{
  "mood": "ANXIOUS",
  "isPremium": false,
  "source": "HOME"
}
```

Example recommendation properties:

``` json
{
  "recommendationId": "RECOMMENDATION_ID",
  "contentType": "MEDITATION",
  "placement": "HOME_PERSONALIZED_RESET"
}
```

Do not include sensitive free-text journal or prayer content in
analytics properties.

------------------------------------------------------------------------

## 10. Loading, Empty, and Error States

### Mood submission failure

-   Do not silently represent an unsaved selection as persisted.
-   Preserve the selection locally when appropriate.
-   Provide a lightweight retry mechanism.

### Premium recommendation loading

Show a skeleton/loading state in the Personalized Reset area.

### Recommendation unavailable

Fall back to **Today's Verse** using the current morning/night scheduled rotation.

### New Premium user

A new Premium user may not have enough history for meaningful
personalization. Show general content or an explicitly non-personalized
starter recommendation until sufficient signals exist. Do not claim
content is based on behavior when it is not.

------------------------------------------------------------------------

## 11. Privacy and Safety Requirements

Mood check-ins may represent sensitive wellbeing information.

-   Collect only data required for defined product purposes.
-   Follow applicable privacy and consent requirements.
-   Avoid exposing mood history in unnecessary logs.
-   Do not send journal or prayer free text to analytics.
-   Clearly distinguish personalized recommendations from general
    content.
-   Do not imply a clinical diagnosis or treatment from mood selections.
-   Treat `I don't know` as a valid check-in, not an error.

------------------------------------------------------------------------

## 12. Acceptance Criteria

### Free

-   [ ] User can select all seven check-in options.
-   [ ] Selected mood is visually identifiable.
-   [ ] Check-in can be persisted.
-   [ ] Home displays general/non-personalized daily content.
-   [ ] No AI/ML recommendation is presented as a result of the
    check-in.
-   [ ] Explore More follows existing feature entitlements.

### Premium

-   [ ] User receives the same mood check-in UI.
-   [ ] Check-in can be persisted.
-   [ ] Home can request a personalized recommendation.
-   [ ] Personalized Reset identifies the recommended content.
-   [ ] Recommendation CTA opens the correct content.
-   [ ] General content is used when personalization is unavailable.
-   [ ] Explore More follows existing feature entitlements.

### Both

-   [ ] `I don't know` is accepted as a valid state.
-   [ ] UI remains usable during network operations.
-   [ ] Analytics distinguish general content from personalized
    recommendations.
-   [ ] Sensitive free-text content is excluded from analytics.

------------------------------------------------------------------------

## 13. Final Implementation Rule

**Do not build two unrelated Home screens.**

Build **one shared Home experience** with a conditional content module:

-   **Free:** `DailyContentCard`
-   **Premium + recommendation available:** `PersonalizedResetCard`
-   **Premium + recommendation unavailable:** `DailyContentCard`
    fallback

This keeps the UX consistent, reduces duplicated implementation, and
makes the Premium value proposition clear: **Stay Positive adapts to the
individual rather than simply presenting a different-looking Home
screen.**
