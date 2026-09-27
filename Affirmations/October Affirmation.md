# October Daily Affirmations — Feature Specification

**Product:** Stay Positive Android app  
**Campaign:** October 1–31, 2026  
**Access:** Free for all users  
**Status:** Product and developer handoff

## Purpose

Show one October affirmation directly in the existing **Today's Affirmation** card on the home screen each day. A user should immediately see the affirmation, its category, and which day of the 31-day series it is. No ZIP download, signup, or separate October collection screen is required for this feature.

## Home screen experience

On each local calendar day in October 2026, use the existing top affirmation card:

| Element | Display rule | October 1 example |
| --- | --- | --- |
| Eyebrow | `OCTOBER AFFIRMATION · DAY {day} OF 31` | `OCTOBER AFFIRMATION · DAY 1 OF 31` |
| Main text | Exactly one affirmation assigned to that date | “I am allowed to begin again.” |
| Category chip | The category assigned to that day's affirmation | `Self-Worth` |
| Actions | Keep the existing favorite and share actions | Heart and share icons |

The card should remain readable on a small phone. Let long affirmations wrap naturally; do not truncate the text. Use the current home-card style and accessibility settings. The `DAY {day} OF 31` label must be visible without opening another screen. The category is a descriptive label for this daily series; it does **not** add an item to, or change counts in, the existing **Explore Categories** section.

The separate **October Affirmations** promotional/category card shown in the current home design should be removed or hidden. The existing general categories remain available.

## Date and rotation rules

1. **October 1–31, 2026:** Show the entry whose `day` equals the user's local day of the month. All users in the same local date see the same affirmation. Day 1 is October 1; Day 31 is October 31.
2. **Changeover:** Re-evaluate on app launch, when the home screen resumes, and when the local calendar date changes while the app is open. The new affirmation should appear at local midnight without requiring a reinstall or manual refresh.
3. **Outside the campaign:** Before October 1 and from November 1 onward, show the normal Today's Affirmation behavior. Do not show an October day label outside the campaign.
4. **Offline:** Bundle or cache all 31 entries so the correct day can still display without a network connection. The date calculation uses the device's current local time zone.
5. **Favorite/share:** Reuse existing actions for the visible entry. Save the entry by its stable ID (`oct-2026-01` through `oct-2026-31`), so a favorite remains associated with the correct affirmation after the date changes. Sharing uses the currently visible day's text and existing share behavior.

## Category labels

Each entry has **one** campaign category. These labels describe the affirmation's theme and appear as the chip on the home card:

- **Faith** — trust in God and His presence.
- **Peace & Well-Being** — rest, calm, feelings, and boundaries.
- **Self-Worth** — dignity, self-compassion, and freedom from comparison.
- **Growth & Courage** — progress, hope, and brave steps.
- **Connection** — support, asking for help, and caring for others.

These are campaign labels, not new global browsing categories. In particular, **Faith** is not labeled **Scripture Affirmations**: the entries mention God but do not quote a Bible verse or claim a Bible reference.

## Approved October content

Use the text below exactly, including punctuation and apostrophes. The dates are in the user's local calendar.

| Day | Date | Category | Affirmation |
| ---: | --- | --- | --- |
| 1 | Oct 1 | Self-Worth | I am allowed to begin again. |
| 2 | Oct 2 | Faith | God meets me where I am today. |
| 3 | Oct 3 | Growth & Courage | I can take one faithful step at a time. |
| 4 | Oct 4 | Self-Worth | My worth is not measured by my productivity. |
| 5 | Oct 5 | Peace & Well-Being | I can rest without falling behind. |
| 6 | Oct 6 | Growth & Courage | I am growing, even when progress feels quiet. |
| 7 | Oct 7 | Peace & Well-Being | I release what I cannot control. |
| 8 | Oct 8 | Peace & Well-Being | Peace is available to me in this moment. |
| 9 | Oct 9 | Growth & Courage | My voice matters, and I can use it with courage. |
| 10 | Oct 10 | Peace & Well-Being | I can feel deeply and still move forward. |
| 11 | Oct 11 | Connection | I do not have to carry today alone. |
| 12 | Oct 12 | Faith | God is with me in the waiting. |
| 13 | Oct 13 | Connection | I can ask for help and still be strong. |
| 14 | Oct 14 | Connection | Small acts of care make a difference. |
| 15 | Oct 15 | Growth & Courage | I am learning to trust my own pace. |
| 16 | Oct 16 | Growth & Courage | My future does not require me to fear today. |
| 17 | Oct 17 | Self-Worth | I can be gentle with myself as I grow. |
| 18 | Oct 18 | Self-Worth | I am more than a difficult season. |
| 19 | Oct 19 | Growth & Courage | Hope can begin with one small choice. |
| 20 | Oct 20 | Peace & Well-Being | I make room for joy without guilt. |
| 21 | Oct 21 | Peace & Well-Being | I can pause, breathe, and begin again. |
| 22 | Oct 22 | Growth & Courage | I am becoming more grounded each day. |
| 23 | Oct 23 | Faith | God's love is steady, even when I am uncertain. |
| 24 | Oct 24 | Growth & Courage | I can choose courage without having all the answers. |
| 25 | Oct 25 | Peace & Well-Being | My boundaries make space for peace. |
| 26 | Oct 26 | Growth & Courage | I celebrate the progress I used to pray for. |
| 27 | Oct 27 | Self-Worth | I am worthy of care, connection, and rest. |
| 28 | Oct 28 | Self-Worth | I can let go of comparison and honor my journey. |
| 29 | Oct 29 | Faith | I trust God with what I cannot yet see. |
| 30 | Oct 30 | Growth & Courage | I have made it through hard days before. |
| 31 | Oct 31 | Growth & Courage | I step into what is next with hope. |

## Suggested data shape

```json
{
  "id": "oct-2026-01",
  "campaign": "october-2026-daily-affirmations",
  "date": "2026-10-01",
  "day": 1,
  "totalDays": 31,
  "category": "Self-Worth",
  "text": "I am allowed to begin again."
}
```

All 31 records need a unique ID and date. The visible day label and category should come from the same record as the text. The implementation can use the app's existing content store or bundled configuration; this document does not require a new service.

## Acceptance checks

- On October 1 in a device's local time zone, the top card shows Day 1, its category, and the Day 1 text; on October 31 it shows Day 31.
- On a date change while the app stays open, the card updates to the next entry. It also updates when the user returns to the home screen.
- The category chip and day label always match the text, including on a small screen and offline.
- Favorite and share refer to the displayed day's entry; prior favorites are not overwritten on the next day.
- The separate October category card does not duplicate the daily feature, and normal home affirmation behavior returns on November 1.