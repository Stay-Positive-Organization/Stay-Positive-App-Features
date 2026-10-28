# Today's Verse — Home content and rotation

## Purpose
Home must show a Bible verse before the user checks in. Developers for Android and iOS should use this document as the shared source for the verse catalog and selection behavior.

## Content handoff status
**Initial reference catalogs populated:** 30 default selections and 10 selections for each of the seven Home moods (70 mood assignments). These lists were generated for this feature; they were not supplied by Eve.

**Translation:** NIV. The tables provide passage references and reader navigation fields, not Scripture transcriptions. Resolve exact NIV text from the app's authorized Bible content source and validate each passage before publishing. Do not substitute KJV, paraphrases or generated wording. Bundle/cache retrieved text as permitted by that source so the default card works offline.

When a selection spans multiple verses, show the complete passage with its full reference and allow the card to grow; do not truncate Scripture to fit a fixed-height card. Seed records need `id`, `translation: NIV`, `reference`, `book`, `chapter`, `startVerse`, `endVerse`, `text` and slot/mood pool membership. Table row IDs identify pool entries; deduplicate actual passages by translation/book/chapter/start/end. Default offline fallback: Psalm 46:1, with NIV text retrieved and bundled before release.

## Default verses
- Maintain a curated default list, independent of mood, for Today's Verse.
- Show a verse immediately on Home before today's check-in, including first launch and the next local day.
- Retain the existing morning/evening rotation. Select from a shuffled cycle of approved default entries, without repeating an entry until the available pool is exhausted; avoid an immediate repeat across cycle boundaries when possible.
- Keep the selection stable within its local date/time slot across recomposition, navigation and app relaunch. Do not reshuffle on each render.
- Morning/evening cutoff times must be defined in shared configuration before implementation; use the user's local timezone consistently on both platforms.
- Bundle or cache approved default verses so Home can display content offline.

### Default catalog

30 selections: 15 for morning and 15 for evening. These are content pools, not a fixed day-by-day schedule; shuffle within the current slot's pool. At two slots per day, this supports 15 days before a slot pool repeats.

| ID | Slot | NIV reference | Book | Chapter | Start verse | End verse |
|---|---|---|---|---|---|---|
| DEFAULT_01 | MORNING | Psalm 118:24 | Psalm | 118 | 24 | 24 |
| DEFAULT_02 | MORNING | Lamentations 3:22–23 | Lamentations | 3 | 22 | 23 |
| DEFAULT_03 | MORNING | Psalm 143:8 | Psalm | 143 | 8 | 8 |
| DEFAULT_04 | MORNING | Proverbs 3:5–6 | Proverbs | 3 | 5 | 6 |
| DEFAULT_05 | MORNING | Isaiah 40:31 | Isaiah | 40 | 31 | 31 |
| DEFAULT_06 | MORNING | Joshua 1:9 | Joshua | 1 | 9 | 9 |
| DEFAULT_07 | MORNING | Psalm 90:14 | Psalm | 90 | 14 | 14 |
| DEFAULT_08 | MORNING | Colossians 3:17 | Colossians | 3 | 17 | 17 |
| DEFAULT_09 | MORNING | Psalm 37:5 | Psalm | 37 | 5 | 5 |
| DEFAULT_10 | MORNING | James 1:5 | James | 1 | 5 | 5 |
| DEFAULT_11 | MORNING | Micah 6:8 | Micah | 6 | 8 | 8 |
| DEFAULT_12 | MORNING | Ephesians 2:10 | Ephesians | 2 | 10 | 10 |
| DEFAULT_13 | MORNING | Romans 15:13 | Romans | 15 | 13 | 13 |
| DEFAULT_14 | MORNING | Psalm 19:14 | Psalm | 19 | 14 | 14 |
| DEFAULT_15 | MORNING | Matthew 5:16 | Matthew | 5 | 16 | 16 |
| DEFAULT_16 | EVENING | Psalm 4:8 | Psalm | 4 | 8 | 8 |
| DEFAULT_17 | EVENING | Matthew 11:28–30 | Matthew | 11 | 28 | 30 |
| DEFAULT_18 | EVENING | Psalm 23:1–3 | Psalm | 23 | 1 | 3 |
| DEFAULT_19 | EVENING | John 14:27 | John | 14 | 27 | 27 |
| DEFAULT_20 | EVENING | Psalm 121:7–8 | Psalm | 121 | 7 | 8 |
| DEFAULT_21 | EVENING | 1 Peter 5:7 | 1 Peter | 5 | 7 | 7 |
| DEFAULT_22 | EVENING | Psalm 46:10 | Psalm | 46 | 10 | 10 |
| DEFAULT_23 | EVENING | Isaiah 26:3 | Isaiah | 26 | 3 | 3 |
| DEFAULT_24 | EVENING | Psalm 62:5–6 | Psalm | 62 | 5 | 6 |
| DEFAULT_25 | EVENING | Psalm 91:1–2 | Psalm | 91 | 1 | 2 |
| DEFAULT_26 | EVENING | Psalm 16:7–8 | Psalm | 16 | 7 | 8 |
| DEFAULT_27 | EVENING | Psalm 139:11–12 | Psalm | 139 | 11 | 12 |
| DEFAULT_28 | EVENING | Romans 8:38–39 | Romans | 8 | 38 | 39 |
| DEFAULT_29 | EVENING | Psalm 63:6–8 | Psalm | 63 | 6 | 8 |
| DEFAULT_30 | EVENING | Zephaniah 3:17 | Zephaniah | 3 | 17 | 17 |


