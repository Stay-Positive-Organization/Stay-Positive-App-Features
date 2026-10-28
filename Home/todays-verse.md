# Today's Verse — Home content and rotation

## Purpose
Home must show a Bible verse before the user checks in. Developers for Android and iOS should use this document as the shared source for the verse catalog and selection behavior.

## Content handoff status
**Behavior documented; verse catalogs awaiting Eve's lists.** The full default catalog and mood-specific catalog have not yet been supplied for this update. Do not treat the seven first-time onboarding verses as the approved Home rotation or invent missing entries. Add the supplied references and approved NIV wording here before seeding the production catalog.

## Default verses
- Maintain a curated default list, independent of mood, for Today's Verse.
- Show a verse immediately on Home before today's check-in, including first launch and the next local day.
- Retain the existing morning/evening rotation. Select from a shuffled cycle of approved default entries, without repeating an entry until the available pool is exhausted; avoid an immediate repeat across cycle boundaries when possible.
- Keep the selection stable within its local date/time slot across recomposition, navigation and app relaunch. Do not reshuffle on each render.
- Morning/evening cutoff times must be defined in shared configuration before implementation; use the user's local timezone consistently on both platforms.
- Bundle or cache approved default verses so Home can display content offline.

### Default catalog
Pending Eve's list. Each entry needs a stable ID, NIV reference, approved verse text, book, chapter, starting verse and ending verse (if a passage). Optional morning/evening tags may be added when supplied.

## Mood-specific verses
Maintain separate lists for ANXIOUS, DISCOURAGED, OVERWHELMED, OKAY, PEACEFUL, GRATEFUL and UNKNOWN ("I don't know").
- After today's check-in, a mood-aware verse selection uses the approved list for that mood.
- Shuffle within that mood's pool and avoid repeats until its pool is exhausted. If only one entry exists, reuse it.
- Keep a selected mood verse stable for the same local day and mood across reopening.
- A changed mood can select from the new mood's pool. Tapping the already selected mood does not reshuffle.
- Missing/empty mood list, offline lookup failure or unavailable content falls back to the cached default verse. Never show an empty card.
- Do not infer mood from journal, prayer or chat text.

### Mood catalog
| Mood | Approved Home verses |
|---|---|
| Anxious | Awaiting supplied list |
| Discouraged | Awaiting supplied list |
| Overwhelmed | Awaiting supplied list |
| Okay | Awaiting supplied list |
| Peaceful | Awaiting supplied list |
| Grateful | Awaiting supplied list |
| I don't know | Awaiting supplied list |

Onboarding uses Happy/Sad in places. Resolve any supplied labels explicitly; do not silently map Happy to Grateful or Sad to Discouraged.

## Plan and consent integration
Preserve existing Home eligibility:
- Free: Today's Verse before and after check-in.
- Premium without personalization consent: default Today's Verse before and after check-in.
- Premium with consent: default Today's Verse before check-in; the existing "For your heart today" activity card after check-in.

Mood-based verse selection must respect the existing Premium personalization consent requirement. This document does not add Bible verses as a sixth HeartPick type or replace the existing activity card. For the current layout, a mood-specific verse may be used when a consented, checked-in Premium user falls back to Today's Verse; otherwise use the default list. Broader Free mood-personalization or displaying an additional verse beside the activity card requires an explicit product decision before implementation.

## Display and navigation
- Show the verse text, Scripture reference and NIV translation label.
- Preserve the existing forest card design and "Read full chapter" action.
- Open the existing Bible reader at the correct chapter and highlight/scroll to the displayed passage.
- Opening the verse continues to count as DAILY_VERSE streak activity; merely displaying it does not.
- No AI-generated or paraphrased Scripture text.

## Acceptance criteria
- [ ] Approved default and mood catalogs are populated from Eve's supplied lists, with complete reader navigation fields.
- [ ] Home shows an approved default verse before check-in without requiring a mood.
- [ ] Rotation shuffles eligible content without changing on every visit or render.
- [ ] Check-in, consent and subscription state follow the eligibility rules above.
- [ ] Mood-aware selection uses only the matching approved pool and respects consent.
- [ ] Empty pools and offline failures show cached default content.
- [ ] New local days, slot changes, mood changes, relaunch and repeat prevention are verified.
- [ ] Android and iOS use the same catalog and documented selection rules.

Related: [Daily Content Module](Daily%20Content%20Module.md), [Android scheduling #419](https://github.com/Stay-Positive-Organization/Stay-Positive-Kotlin-App/issues/419), [iOS scheduling #58](https://github.com/Stay-Positive-Organization/StayPositive-IOS/issues/58).
