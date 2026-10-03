# Stories: Home Card and Story Screen

Design detail for Stories. Requirements live in `Stories Feature.md`; this doc adds layout, copy, and the MVP decision on comments.

> **No comments in MVP.** Stories have Like and Share only. The comment data model, reporting, moderation tools and comment analytics from `Stories Feature.md` are out of MVP.

## Home card

Directly after the daily card. Free and Premium.

```text
Stories
Real moments of faith, hope, and healing.
┌──────────────────────────────────────┐
│ [ image ]                            │
│ — Today's story                      │
│ How Much Are You Worth?              │
│ When someone asks this question, our │
│ minds often rush to a monetary…      │
│ Claudia da S.                 ♥   ⇪  │
└──────────────────────────────────────┘
```

| Element | Spec |
|---|---|
| Card | warmWhite, thin outline, rounded; whole card opens the Story |
| Image | `imageUrl`; omit the area if null |
| Tag | Gold line + "Today's story" |
| Title | Cormorant 600, ~22–24sp, forest |
| Excerpt | `excerpt`, small, muted, 2–3 lines |
| Footer | `authorName` (omit if null); Like and Share on the right |

Only the featured Story is shown on Home.

## Story screen (Figma)

```text
‹                                   ⇪
┌──────────────────────────────────┐
│ [ image ]                        │
└──────────────────────────────────┘
— Today's story
The morning I stopped pretending
Claudia da S.

Story body…

( ⇪ Share )                       ♡
```

| Area | Spec |
|---|---|
| Top bar | Back (left), Share icon (right). Share appears here and in the bottom bar; both open the same share sheet. |
| Image | `imageUrl`, rounded; omit if null |
| Tag | Gold line + "Today's story" (only for today's featured Story) |
| Title | Story title |
| Author | `authorName`; omit if null |
| Body | `content`, with paragraph breaks preserved |
| Bottom bar | "Share" outline button (left), Like heart (right) |
| End of story | Reaching the end of the body fires `story_read_complete` |

Visual details are in Figma.

### Like

- Signed-in users can like; tapping again unlikes. One like per user per Story.
- **No like count is shown** to users (Home card or Story screen). Still store likes so the count is available for analytics. This replaces the "display total likes" requirement in `Stories Feature.md`.
- Like state persists across sessions.
- Signed out: toast "Sign in to like stories."

### Share

Native share sheet with the title and the Story's unique link. Deep link opens the Story in the app; web fallback for people without the app (per `Stories Feature.md`).

## Streaks

Opening a Story counts as streak activity.

## Analytics (MVP)

```text
story_impression
story_open
story_like / story_unlike
story_share_tap
story_share_link_open
story_read_complete
story_deep_link_open
```

Comment events (`story_comment_*`) are out of MVP.