## Mood-specific verses
Maintain separate lists for ANXIOUS, DISCOURAGED, OVERWHELMED, OKAY, PEACEFUL, GRATEFUL and UNKNOWN ("I don't know").
- After today's check-in, a mood-aware verse selection uses the approved list for that mood.
- Shuffle within that mood's pool and avoid repeats until its pool is exhausted. If only one entry exists, reuse it.
- Keep a selected mood verse stable for the same local day and mood across reopening.
- A changed mood can select from the new mood's pool. Tapping the already selected mood does not reshuffle.
- Missing/empty mood list, offline lookup failure or unavailable content falls back to the cached default verse. Never show an empty card.
- Do not infer mood from journal, prayer or chat text.

### Mood catalogs

10 selections per mood. References may belong to multiple pools; treat identical passages as the same content when avoiding immediate repeats between default and mood selections. A 10-item pool does not guarantee 14 days without repeats; the activity-pick engine's separate 14-day rule does not apply to these verse pools.

#### ANXIOUS

| ID | NIV reference | Book | Chapter | Start verse | End verse |
|---|---|---|---|---|---|
| ANXIOUS_01 | Philippians 4:6–7 | Philippians | 4 | 6 | 7 |
| ANXIOUS_02 | 1 Peter 5:7 | 1 Peter | 5 | 7 | 7 |
| ANXIOUS_03 | Psalm 56:3–4 | Psalm | 56 | 3 | 4 |
| ANXIOUS_04 | Isaiah 41:10 | Isaiah | 41 | 10 | 10 |
| ANXIOUS_05 | John 14:27 | John | 14 | 27 | 27 |
| ANXIOUS_06 | Matthew 6:34 | Matthew | 6 | 34 | 34 |
| ANXIOUS_07 | Psalm 94:19 | Psalm | 94 | 19 | 19 |
| ANXIOUS_08 | Psalm 46:1 | Psalm | 46 | 1 | 1 |
| ANXIOUS_09 | Isaiah 26:3 | Isaiah | 26 | 3 | 3 |
| ANXIOUS_10 | Psalm 121:1–2 | Psalm | 121 | 1 | 2 |

#### DISCOURAGED

