# Shop Stay Positive

**Status:** Feature specification for implementation; not a claim that the feature has shipped.  
**Platforms:** Android (Kotlin) and iOS product behavior.  
**Access:** Free and Premium, no badge, no upgrade screen.  
**Design:** [Shop Stay Positive entry canvas](https://claude.ai/artifact/VGYs7Zvho2gNwQPBzk3HJ2). Not in the Figma file yet; once added there, Figma is the source of truth.

## Purpose

The app has no visible link to the Stay Positive store, so users may not know it exists. This adds one quiet entry point on Home that opens the store website. Browsing, cart and checkout all happen on the website, not in the app.

## Placement

The **last row of Explore more** on Home, after Reset Routine, Virtual Library and Talk with Alex. See [Home Screen](README.md).

```text
ExploreMoreSection
├── Reset Routine
├── Virtual Library
├── Talk with Alex
└── Shop Stay Positive      new, external link
```

Why here:

- Explore more is already where Home says "there's more here", and users pass it every time they scroll past the daily content.
- Last in the list, after the wellness tools, so the store reads as an extra and never competes with check-in, daily content, Stories or Words to carry.
- The Profile screen is account settings only (Edit Profile, Change Password, Delete Account, Logout), so it was not chosen.

On Free, the row sits above the ad banner, never inside or next to it as part of the ad.

## Row

Same pattern as the other Explore more rows, with two differences: no PREMIUM badge, and an external-link icon instead of the arrow.

| Element | Spec |
|---|---|
| Leading icon | Shopping bag with a heart inside, line style, `sage`. Matches the heart motif in the Reset Routine and Talk with Alex icons. |
| Title | Shop Stay Positive |
| Subtitle | Discover pieces inspired by faith and positivity. |
| Trailing icon | Open-in-new (↗), same color as the other rows' arrows. Signals that the row leaves the app. |
| Badge | None, for Free and Premium |
| Dividers | Same hairline dividers as the other rows; one below this row as it is last |
| Pressed state | Standard ripple / highlight, same as the other rows |

Subtitle uses `muted`, not `sage`: sage fails contrast for small text (see [design-tokens.md](design-tokens.md)).

Fonts, sizes and spacing: see the design (Figma once added).

## Behavior

1. User taps anywhere on the row.
2. Log `explore_feature_opened { feature: "shop", locked: false }`.
3. Open the store URL outside the app:
   - **Android:** Chrome Custom Tab, toolbar color `forest`. If no Custom Tabs browser is available, open the default browser with `ACTION_VIEW`.
   - **iOS:** `SFSafariViewController`.
4. Closing the tab or pressing Back returns to Home at the same scroll position.

No confirmation dialog before opening; the ↗ icon sets the expectation. No change to streaks, check-in, daily content or ads.

If the URL can't be opened (no browser), show a short snackbar: "Couldn't open the store. Please try again." Don't hide the row.

Store URL: keep it in remote config (or a single constant), not hard-coded in the row, so it can change without a release.

## Accessibility

- The row is one target, role **link**, at least 48dp tall.
- Content description: "Shop Stay Positive. Discover pieces inspired by faith and positivity. Opens in your browser."
- Both icons are decorative (no separate content descriptions).

## Analytics

```text
explore_feature_opened   { feature: "shop", locked: false }
```

Sent before handing off to the browser. Nothing is tracked inside the store website from the app.

## Optional card variant (not the permanent entry)

The design also has a card with a **Visit the Store** button (forest pill, white text, ↗). Use it only for a one-off promotion, such as a new collection. The Explore more row stays the permanent entry.

## Open decisions

| Question | Status |
|---|---|
| Store URL | Open |
| Add the design to the Figma file | Open |

## Acceptance criteria

- [ ] "Shop Stay Positive" is the last row in Explore more, for Free and Premium.
- [ ] No PREMIUM badge; tapping never opens the upgrade screen.
- [ ] Row shows the bag icon, title, subtitle and ↗ icon, matching the design.
- [ ] Tapping opens the store website in a Custom Tab (Android) or Safari view (iOS), with the browser fallback.
- [ ] Returning lands on Home at the same scroll position.
- [ ] `explore_feature_opened { feature: "shop", locked: false }` is logged on tap.
- [ ] Subtitle meets 4.5:1 contrast; row is one 48dp+ target with the content description above.
- [ ] On Free, the row sits above the ad banner and is visually separate from it.
