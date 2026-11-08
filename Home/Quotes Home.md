# Quotes: "Words to carry"

Shown to Free and Premium, after Stories and before Explore more. One quote per day, the same for everyone. Quotes are our own: written by Stay Positive or posted by Seeds for Life.

Figma: [Welcome Page - Free](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=2699-143)

## Layout

```text
┌────────────────────────────────────┐
│ ── Words to carry                  │
│ "                                  │
│ Not every wave is meant to knock   │
│ you down. Some are meant to teach  │
│ you how to rise stronger.          │
│ Seeds for Life                     │
│                                    │
│ ( See more )               ♡   ⇪   │
└────────────────────────────────────┘
```

| Element | Spec |
|---|---|
| Card | Sand surface (`cream_muted`), 20dp corners, 1dp gold stroke, full width |
| Label | Gold line (27dp × 1dp) + "Words to carry", Montserrat Medium |
| Quote mark | Large gold “, top left above the quote |
| Quote | Alegreya Italic, ~19sp, forest. Shown without quote marks around it (the gold “ is the opening mark) |
| Author | Montserrat Medium, small, sage-muted |
| See more | Outline pill, gold, Cormorant Italic (buttons use Cormorant Italic) |
| Actions | Heart (save), Share. 48dp tap areas. No comments. |

Fonts follow the app rule: Montserrat for text, Alegreya for titles and quotes, Cormorant Italic for buttons.

## Today's quote

Quotes live in Firebase Realtime Database and are edited in the Firebase console, not in the app.

```text
quotes/
  library/
    {quoteId}/            e.g. "sfl_0001"
      text                no quote marks around it
      author              "Stay Positive" or "Seeds for Life"
      order               rotation position: 1, 2, 3…
      active              optional, defaults to true
  schedule/
    {yyyy-MM-dd}          quoteId, e.g. "2026-12-25": "sfl_0042"
```

The app picks the quote in this order:

1. **Scheduled:** the quote set for today's date in `schedule`, if it's active. Use this for special days (Christmas, Easter, Lent, New Year…).
2. **Already shown today:** the quote this device showed earlier today, so the card never changes in the middle of someone's day.
3. **Rotation:** the next quote from `library`, one per day in `order`, starting over after the last one. Inactive quotes and any quote that appears in `schedule` are skipped, so holiday quotes don't show up on random days.
4. **Fallback:** if nothing can be loaded (first launch offline, or an empty library): "The more you protect your peace, the more your life begins to bloom." — Stay Positive.

The day changes at the user's local midnight. If Home is left open past midnight, the new quote loads when the user comes back to it.

**Adding and retiring quotes**
- Add new quotes at the end with the next `order` number. Never reuse or renumber ids: saved quotes are stored by id.
- To retire a quote, set `active: false`. Don't delete it.
- Adding or retiring quotes shifts the rotation from the next day on. That's expected.
- Database rules: `quotes` is readable by signed-in users and not writable from the app.

## Actions

| Action | Result |
|---|---|
| See more | Opens https://www.instagram.com/seedsforlife1111/ in the Instagram app, or the browser if Instagram isn't installed. The URL is one app config value. |
| Heart | Saves to the **Quotes favorites** list (separate from Affirmations favorites), stored by quote id. Filled heart when saved; tapping again unsaves. There is no screen to view saved quotes yet (Phase 2). |
| Share | Share sheet with `“{quote}” — {author}` |

## Content rules

- Use only our own quotes: credited **Stay Positive** (written by us) or **Seeds for Life** (posted by Seeds for Life, no outside author).
- No quotes by outside authors, including public domain authors.
- The full list, and what was left out and why, is in [Quotes.md](Quotes.md).

## Analytics

```text
quote_impression     { quoteId }
quote_see_more
quote_saved / quote_unsaved  { quoteId }
quote_shared         { quoteId }
```
