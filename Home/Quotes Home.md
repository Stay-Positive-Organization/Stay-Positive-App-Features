# Quotes: "Words to carry"

Shown to Free and Premium, after Stories and before Explore more. All quotes come from Seeds for Life.

## Layout

```text
┌────────────────────────────────────┐
│ — Words to carry                   │
│ "                                  │
│ Let nothing disturb you, let       │
│ nothing frighten you. All things   │
│ are passing; God never changes.    │
│                                    │
│ Teresa of Ávila                    │
│                                    │
│ ( See more )               ♡   ⇪   │
└────────────────────────────────────┘
```

| Element | Spec |
|---|---|
| Card | Sand surface, rounded, full width |
| Label | Gold line + "Words to carry" |
| Quote mark | Large gold “ |
| Quote | Cormorant Italic, ~18–20sp |
| Author | Small, sage-muted |
| See more | Outline pill |
| Actions | Heart (save), Share. No comments. |

One quote per day, rotated editorially.

## Actions

| Action | Result |
|---|---|
| See more | Opens https://www.instagram.com/seedsforlife1111/ in the Instagram app, or the browser if Instagram isn't installed. Store the URL as one app config value. |
| Heart | Saves to the **Quotes favorites** list (separate from Affirmations favorites). Filled heart when saved; tapping again unsaves. There is no screen to view saved quotes yet (Phase 2), so store them per user for later. |
| Share | Share sheet with `"{quote}" — {author}` |

## Content rules

- Use authors whose original works are in the public domain, and check the English translation is too (or licensed).
- Modern authors need permission.
- Verify attributions before publishing.

## Analytics

```text
quote_impression     { quoteId }
quote_see_more
quote_saved / quote_unsaved  { quoteId }
quote_shared         { quoteId }
```