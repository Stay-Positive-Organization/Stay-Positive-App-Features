# 25 Days of Christmas (Bible Study)

**Status:** Feature specification for implementation; not yet a shipped feature.  
**Location:** Prayer screen (where Read the Bible and Bible notes live).  
**Platforms:** Shared product behavior for Android (Kotlin) and iOS.  
**Campaign:** December / Christmas season.  
**Card subtitle:** Meet Jesus through Scripture, one day at a time.  
**Translation:** references are NIV; Read passage opens the existing Bible reader in the user's current version.

## Purpose

Help people explore the story and meaning of Jesus' coming through one short Bible study a day from December 1 to 25. The study moves from the promises about the Messiah to Jesus' birth and the response of the people who encountered Him. Each day has a passage, a reflection question, and an optional private reflection.

This is a **Bible Study** experience, separate from [December Reflections](../Journaling/december-reflections.md) in Journal. The two never share progress, completion, or entries. A study reflection appears in Journal only if the person chooses **Copy to Journal**.

The app has no separate Bible Study screen yet, so the study card lives on the Prayer screen, next to Read the Bible.

## First-version scope

- A **25 Days of Christmas** card on the Prayer screen (Dec 1–31).
- An overview listing all 25 days and their state.
- A daily study screen: passage reference, **Read passage**, reflection question, optional reflection, **Save reflection**, **Mark day complete**.
- A study-complete screen and a **My reflections** screen.
- Optional **Copy to Journal** for a saved reflection.

Self-paced by design:
- No locked days. Day 20 can be opened on December 3.
- No streak, deadline, countdown, or reset. Missing a day has no consequence.
- Days can be completed in any order, revisited, and edited.
- Writing is optional. A day can be completed without a reflection.

## User flow

1. Open the Prayer screen.
2. See the **25 Days of Christmas** card.
3. Tap **Start study** (or **Continue Day {n}**) to open that day, or **See all 25 days** to pick any day.
4. Tap **Read passage** to read in the Bible reader, then come back to the same day.
5. Optionally write a reflection. It autosaves; **Save reflection** saves right away.
6. Tap **Mark day complete**. Progress updates.
7. Return later to continue, open any other day, or edit a saved reflection.
8. When the 25th day is completed, see the study-complete screen.

## Prayer screen card

Sits on the Prayer screen under the greeting and above **Scripture of the day**. The greeting, Scripture of the day, Today's prayer focus, **Read the Bible**, the Free ad banner, and bottom navigation stay unchanged.

| State | Content | Primary action | Secondary action |
|---|---|---|---|
| Not started | **25 Days of Christmas** / Meet Jesus through Scripture, one day at a time. / 0 of 25 days complete | Start study | See all 25 days |
| In progress | **25 Days of Christmas** / same subtitle / {completedCount} of 25 days complete | Continue Day {n} | See all 25 days |
| All complete | **25 Days of Christmas** / same subtitle / 25 of 25 days complete | Review study | See all 25 days |

- **Start study** opens Day 1.
- **Continue Day {n}** opens the lowest-numbered day that isn't complete.
- **Review study** opens the overview (All 25 days).
- "In progress" starts once any day is completed or any reflection is saved.
- Progress counts distinct completed days only. Opening a day, reading the passage, or saving a reflection does not count.
- Progress uses a thin bar plus the text count, so it doesn't rely on color alone.
- "See all 25 days" is a text link, not a second button.

## All 25 days (overview)

Opened from **See all 25 days**, **Review study**, or the back action on a day.

- Header: **25 Days of Christmas**, back action.
- Intro: **From the promise of a Savior to His birth. Open any day, any time.**
- Progress card: **{completedCount} of 25 days complete**, progress bar, and the same primary action as the card (Continue Day {n} / Review study).
- **All 25 days**, grouped under the five outline sections (small labels, e.g. DAYS 1–4 · THE PROMISE OF THE MESSIAH).
- Each row shows the day number, date (e.g. "Mon, Dec 7"), title, passage reference, and state: **Not started**, **In progress** (reflection saved, not complete), or **Completed**. State is text plus icon, not color alone.
- Today's day (Dec 1–25) shows a "Today" label. This is a pointer, not a restriction.
- Tapping any row opens that day.

