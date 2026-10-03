# Design Tokens

Fonts, sizes, spacing and layout live in the Figma file. This doc covers what Figma doesn't: color names for code, contrast rules, motion, and assets.

The app has **no dark mode** for now.

## Colors

Use these names in code, matching the Figma color styles.

| Token | Hex | Use |
|---|---|---|
| `forest` | #3A584A | Primary color, headings, primary buttons, bold cards |
| `sage` | #8FB0A1 | Decoration, outlines, filled heart for liked or saved items |
| `gold` | #B8976A | Decoration: accent lines, dots, flame, sound bars |
| `warmWhite` | #FDFAF7 | App background; text and buttons on forest |
| `surface` | #F4EFE7 | Sand cards and default mood tiles |
| `line` | #E3DBCF | Dividers and card outlines |
| `ink` | #3A584A | Headings and primary text |
| `text` | #2F3F37 | Long reading text (Stories, journal) |
| `muted` | #5E6F66 | Secondary text, timestamps, inactive tabs |
| `goldText` | #7D6139 | Gold-colored text on light backgrounds |
| `goldOnForest` | #E0C9A6 | Gold-colored text on forest cards |
| `danger` | #A9564B | Destructive actions (delete) |
| Mood pastels | From Figma | Mood tiles after check-in |

## Contrast rules

Target WCAG 2.1 AA: 4.5:1 for normal text.

| Pair | Ratio | Small text OK |
|---|---|---|
| forest on warmWhite | 7.55 | Yes |
| muted on warmWhite | 5.12 | Yes |
| muted on surface | 4.65 | Yes |
| goldText on warmWhite | 5.55 | Yes |
| goldText on surface | 5.04 | Yes |
| goldOnForest on forest | 4.89 | Yes |
| sage on warmWhite | 2.27 | No |
| gold on warmWhite | 2.63 | No |

- `sage` and `gold` are decoration only, never small text on light backgrounds.
- Gold-colored text uses `goldText` (light backgrounds) or `goldOnForest` (forest cards). These replace the earlier #8A6C42 and #D2B68C, which fail AA; Figma is being updated to match.
- Check label contrast on each pastel mood tile.

## Motion

| Animation | Behavior |
|---|---|
| Mood selection | Short color change |
| Like / save heart | Small pop when filled |
| Sound bars (listening) | Bars rise and fall in a loop, staggered |
| Mic while listening | Pulsing ring |
| Empty journal page | Blinking cursor |

When the system **reduce motion** setting is on, turn off all looping animations.

## Icons and illustrations

Line icons: 24 × 24, 1.5 stroke, round caps and joins, `forest` (or `warmWhite` on forest).

| Asset | File |
|---|---|
| Guided meditation | guided-meditation.svg |
| Talk with Alex | talk-with-alex.svg |
| Virtual library | virtual-library.svg |
| Share | share.svg (used on all platforms, as in Figma) |
| Streak | streak.svg |
| Bell / reminder | reminder.svg |
| Microphone | microphone.svg |
| Sound bars | sound-bars.svg |
| Verse card sprig | verse-card-sprig.svg |
| Meditation pick thumbnail | meditation-reset-thumbnail.svg |
| Story image | story-featured-image.svg / @3x.png |

After converting SVGs to Android Vector Drawables, check that transparency (`fillAlpha`) survived.