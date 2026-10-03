# Home Screen

The main reference for the Stay Positive Home screen: what it contains, in what order, how Free and Premium differ, and where the detailed specs live.

> **One Home screen, conditional content.** Free and Premium share the same layout. Free sees Today's Verse, Premium badges in Explore more, and an ad banner. Premium sees Today's Verse until they check in, then **For your heart today**, and no ads.

**Source of truth:** the Figma file (Welcome Page frames and the screens they open). This folder describes that design and the product decisions behind it. It supersedes `stay-positive-home-free-premium-spec.md` where they conflict; conflicts are listed at the end.

## Naming

| Name | What it is |
|---|---|
| **For your heart today** | The daily personalized card on Home (Premium, after check-in). Code: `HeartPickCard`, events `heart_pick_*`. |
| **Reset Routine** | The existing, already-built Premium guided routine. Reached from Explore more. Not covered here. |
| **Today's Verse** | The general daily verse card (Free, and Premium before check-in or as fallback). Code: `DailyContentCard`. |

"Reset" refers only to Reset Routine. Never use it for the daily card.

## Documents in this folder

| Document | Covers |
|---|---|
| [design-tokens.md](design-tokens.md) | Colors, type, spacing, icons, dark mode, contrast |
| [mood-check-in.md](mood-check-in.md) | "How is your heart today?" check-in |
| [daily-content-module.md](daily-content-module.md) | Today's Verse and For your heart today (five pick types, Phase 1 rules) |
| [pick-content.md](pick-content.md) | The specific content for each mood and pick type |
| [pick-destinations.md](pick-destinations.md) | Meditation player, Guided prayer, Talk with Alex, Journaling |
| [stories-home.md](stories-home.md) | Today's story card and Story screen |
| [quotes-home.md](quotes-home.md) | "Words to carry" card |
| [streaks.md](streaks.md) | Streak icon and Your streak screen |
| [notifications.md](notifications.md) | Bell, Notifications screen, reminders, copy |
| [journal.md](journal.md) | Journal tab |
| [privacy-and-safety.md](privacy-and-safety.md) | Consent, data rules, Alex safety |
| [open-decisions.md](open-decisions.md) | What's still open, and every decision made |

## Screen structure

```text
HomeScreen
├── WelcomeHeader            "Hello, {name}", date, initial avatar
├── MoodCheckInCard          title row with StreakIcon + NotificationBell
│   ├── MoodOption × 6       3 × 2 grid
│   └── UnknownMoodOption    full width
├── HomeContentModule        forest card, the one bold element on Home
│   ├── DailyContentCard     Today's Verse
│   └── HeartPickCard        For your heart today (Premium, after check-in)
├── StoriesSection           "Stories" + Today's story card
├── QuotesSection            "Words to carry" card
├── ExploreMoreSection       Reset Routine, Virtual Library, Talk with Alex
├── AdBanner                 Free only, above the bottom navigation
└── BottomNavigation         Home · Meditations · Affirmations · Journal · Prayer
```

Build one `HomeScreen` with conditional content, not separate Free and Premium screens.

### Welcome header

| Element | Spec |
|---|---|
| Greeting | "Hello, {firstName}", with the name in forest. No eyebrow. |
| Date | e.g. "Thursday, April 16" |
| Avatar | Circle with the user's first initial. Opens Profile. |

Fonts, sizes and spacing: see the Figma file.

### Explore more

Title "Explore more", subtitle "Tools to help you stay grounded." One list with hairline dividers. Row: icon, title, subtitle, arrow.

| Tool | Free | Premium |
|---|---|---|
| Reset Routine | "PREMIUM" badge → upgrade screen | Opens Reset Routine |
| Virtual Library | "PREMIUM" badge → upgrade screen | Opens Virtual Library |
| Talk with Alex | "PREMIUM" badge → upgrade screen | Opens Talk with Alex |

Tapping a badged row opens the existing full-screen **upgrade screen**. Pass the tapped feature as `source` so it can be tracked.

Row subtitles: take the exact text from Figma.

### Bottom navigation

Home, Meditations, Affirmations, Journal, Prayer. All four content tabs are fully available to Free users, with no limits.

### Ad banner (Free only)

Full-width banner anchored **above** the bottom navigation (moved from below it in Figma, to avoid accidental taps that can flag the AdMob account). Home only.

## Free vs Premium

| Capability | Free | Premium |
|---|---|---|
| Mood check-in, history saved | Yes | Yes |
| Daily card | Today's Verse | Today's Verse before check-in; For your heart today after |
| Stories, Words to carry | Yes | Yes |
| Meditations, Affirmations, Journal, Prayer tabs | Yes, no limits | Yes |
| Streaks, Notifications | Yes | Yes |
| Reset Routine, Virtual Library, Talk with Alex | Badge → upgrade screen | Yes |
| Ad banner on Home | Yes | No |
| Personalization | No | Yes, with consent |

## Home state logic

```text
Load Home
 ├─ Load today's check-in (restore same-day selection)
 ├─ Render MoodCheckInCard
 ├─ Premium AND checked in today AND consented?
 │   ├─ No  → DailyContentCard (Today's Verse, morning/night rotation)
 │   └─ Yes → skeleton, then today's pick
 │        ├─ Pick exists for today → HeartPickCard
 │        ├─ Request succeeds      → HeartPickCard
 │        └─ Error                 → DailyContentCard
 ├─ Render Stories, Words to carry, Explore more
 └─ Free → AdBanner
```

Mood changed later the same day (Premium):
- Today's pick **not opened** → request a new pick for the new mood.
- Today's pick **opened or finished** → keep it.

## Content rules

- The app never adds its own ads to meditation, prayer, journaling, Alex or completion screens. Meditations are YouTube videos; ads YouTube shows inside a video are outside the app's control.
- Never show journal or prayer text written by the user on Home.
- Never claim content is personalized when it isn't.
- Never imply a diagnosis or treatment from a mood.
- `I don't know` is a valid check-in.

## Analytics

```text
home_viewed
mood_checkin_viewed
mood_selected            { mood, isPremium, source: "HOME" }
mood_changed             { mood, previousMood, isPremium }
daily_content_viewed     { contentId, slot }
daily_content_opened     { contentId }
heart_pick_viewed        { pickId, contentType }
heart_pick_opened        { pickId, contentType }
heart_pick_completed     { pickId, contentType }
explore_feature_opened   { feature, locked }
upgrade_screen_viewed    { source }
streak_opened
notifications_opened
ad_banner_viewed / ad_banner_clicked
```

Never send journal, prayer or chat text in analytics.

## Accessibility

- WCAG 2.1 AA; see [design-tokens.md](design-tokens.md).
- Content descriptions on icon-only buttons (bell, streak, avatar, heart, share, mic).
- 44 × 44dp minimum touch targets, including the small streak and bell icons.
- Mood options expose a selected state.
- Respect reduced motion.

## Changes from the earlier spec

| Earlier spec | Now |
|---|---|
| "WELCOME BACK" eyebrow | Removed |
| "Your Personalized Reset" | "For your heart today" + "Chosen for you" |
| Premium always shows the personalized card | Only after a check-in; Today's Verse before |
| CTA "Start Now" | Specific CTA per pick type |
| "Journaling prompt" | Free-text journaling, never a prompt |
| Six tools in Explore more | Reset Routine, Virtual Library, Talk with Alex |
| Home: check-in, daily content, Explore more | Adds Stories, Words to carry, streak and bell, ad banner (Free) |