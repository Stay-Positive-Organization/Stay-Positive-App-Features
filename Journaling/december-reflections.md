# December Reflections

**Status:** Feature specification for implementation; not yet a shipped feature.  
**Location:** Journal tab.  
**Platforms:** Shared product behavior for Android (Kotlin) and iOS.  
**Campaign:** December / Christmas season.  
**Card subtitle:** Make a little space to write about what's on your heart this season.

## Purpose

Offer one optional personal-writing prompt for each day of December, so people have a gentle, private place to notice how they're feeling through the holiday season and the close of the year.

December Reflections is a **Journal** experience. The Christmas Bible study belongs to Bible Study and is a separate feature: the two never share progress, completion, or entries.

This extends the existing [Journal specification](../Home/Journal.md) and follows the same pattern as [30 Days of Gratitude](30-days-of-gratitude.md). Regular free-writing keeps its existing behavior; only December Reflections entries carry an assigned prompt.

## First-version scope

- December Reflections card on the Journal tab, in the slot the November "Your gratitude journey" card uses.
- A prompt list showing all 31 days and their state.
- A prompt-entry screen built on the existing journal editor.
- Saving marks the day complete, updates progress, and adds the entry to the normal Journal list and calendar.
- Editing saved entries; opening any of the 31 prompts at any time.

Self-paced by design:
- No locked days. Day 20 can be opened on December 3.
- No streak, deadline, countdown, or reset. Missing days has no consequence.
- One reflection per day number per user.

## User flow

1. Open the Journal tab.
2. See the **December reflections** card.
3. Tap **Start Day 1** (or **Continue Day {n}**) to open that day's prompt-entry screen, or **See all 31 prompts** to pick any day.
4. Write a reflection.
5. Tap **Save Entry**.
6. The day is marked complete, progress updates, and the entry appears in the Journal list and calendar.
7. Return later to continue, open any other day, or edit a saved reflection.

## Journal tab card

Replaces the November **Your gratitude journey** card in the same position: full width, under the Explore prompts and Talk it through cards. The header (Journal, lock line "Only you can see your entries", calendar icon), **New entry**, the saved-entry list, the Free ad banner and bottom navigation stay unchanged.

| State | Content | Primary action | Secondary action |
|---|---|---|---|
| Not started | **December reflections** / Make a little space to write about what's on your heart this season. / 0 of 31 reflections completed | Start Day 1 | See all 31 prompts |
| In progress | **December reflections** / same subtitle / {completedCount} of 31 reflections completed | Continue Day {n} | See all 31 prompts |
| All complete | **December reflections** / same subtitle / 31 of 31 reflections completed | Read my reflections | See all 31 prompts |

- **Continue Day {n}** opens the lowest-numbered day that isn't completed, restoring its draft if one exists.
- Progress counts distinct completed days only. Opening a prompt, or a draft, does not count.
- Progress uses a thin progress bar plus the text count, so it doesn't rely on color alone.
- "See all 31 prompts" is a text link, not a second button.

Design: Figma › Journaling V3 › December Reflections row
- [Journal tab with card](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=3319-974)
- [Card component, 3 states](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=3319-972)
- [All prompts](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=3321-1019) · [Prompt row component](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=3321-1018)
- [Prompt entry](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=3322-1086) · [Prompt entry, empty](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=3322-1152)
- [Saved](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=3322-1218)

## All prompts screen

Opened from **See all 31 prompts**.

- Header: **December reflections**, back action.
- Intro line: **Write when it helps. Every prompt is open, any day.**
- Progress: **{completedCount} of 31 reflections completed**, with an accessible progress bar.
- A scrolling list of Day 1 to Day 31, in order. Each row shows the day number, its date (e.g. "Thu, Dec 3"), the prompt (up to two lines), and a state: **Not started**, **Draft**, or **Completed** (text plus icon, not color alone).
- Today's day (during December) is gently highlighted with a "Today" label. This is a pointer, not a restriction.
- Tapping any row opens that day's prompt-entry screen with its existing entry, if any.

## Prompt-entry screen

Reuses the existing journal editor (ruled page, optional mood chip, dictation behavior and Premium rules, autosaved drafts, privacy footer).

