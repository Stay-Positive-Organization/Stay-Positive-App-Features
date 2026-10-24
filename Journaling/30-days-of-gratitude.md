# 30 Days of Gratitude

**Status:** Feature specification for implementation; not yet a shipped feature.  
**Location:** Journaling screen / Journal tab.  
**Platforms:** Shared product behavior for Android (Kotlin) and iOS.  
**Campaign:** Thanksgiving-season gratitude journey.  
**Tagline:** One day. One blessing. One thankful heart.

## Purpose

Offer a guided space to notice everyday blessings, reflect on faith and relationships, and build a personal collection of gratitude entries through 30 prompts. Supporting a regular journaling habit is a product hypothesis to validate after release.

This extends the existing [Journal specification](../Home/Journal.md). Regular free-writing remains available and keeps its existing editor behavior. Only gratitude entries receive an assigned prompt.

## First-version scope

- Featured card within the Journaling screen.
- Journey overview with 30 numbered days and saved progress.
- Prompt-based writing using the existing journal editor.
- Automatic draft saving, explicit completion, revisiting and editing.
- Entries accessible from both the journey and ordinary journal history.
- Gentle reflection and journey completion messages.

Suggested first-version defaults: self-paced progression, no calendar locking, and one journey per user. Users may start any time, miss days, and return without losing progress. These are journey days, not dates in November. No automatic reset or one-entry-per-calendar-day restriction.

Access entitlement and campaign-card visibility dates require product confirmation before implementation; do not infer a Premium restriction or an automatic seasonal expiry.

## User flow

1. Open the Journal tab.
2. Discover the 30 Days of Gratitude card.
3. Tap **Begin my journey** to open the introduction and day overview.
4. Open Day 1 and write a reflection.
5. Draft saves automatically; tap **Complete reflection** when ready.
6. See saved progress and return to the overview or Journal.
7. Return later through **Continue Day {n}**, reopening the next unfinished reflection.
8. Revisit or edit any completed reflection.
9. Complete all 30 reflections and open **Read my reflections**.

Opening the journey or editor alone does not complete a day. Existing users do not repeat account onboarding to start.

## Journaling entry card

Place the card in the Journal tab without replacing **New entry**, journal history, the privacy line, or bottom navigation. Final placement follows the Journaling design.

| State | Content | Action |
|---|---|---|
| Before starting | **30 Days of Gratitude** / One day. One blessing. One thankful heart. / Take a moment each day to notice the blessings in your life with a guided gratitude prompt. | Begin my journey |
| In progress | **Your gratitude journey** / {completedCount} of 30 reflections completed / Make a little space for gratitude today. | Continue Day {n} |
| All complete | **30 Days of Gratitude** / 30 of 30 reflections completed | Read my reflections |

The continue action opens the lowest-numbered unfinished day, restoring its draft if present. Progress is the count of distinct completed days, not the number of visits or saved drafts. Starting without completing a reflection shows 0 of 30.

## Journey overview

- Header: **30 Days of Gratitude**, back action.
- Introduction: **You don’t need perfect words or a perfect day. Begin with something small, and return whenever you’re ready.**
- Progress: **{completedCount} of 30 reflections completed**, with an accessible progress indicator.
- A scrollable grid or list of Day 1 through Day 30, in order.
- Each day has a visible text/icon state: **Not started**, **Draft**, or **Completed**.
- Recommended next day is visually indicated; no days are locked in this self-paced version.
- Selecting a day opens its assigned prompt and existing entry, if any.
- Completed entries remain readable and editable after the campaign ends.

Use state labels and icons in addition to color. Support screen readers, larger text, and small screens without clipping the days or controls.

## Guided journal editor

Reuse the existing journal editor and its privacy, optional mood, dictation, edit, and delete behavior.

| Element | Content / behavior |
|---|---|
| Journey label | Day {n} of 30 · Gratitude |
| Heading | Exact prompt for that day |
| Empty writing placeholder | Start wherever your heart leads… |
| Writing area | User’s private free-text reflection |
| Saving | Automatic draft saving with accurate saving/saved/error feedback |
| Primary action | Complete reflection |
| Completed-entry action | Save changes, preserving completion for a nonempty reflection |
| Exit | Return to journey or Journal with saved draft intact |

A whitespace-only response cannot complete a day. There is no minimum length beyond a nonempty reflection, and no requirement to answer in a particular way.

Do not report an entry as saved or a day as completed until the relevant write succeeds according to the existing journal persistence model. If saving fails, keep the text available, show a retry action, and preserve the last successfully saved state.

## Completion and return behavior

After a successful completion:

> Another blessing remembered.  
> Your Day {n} reflection has been saved.

Offer **Back to my journey**. Users can open another day from the overview if they choose; there is no countdown.

After all 30:

> **30 reflections. So much to be thankful for.**  
> You’ve made space to notice the blessings in your life. Revisit your reflections whenever you need a reminder of what matters.

Primary action: **Read my reflections**, opening the user's gratitude entries in day order.

Missed days do not reset progress or trigger guilt-based messaging. Do not add streak penalties, deadlines, or a restart that clears entries.

## Journal history integration

- Use the same entry from both the journey and normal Journal history; do not create duplicate copies.
- Label entries **30 Days of Gratitude · Day {n}**, retaining their saved date and optional mood.
- Store the assigned prompt with the entry so the question remains understandable when revisited.
- Reopening a day restores its associated draft or completed entry.
- Editing a nonempty completed reflection keeps the day completed and retains the original entry date.
- Deletion uses the existing confirmation flow. Deleting a completed gratitude entry changes that day to Not started and decreases progress.
- If all text is removed from a completed entry, explain that saving it empty removes that reflection and its completion, and use the existing delete confirmation rather than silently clearing it.
- Journey metadata must never recreate a deleted private reflection.
- Persist progress and drafts through navigation, app restarts, and normal account restoration supported by the existing Journal system.