| ID | NIV reference | Book | Chapter | Start verse | End verse |
|---|---|---|---|---|---|
| DISCOURAGED_01 | Psalm 34:18 | Psalm | 34 | 18 | 18 |
| DISCOURAGED_02 | Isaiah 40:29–31 | Isaiah | 40 | 29 | 31 |
| DISCOURAGED_03 | Galatians 6:9 | Galatians | 6 | 9 | 9 |
| DISCOURAGED_04 | 2 Corinthians 4:16–18 | 2 Corinthians | 4 | 16 | 18 |
| DISCOURAGED_05 | Psalm 42:11 | Psalm | 42 | 11 | 11 |
| DISCOURAGED_06 | Deuteronomy 31:8 | Deuteronomy | 31 | 8 | 8 |
| DISCOURAGED_07 | Psalm 147:3 | Psalm | 147 | 3 | 3 |
| DISCOURAGED_08 | Romans 15:13 | Romans | 15 | 13 | 13 |
| DISCOURAGED_09 | Lamentations 3:22–24 | Lamentations | 3 | 22 | 24 |
| DISCOURAGED_10 | Isaiah 43:2 | Isaiah | 43 | 2 | 2 |

#### OVERWHELMED

| ID | NIV reference | Book | Chapter | Start verse | End verse |
|---|---|---|---|---|---|
| OVERWHELMED_01 | Matthew 11:28–30 | Matthew | 11 | 28 | 30 |
| OVERWHELMED_02 | Psalm 61:1–2 | Psalm | 61 | 1 | 2 |
| OVERWHELMED_03 | Psalm 55:22 | Psalm | 55 | 22 | 22 |
| OVERWHELMED_04 | Isaiah 40:29 | Isaiah | 40 | 29 | 29 |
| OVERWHELMED_05 | 2 Corinthians 12:9 | 2 Corinthians | 12 | 9 | 9 |
| OVERWHELMED_06 | Psalm 46:10 | Psalm | 46 | 10 | 10 |
| OVERWHELMED_07 | Exodus 33:14 | Exodus | 33 | 14 | 14 |
| OVERWHELMED_08 | Psalm 62:5–8 | Psalm | 62 | 5 | 8 |
| OVERWHELMED_09 | Psalm 23:1–3 | Psalm | 23 | 1 | 3 |
| OVERWHELMED_10 | Hebrews 4:16 | Hebrews | 4 | 16 | 16 |

#### OKAY

| ID | NIV reference | Book | Chapter | Start verse | End verse |
|---|---|---|---|---|---|
| OKAY_01 | Psalm 118:24 | Psalm | 118 | 24 | 24 |
| OKAY_02 | Colossians 3:17 | Colossians | 3 | 17 | 17 |
| OKAY_03 | Micah 6:8 | Micah | 6 | 8 | 8 |
| OKAY_04 | Psalm 90:17 | Psalm | 90 | 17 | 17 |
| OKAY_05 | Proverbs 16:3 | Proverbs | 16 | 3 | 3 |
| OKAY_06 | Matthew 6:11 | Matthew | 6 | 11 | 11 |
| OKAY_07 | Philippians 4:11–13 | Philippians | 4 | 11 | 13 |
| OKAY_08 | 1 Corinthians 10:31 | 1 Corinthians | 10 | 31 | 31 |
| OKAY_09 | Psalm 16:8 | Psalm | 16 | 8 | 8 |
| OKAY_10 | Ephesians 2:10 | Ephesians | 2 | 10 | 10 |

#### PEACEFUL