| Element | Content / behavior |
|---|---|
| Top bar | Back action; **Day {n} · {Weekday}, December {n}** |
| Prompt | That day's exact prompt (heading style) |
| Writing field | Large free-writing area. Placeholder: **Start wherever your heart is today…** |
| Mood | Existing optional mood chip / grid behavior |
| Privacy reminder | 🔒 **Only you can see your entries** |
| Primary action | **Save Entry** (forest button) |
| Saved entry | Button reads **Save changes** when editing a completed day |

Rules:
- A whitespace-only reflection cannot be saved as complete; **Save Entry** stays disabled until there's text.
- No minimum length.
- The date shown is the prompt's day in December. The entry's own saved date is when the person actually wrote it (Day 5 written on December 12 is listed under December 12 in the Journal list and calendar, labeled Day 5).
- Leaving without saving keeps the autosaved draft (existing editor behavior) and shows the day as **Draft**.
- Don't confirm a save until the write succeeds. On failure, keep the text, show a retry, and leave the day's state unchanged.

## After saving

Show a short, calm confirmation:

> **Reflection saved.**  
> Day {n} is part of your December now.

Actions: **Back to December reflections** (prompt list) and **Done** (Journal tab). The card and list reflect the new count right away.

After all 31:

> **31 reflections. A whole season, written down.**  
> Come back to them whenever you want to remember this December.

Primary action: **Read my reflections**, opening the person's December Reflections entries in day order.

No guilt-based messaging for missed days, ever.

## Journal list and calendar integration

- One entry, shared between December Reflections and the normal Journal list; never a duplicate copy.
- Journal list row label (small gold label): **DECEMBER REFLECTIONS · DAY {n}**, with the usual two-line preview and mood.
- The calendar shows the entry on the date it was written.
- The prompt is stored with the entry so it stays readable when revisited.
- Editing keeps the entry's original date and keeps the day completed (if it's not emptied).
- Deleting uses the existing confirmation sheet. Deleting a completed day returns it to **Not started** and lowers progress.
- Removing all text from a completed entry and saving uses the existing delete confirmation; it doesn't silently clear completion.
- Progress and drafts survive navigation, app restarts and account restore, per the existing Journal sync.

## Separation from Bible Study

- December Reflections progress lives only in Journal.
- Completing a Bible Study Christmas day does not complete a December Reflections day, and vice versa.
- No shared counters, badges or completion screens.

## Prompt content

Use these prompts exactly. Day IDs are stable and independent of wording.

| Day | Stable ID | Prompt |
|---|---|---|
| 1 | december-01 | What feeling are you carrying into December? |
| 2 | december-02 | What would help you feel grounded this week? |
| 3 | december-03 | What small moment brought you comfort today? |
| 4 | december-04 | What does peace look like for you right now? |
| 5 | december-05 | What do you want to make more room for this month? |
| 6 | december-06 | Who has helped you feel supported recently? |
| 7 | december-07 | What boundary would protect your energy this season? |
| 8 | december-08 | What is one thing you can release instead of carrying? |
| 9 | december-09 | What tradition brings warmth or meaning to you? |
| 10 | december-10 | What are you looking forward to? |
| 11 | december-11 | What feels heavy about this season, and what support would help? |
| 12 | december-12 | What is one way you can show kindness to yourself? |
| 13 | december-13 | What have you handled this year that deserves recognition? |
| 14 | december-14 | What is one thing you want to savor this week? |
| 15 | december-15 | What helps you reconnect with hope? |
| 16 | december-16 | What would a restful evening look like for you? |
| 17 | december-17 | What meaningful gift can you give that costs nothing? |
| 18 | december-18 | What do you appreciate about the people in your life? |
| 19 | december-19 | What could help when holiday expectations feel overwhelming? |
| 20 | december-20 | What would you like to forgive yourself for? |
| 21 | december-21 | What are you learning about the support you need? |
| 22 | december-22 | What moment this month has made you smile? |
| 23 | december-23 | What do you want to remember about this season? |
| 24 | december-24 | What could help you feel present today? |
| 25 | december-25 | What is one thing you want to carry forward from Christmas? |
| 26 | december-26 | How are you feeling now that Christmas has passed? |
| 27 | december-27 | What expectation can you let go of before the year ends? |
| 28 | december-28 | What did this year teach you about yourself? |
| 29 | december-29 | What small win do you want to acknowledge? |
| 30 | december-30 | What do you want to leave behind as the year closes? |
| 31 | december-31 | What intention do you want to carry into the new year? |