## Daily study screen

| Element | Content / behavior |
|---|---|
| Top bar | Back action; save status (**Saving…** / **Saved just now** / empty when nothing is written) |
| Day label | **Day {n} · {Weekday}, December {n}** |
| Title | The day's title (heading style) |
| Reading | **READING** / the passage reference, with a **Read passage** button |
| Reflect | **REFLECT** / the day's reflection question |
| Reflection field | Optional. Placeholder: **Write your reflection (optional)** |
| Privacy line | 🔒 **Private to you. Saved with this day, not in Journal unless you copy it.** |
| Actions (not complete) | **Save reflection** (outline; disabled with no text) and **Mark day complete** (primary) |
| Actions (complete) | **✓ Day {n} complete** badge, **Go to Day {n+1}** (primary; on Day 25 the badge only), **Copy to Journal**, **Mark as not complete** |

Rules:
- **Read passage** opens the existing Bible reader at the passage's book, chapter, and first verse, exactly as the reader works today (the user's current version and saved position behavior). Back returns to the same day with any typed text intact.
- The reflection autosaves while typing (debounced) and on leaving the screen. **Save reflection** saves immediately. The top bar shows the saved state.
- Whitespace-only text is not saved as a reflection.
- **Mark day complete** works with or without a reflection, and saves any typed text first.
- A completed day stays editable. Editing doesn't change its completion.
- **Mark as not complete** returns the day to In progress (or Not started if there's no reflection), lowers progress, and keeps the reflection.
- **Copy to Journal** appears once a reflection is saved. It creates one regular Journal entry with the day's title, reference, question, and reflection, labeled **25 DAYS OF CHRISTMAS · DAY {n}**, then shows "Copied to Journal" with a View action. The link reads **Copied to Journal** until the reflection changes. The copy is independent: later edits on either side don't sync.
- Don't confirm a save until the write succeeds. On failure, keep the text, show a retry, and leave the day's state unchanged.

## Study complete

Shown right after the 25th distinct day is marked complete (whichever day that is):

> **You finished 25 Days of Christmas.**  
> The Savior is born. Carry the good news with you beyond Christmas.

- Progress: **25 of 25 days complete** (full bar).
- Primary: **Review my reflections** (opens My reflections).
- Secondary: **Revisit the study** (opens the overview).

No confetti, countdowns, or guilt-based messaging for missed days, ever.

## My reflections

- Header: **My reflections**, back action.
- Intro: **Only you can see these. They stay with the study, separate from Journal.**
- One card per day with a saved reflection, Day 25 first: day and date, title · reference, and the reflection (preview).
- Tapping a card opens that day.
- Empty state (no reflections yet): **Your reflections will show here when you write one.**

## Card timing

- The card shows on the Prayer screen from **December 1 through December 31** (user's local time) and leaves on **January 1**.
- Before December 1, nothing appears in the app. (Pre-launch social posts link to the waitlist.)
- All 25 days are open from December 1. People can start late or finish after December 25 until the card leaves.
- Progress and reflections are kept after January 1.

## Access

Open to everyone, Free and Premium. No Premium badge.

## Study content

Use these titles, readings, and questions exactly. Day IDs are stable and independent of wording. All references are NIV.

**Outline sections**
- Days 1–4: The promise of the Messiah
- Days 5–10: The announcement and Mary's response
- Days 11–15: Faithfulness, preparation, and the name of Jesus
- Days 16–20: Immanuel, the journey to Bethlehem, and the angels' announcement
- Days 21–25: The witnesses, worship, and the good news of Jesus' birth

| Day | Stable ID | Title | Reading | Reflection question |
|---|---|---|---|---|
| 1 | christmas-01 | The first promise | Genesis 3:15 | What promise did God give about the coming Savior? |
| 2 | christmas-02 | God with us | Isaiah 7:14 | What does "Immanuel, God with us," mean to you? |
| 3 | christmas-03 | The promised King | Isaiah 9:2–7 | Which name of Jesus speaks to your heart today? |
| 4 | christmas-04 | Bethlehem | Micah 5:2 | What does Bethlehem teach you about God's plans? |
| 5 | christmas-05 | A promise remembered | Luke 1:5–17 | How can you prepare your heart for Jesus? |
| 6 | christmas-06 | The announcement | Luke 1:26–33 | Which part of the angel's message gives you hope? |
| 7 | christmas-07 | Mary's trust | Luke 1:34–38 | What does Mary's response teach you about trust? |
| 8 | christmas-08 | Encouraging faith | Luke 1:39–45 | Who encourages your faith, and how can you encourage them? |
| 9 | christmas-09 | Mary's praise | Luke 1:46–49 | What is one reason you can praise God today? |
| 10 | christmas-10 | God's mercy | Luke 1:50–55 | Where do you see God's mercy in your life? |
| 11 | christmas-11 | John is born | Luke 1:57–66 | What does John's birth show you about God's promises? |
| 12 | christmas-12 | God's faithfulness | Luke 1:67–75 | What do you want to remember about God's faithfulness? |
| 13 | christmas-13 | Preparing the way | Luke 1:76–80 | How can you make room for Jesus in your heart? |
| 14 | christmas-14 | Joseph's compassion | Matthew 1:18–19 | What does Joseph's response show you about compassion? |
| 15 | christmas-15 | Jesus saves | Matthew 1:20–21 | What does it mean to you that Jesus came to save? |
| 16 | christmas-16 | God is with us | Matthew 1:22–25 | How does knowing God is with you change a season of waiting? |
| 17 | christmas-17 | The journey to Bethlehem | Luke 2:1–5 | Where do you see God in the middle of ordinary plans? |
| 18 | christmas-18 | Jesus shares our humanity | Hebrews 2:14–18 | How does Jesus sharing our humanity comfort you? |
| 19 | christmas-19 | Jesus is born | Luke 2:6–7 | What does Jesus' humble birth reveal about God's heart? |
| 20 | christmas-20 | Good news for all | Luke 2:8–14 | What part of the angels' good news do you need today? |
| 21 | christmas-21 | The shepherds respond | Luke 2:15–20 | What can you learn from the shepherds' response? |
| 22 | christmas-22 | Seeking Jesus | Matthew 2:1–2 | What helps you keep seeking Jesus? |
| 23 | christmas-23 | Jesus the King | Matthew 2:3–6 | What does this passage reveal about Jesus as King? |
| 24 | christmas-24 | Worship and gifts | Matthew 2:7–11 | What can you offer Jesus in worship? |
| 25 | christmas-25 | Carrying the good news | Luke 2:10–20 | What good news about Jesus will you carry beyond Christmas? |

The email version uses the same day, reading, and question for each day.

## Visual direction

Match the Prayer screen and December Reflections so the card feels native, not promotional.

- Palette: warm cream background (`warmWhite`), soft sage card (#E7EFEB) so it doesn't read as the peach December Reflections card, `forest` for headings and the primary button, gold (#B8976A) for the progress fill and small labels, sage (#8FB0A1) for decoration only.
- Sage and gold are decoration and labels only; never body text on light backgrounds (see [design tokens](../Home/design-tokens.md)).
- Typography per app standard: Alegreya for titles, Montserrat for body and supporting text, Cormorant Garamond Bold on buttons.
- Small seasonal sprig and star detail, kept outside the writing area.

Support large text, screen readers (progress announced as "{n} of 25 days complete"), and small screens without clipping.

## Privacy

- Reflections are visible only to their owner.
- Reflection text never appears in Home previews, notifications, analytics, or logs.
- No use for personalization without explicit consent.
- No sharing in this version. Copy to Journal is the only way a reflection leaves the study.

## Suggested data structure

**Study (bundled content):** `id` (`christmas-2026`), `title`, `description`, `startDate` (Dec 1), `endDate` (Dec 25), `cardEndDate` (Dec 31), `totalDays` (25), and the 25 days: `dayNumber`, `dayId`, `title`, `theme` (outline section), `passageReference`, `reflectionPrompt`.

**Per user, per day** (only for days the user has touched): `dayId`, `reflectionText`, `isComplete`, `completedAt`, `updatedAt`, `copiedToJournalAt` (optional).

- Stored separately from Journal entries and December Reflections.
- At most one record per user/study/day.
- Completed count is derived from distinct completed days.
- Repeated taps and retries never duplicate a record or double-count progress.
- Progress and reflections survive navigation, app restarts, and reinstall/sign-in on another device.

## Design

Figma › Version 3.0 › [25 Days of Christmas](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=3331-1193)
- [Prayer screen, card not started](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=3332-1501) · [card in progress](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=3332-1570) · [Card component, 3 states](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=3331-1196)
- [All 25 days](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=3332-1640) · [Day row component](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=3331-1262)
- [Day, not started](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=3333-1467) · [Day, reflection written](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=3333-1551) · [Day, completed](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=3333-1635)
- [Study complete](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=3333-1720) · [My reflections](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=3333-1779)

## Acceptance criteria

- [ ] The card appears on the Prayer screen from Dec 1 through Dec 31 (local time) and is gone on Jan 1; the rest of the Prayer screen is unchanged.
- [ ] Free and Premium users both see the card, with no Premium badge.
- [ ] A new user sees "0 of 25 days complete" and **Start study**, which opens Day 1.
- [ ] After any progress, the card shows **Continue Day {n}** for the lowest-numbered incomplete day.
- [ ] With all 25 complete, the card shows **Review study**.
- [ ] **See all 25 days** lists Day 1–25 with dates, titles, references, outline sections, and correct states.
- [ ] Every day can be opened at any time; no day is locked.
- [ ] All titles, readings, and questions match the table above and map to the correct stable IDs.
- [ ] **Read passage** opens the existing Bible reader at the right book, chapter, and verse; back returns to the same day.
- [ ] Reflections autosave and show a saved state; **Save reflection** is disabled with no text.
- [ ] A day can be completed without a reflection, and progress increases exactly once.
- [ ] Completed days stay editable; **Mark as not complete** lowers progress and keeps the reflection.
- [ ] Reflections never appear in Journal unless the user taps **Copy to Journal**, which creates exactly one entry per tap-after-change.
- [ ] Completing the 25th distinct day shows the study-complete screen with **Review my reflections** and **Revisit the study**.
- [ ] My reflections lists every day with a saved reflection.
- [ ] Progress and reflections survive leaving the screen, restarting the app, and signing in on another device.
- [ ] A failed save keeps the text and doesn't show a false confirmation.
- [ ] No streak, deadline, lock, or reset exists in this feature.
- [ ] 25 Days of Christmas and December Reflections progress are fully independent.
- [ ] Another account can't read the person's reflections or progress.
- [ ] Reflection text is excluded from analytics, logs, notifications, and previews.
- [ ] Large text, screen readers, and small screens remain usable.

## Decisions

- **Placement:** Prayer screen, next to Read the Bible (the app has no separate Bible Study screen yet). Nov 2026.
- **Access:** open to everyone, Free and Premium. Nov 2026.
- **Card timing:** December 1 through December 31; leaves on January 1. Nov 2026.
- **Read passage:** opens the Bible reader the app already has, with no study-specific version or mode. Nov 2026.
- **Journal:** reflections stay in the study; Copy to Journal is opt-in.