| ID | NIV reference | Book | Chapter | Start verse | End verse |
|---|---|---|---|---|---|
| PEACEFUL_01 | Psalm 29:11 | Psalm | 29 | 11 | 11 |
| PEACEFUL_02 | John 14:27 | John | 14 | 27 | 27 |
| PEACEFUL_03 | Philippians 4:7 | Philippians | 4 | 7 | 7 |
| PEACEFUL_04 | Isaiah 26:3 | Isaiah | 26 | 3 | 3 |
| PEACEFUL_05 | Colossians 3:15 | Colossians | 3 | 15 | 15 |
| PEACEFUL_06 | Psalm 23:1–3 | Psalm | 23 | 1 | 3 |
| PEACEFUL_07 | Psalm 131:2 | Psalm | 131 | 2 | 2 |
| PEACEFUL_08 | Romans 15:13 | Romans | 15 | 13 | 13 |
| PEACEFUL_09 | Psalm 4:8 | Psalm | 4 | 8 | 8 |
| PEACEFUL_10 | 2 Thessalonians 3:16 | 2 Thessalonians | 3 | 16 | 16 |

#### GRATEFUL

| ID | NIV reference | Book | Chapter | Start verse | End verse |
|---|---|---|---|---|---|
| GRATEFUL_01 | Psalm 107:1 | Psalm | 107 | 1 | 1 |
| GRATEFUL_02 | 1 Thessalonians 5:16–18 | 1 Thessalonians | 5 | 16 | 18 |
| GRATEFUL_03 | James 1:17 | James | 1 | 17 | 17 |
| GRATEFUL_04 | Psalm 103:1–5 | Psalm | 103 | 1 | 5 |
| GRATEFUL_05 | Colossians 3:15–17 | Colossians | 3 | 15 | 17 |
| GRATEFUL_06 | Psalm 100:4–5 | Psalm | 100 | 4 | 5 |
| GRATEFUL_07 | Psalm 9:1 | Psalm | 9 | 1 | 1 |
| GRATEFUL_08 | Hebrews 12:28 | Hebrews | 12 | 28 | 28 |
| GRATEFUL_09 | Psalm 136:1 | Psalm | 136 | 1 | 1 |
| GRATEFUL_10 | Ephesians 5:20 | Ephesians | 5 | 20 | 20 |

#### UNKNOWN — I don’t know

| ID | NIV reference | Book | Chapter | Start verse | End verse |
|---|---|---|---|---|---|
| UNKNOWN_01 | Romans 8:26–27 | Romans | 8 | 26 | 27 |
| UNKNOWN_02 | Psalm 139:1–3 | Psalm | 139 | 1 | 3 |
| UNKNOWN_03 | Psalm 46:1 | Psalm | 46 | 1 | 1 |
| UNKNOWN_04 | Proverbs 3:5–6 | Proverbs | 3 | 5 | 6 |
| UNKNOWN_05 | Psalm 62:8 | Psalm | 62 | 8 | 8 |
| UNKNOWN_06 | James 1:5 | James | 1 | 5 | 5 |
| UNKNOWN_07 | Psalm 143:8 | Psalm | 143 | 8 | 8 |
| UNKNOWN_08 | Isaiah 30:21 | Isaiah | 30 | 21 | 21 |
| UNKNOWN_09 | Psalm 119:105 | Psalm | 119 | 105 | 105 |
| UNKNOWN_10 | Psalm 139:23–24 | Psalm | 139 | 23 | 24 |


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
- [x] Initial reference catalogs include 30 default and 70 mood assignments with stable IDs and reader navigation fields.
- [ ] Resolve and validate exact NIV text for each distinct passage from the app's authorized Bible source; seed and cache the catalog.
- [ ] Home shows an approved default verse before check-in without requiring a mood.
- [ ] Rotation shuffles eligible content without changing on every visit or render.
- [ ] Check-in, consent and subscription state follow the eligibility rules above.
- [ ] Mood-aware selection uses only the matching approved pool and respects consent.
- [ ] Empty pools and offline failures show cached default content.
- [ ] New local days, slot changes, mood changes, relaunch and repeat prevention are verified.
- [ ] Android and iOS use the same catalog and documented selection rules.

Related: [Daily Content Module](Daily%20Content%20Module.md), [Android scheduling #419](https://github.com/Stay-Positive-Organization/Stay-Positive-Kotlin-App/issues/419), [iOS scheduling #58](https://github.com/Stay-Positive-Organization/StayPositive-IOS/issues/58).