## Visual direction

Match the current Journal tab so the card feels native, not promotional.

- Palette: warm cream background (`warmWhite`), soft peach card (#FAE5DA, outline #F1D3C2, same as the November card), `forest` for headings and the primary button, `sage` (#8FB0A1, the Figma color style) for the progress bar and decoration only.
- `sage` and peach are decoration only; never small text on light backgrounds (see [design tokens](../Home/design-tokens.md)).
- Typography per app standard: Alegreya for titles, Montserrat for body and supporting text, Cormorant Garamond Bold on buttons.
- Optional subtle seasonal detail (a small sprig or star line icon), kept outside the writing area.
- Calm and welcoming; no countdowns, confetti, or urgency.

Support large text, screen readers (progress announced as "{n} of 31 reflections completed"), and small screens without clipping.

## Privacy

Inherit the Journal privacy rules:
- Entries are visible only to their owner.
- Reflection text never appears in Home previews, notifications, analytics, or logs.
- No use for personalization without explicit consent.
- Dictation follows existing behavior; audio isn't retained.
- No sharing in this version.

## Suggested persistence contract

Adapt to the existing Journal schema rather than a separate store of reflection text.

- Journey identifier: `december-reflections-2026`.
- Existing journal entry linked to journey ID and stable day ID (`december-01` … `december-31`).
- Prompt snapshot, body, optional mood, created/updated timestamps.
- Entry state: draft or completed, with completion timestamp.
- At most one active entry per user/journey/day.
- Completed count derived from distinct completed entries (or a cache kept consistent with them).
- Repeated taps and retries never duplicate an entry or double-count progress.
- No fields shared with Bible Study progress.

## Acceptance criteria

- [ ] The December reflections card appears in the seasonal slot on the Journal tab; header, New entry, entry list, calendar icon and bottom navigation are unchanged.
- [ ] A new user sees "0 of 31 reflections completed" and **Start Day 1**.
- [ ] After completing any day, the card shows **Continue Day {n}** for the lowest-numbered incomplete day.
- [ ] **See all 31 prompts** lists Day 1–31 with dates, prompts, and correct states.
- [ ] Every day can be opened at any time; no day is locked.
- [ ] All 31 prompts match the table above exactly and map to the correct stable IDs.
- [ ] The prompt-entry screen shows day number and date, the prompt, a writing field, **Save Entry**, and "Only you can see your entries".
- [ ] Save Entry is disabled for empty or whitespace-only text.
- [ ] Saving marks the day complete and increases progress exactly once.
- [ ] Saved entries appear in the Journal list (labeled DECEMBER REFLECTIONS · DAY {n}) and on the calendar for the date written.
- [ ] Editing a saved entry keeps its completion and original date.
- [ ] Deleting a completed entry returns the day to Not started and lowers progress.
- [ ] Drafts and progress survive leaving the screen and restarting the app.
- [ ] A failed save keeps the text and doesn't show a false confirmation.
- [ ] Completing all 31 shows the final message and **Read my reflections**.
- [ ] December Reflections and Bible Study progress are fully independent.
- [ ] No streak, deadline, lock or reset exists in this feature.
- [ ] Another account can't read the person's reflections or progress.
- [ ] Reflection text is excluded from analytics, logs, notifications and previews.
- [ ] Large text, screen readers and small screens remain usable.

## Decisions

- **Access:** open to everyone, Free and Premium. No Premium badge on the card. (Dictation inside the editor keeps its existing Premium rule.)
- **Card timing:** the December Reflections card replaces the November gratitude card in the seasonal slot from December 1 through December 31 (user's local time), and leaves the Journal tab on January 1. Saved gratitude and December entries stay in the Journal list and calendar after their cards are gone.