## Prompt content

Keep stable day IDs independent of display wording. The original campaign prompts are preserved below.

| Day | Stable ID | Prompt |
|---|---|---|
| 1 | gratitude-01 | What are you most thankful for today? |
| 2 | gratitude-02 | Who makes your life brighter? |
| 3 | gratitude-03 | What simple comfort brings you joy? |
| 4 | gratitude-04 | What answered prayer are you grateful for? |
| 5 | gratitude-05 | What do you love most about your home? |
| 6 | gratitude-06 | Which friendship are you thankful for? |
| 7 | gratitude-07 | What challenge taught you a valuable lesson? |
| 8 | gratitude-08 | What family tradition means the most to you? |
| 9 | gratitude-09 | What about your body deserves appreciation? |
| 10 | gratitude-10 | What memory always makes you smile? |
| 11 | gratitude-11 | Who believed in you when you needed it most? |
| 12 | gratitude-12 | What small win are you celebrating? |
| 13 | gratitude-13 | What part of nature fills you with wonder? |
| 14 | gratitude-14 | What act of kindness have you never forgotten? |
| 15 | gratitude-15 | What do you appreciate about yourself? |
| 16 | gratitude-16 | What opportunity are you thankful you took? |
| 17 | gratitude-17 | What song brings you comfort or joy? |
| 18 | gratitude-18 | Who makes you feel loved and accepted? |
| 19 | gratitude-19 | What everyday convenience do you often overlook? |
| 20 | gratitude-20 | What has this year taught you to appreciate? |
| 21 | gratitude-21 | What meal reminds you of love? |
| 22 | gratitude-22 | Who deserves a heartfelt “thank you” today? |
| 23 | gratitude-23 | What moment of peace are you grateful for? |
| 24 | gratitude-24 | What is something you once wished for that you have now? |
| 25 | gratitude-25 | What makes you thankful for your community? |
| 26 | gratitude-26 | How has your faith carried you this year? |
| 27 | gratitude-27 | What made you laugh recently? |
| 28 | gratitude-28 | What Thanksgiving blessing will you celebrate today? |
| 29 | gratitude-29 | How can you turn your gratitude into kindness? |
| 30 | gratitude-30 | After these 30 days, what do you notice and appreciate more? |

**Day 28 wording proposal:** For a journey users can start anytime, consider **“What blessing are you especially thankful for in this season?”** Confirm this copy change before replacing the original Thanksgiving prompt. Day numbers must not imply a fixed Thanksgiving date.

## Visual direction

Use the supplied 30 Days of Gratitude campaign artwork as the visual reference: cream background, autumn leaves, warm brown typography, and restrained sage accents. Keep decorative leaves outside the writing area.

- Headings: Cormorant Garamond.
- Supporting text and controls: Montserrat.
- Maintain readable contrast, accessible controls, and existing Stay Positive navigation.
- Keep the tone calm, welcoming, and reflective.
- Promotional copy about sharing gratitude does not authorize publishing private journal entries.

## Privacy

Inherit the existing Journal privacy rules:
- Entries are accessible only to their owner.
- Never include reflection text in Home previews, notifications, analytics, or logs.
- Do not use entries for personalization without explicit consent.
- Dictation follows the existing behavior; do not retain audio.
- Sharing is outside the first version. If introduced later, require a preview and explicit selection of what to share; never publish entries automatically.

## Suggested persistence contract

Adapt to the existing Journal schema rather than creating a separate store of reflection text.

- Journey identifier/version: `gratitude-30-v1`.
- Journey start timestamp.
- Existing journal entry linked to journey ID and stable day ID.
- Prompt snapshot, entry body, optional mood, original creation timestamp, update timestamp.
- Entry state: draft or completed, with completion timestamp where applicable.
- Enforce at most one active entry per user/journey/day.
- Derive completed count from distinct completed entries or keep cached progress consistent with those entries.
- Repeated completion taps and retries must not create duplicate entries or increment progress twice.
- Follow existing account authorization and synchronization behavior.

## Acceptance criteria

- [ ] The featured card appears within Journaling and preserves normal free-writing and entry history.
- [ ] A new journey shows 0 of 30 completed and the correct Day 1 prompt.
- [ ] All 30 prompts are mapped to the correct stable day IDs.
- [ ] Each day shows its actual Not started, Draft, or Completed state.
- [ ] Draft text survives leaving and reopening the editor after a successful save.
- [ ] Empty/whitespace-only reflections cannot complete a day.
- [ ] Completing a reflection successfully increases progress exactly once.
- [ ] Continue opens the lowest-numbered unfinished day and restores its draft.
- [ ] Missed days and app restarts do not reset progress.
- [ ] The journey and Journal history open the same saved entry.
- [ ] Editing a completed entry preserves completion and its original date.
- [ ] Confirmed deletion removes the entry and updates journey progress.
- [ ] A save failure retains recoverable text and does not falsely confirm completion.
- [ ] All 30 completed days show the final message and access to reflections in day order.
- [ ] Another account cannot read the user's reflections or progress.
- [ ] Reflection text is excluded from analytics, logs, notifications, and public previews.
- [ ] Large text, screen readers, and small-screen scrolling remain usable.

## Product decisions still to confirm

- Free/Premium entitlement.
- Dates, if any, for promoting or hiding the entry card; saved reflections must remain accessible.
- Original Thanksgiving Day 28 wording versus the proposed season-neutral wording.
- Any reminders or sharing beyond the first-version scope.
