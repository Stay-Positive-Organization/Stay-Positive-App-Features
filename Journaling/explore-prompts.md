# Explore Prompts

**Status:** Feature specification for implementation; not yet a shipped feature.  
**Location:** Journaling screen / Journal tab.  
**Platforms:** Shared product behavior for Android (Kotlin) and iOS.  
**Plans:** Free and Premium, no limits (same as the Journal tab).

## Purpose

Give people an easy way to find something to write about whenever they open Journaling. A person can explore a random prompt, choose a topic, or write freely. It should feel like an invitation to express themselves, with room for everyday life, travel, curiosity, faith and deeper reflection.

Sometimes people want to journal but don't know where to begin. Other times they just want to capture a trip, describe a moment or explore an idea. Prompts help them start without making every entry feel like an assignment or requiring a particular emotional or spiritual topic.

This extends the [Journal specification](../Home/Journal.md). Regular free-writing keeps its existing no-prompt editor. Only entries started from Explore prompts carry a prompt.

**Source of truth for visuals:** the Figma file, [Journaling V3](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=3130-723). This doc covers behavior, copy and product decisions; fonts, sizes and spacing live in Figma.

## User story

As someone using Stay Positive, I want to discover a prompt that matches what I feel like writing about, so I can start a personal journal entry without needing to think of a topic first.

> I open Journaling and feel like writing about travel. I choose **Travel and adventure**, see a question about a place I would love to visit, and tap **Write about this**. If that question doesn't interest me, I tap **Another prompt**.

Also:

- **Surprise me.** I don't know what I want to write about, so I get a question from the whole collection.
- **Just write.** I know what I want to say, so I start a blank entry without going through prompts.
- **Look back.** When I reread an entry later, I see the prompt that started it.

## First-version scope

- An optional **Explore prompts** entry point on the Journaling screen.
- A prompt browser with one prompt at a time and unlimited skipping.
- **Surprise me** across the full collection and an optional topic filter.
- A direct path from a prompt into the existing journal editor, with the prompt attached.
- A blank-entry option that stays easy to find.
- Private entries saved in the existing journal, with their prompt retained.

"Random" means choosing from a prepared, reviewed collection. Live AI-generated prompts are outside the first version.

Explore prompts sits alongside the existing guided prompts and structured activities, including [30 Days of Gratitude](30-days-of-gratitude.md). There's no enrollment, sequence, progress count or completion state.

## Flow

```text
Journal tab
├── New entry ───────────────────────────────► Journal editor (blank, as today)
└── Explore prompts ─► Prompt browser
                       ├── Another prompt / Surprise me / topic ─┐
                       │◄────────────────────────────────────────┘  (loop, no limit)
                       ├── Write about this ─► Journal editor (prompt attached) ─► Done ─► Saved entry
                       └── Write without a prompt ─► Journal editor (blank)
```

Leaving the browser, or leaving the editor without typing, saves nothing.

## Journaling entry point

**Explore prompts** is a card on the Journal tab, under **New entry** and beside the **Talk it through** card, above the 30 Days of Gratitude card. New entry, journal history, the privacy line and bottom navigation stay as they are. See [Journal tab](../Home/Journal.md#journal-tab).

| Element | Copy |
|---|---|
| Title | Explore prompts |
| Supporting line | Not sure what to write? Find a question to start with. |

## Prompt browser

| Element | Content / behavior |
|---|---|
| Header | **Explore prompts**, back action |
| Topic filter | **All** plus one chip per active topic, in display order. **All** is selected on open. |
| Prompt card | Topic label above the prompt text. One prompt at a time. |
| Primary action | **Write about this** |
| Secondary actions | **Another prompt** and **Surprise me** |
| Blank option | **Write without a prompt**, visible without scrolling |

Behavior:

- Opening the browser shows a prompt immediately, drawn from the whole collection.
- **Another prompt** shows a different prompt from the current pool (whole collection, or the selected topic). There's no limit on skips.
- No prompt repeats until every prompt in the current pool has been shown; then the pool reshuffles. The seen list lasts for the visit and isn't synced.
- **Surprise me** clears any topic and shows a prompt from the whole collection.
- Selecting a topic shows a prompt from that topic right away. Selecting **All** clears the filter.
- The browser opens on **All** each time; it doesn't remember the last topic.
- Changing prompts uses a simple fade that respects reduced-motion settings.

## Writing

Reuse the existing journal editor and its privacy, optional mood, dictation, draft, edit and delete behavior.

| Element | Content / behavior |
|---|---|
| Prompt | Shown above the writing area with its topic label |
| Remove prompt | A small remove control on the prompt. Removing it turns the draft into a regular entry. |
| Empty writing placeholder | Start wherever your heart leads… |
| Saving | Same as the existing editor: draft saves automatically; Done saves; empty entries are discarded |

## Journal history

- Prompted entries appear in normal Journal history, grouped by month like any entry.
- The entry view shows the saved prompt above the text.
- Editing keeps the prompt and the original date. Deleting uses the existing confirmation flow.
- A retired or reworded prompt never changes an entry that already used it (the entry keeps its own snapshot).

## Prompt collection

Prompts come from one shared, reviewed collection. Reset Routine's prompt library ("Personalize Your Journal") reads from the same collection, so a prompt is written and reviewed once.

- **Launch:** 5 topics × 20 prompts = 100. The full list, with stable IDs, is in [prompt-collection.md](prompt-collection.md).
- **Growth:** the collection grows over time. New prompts and new topics are added in Firestore without an app update; the app shows any active topic that has active prompts.
- **Faith:** a dedicated Faith topic, plus a light touch elsewhere (about 3 of every 20 prompts in other topics carry a faith framing).
- **Review:** every prompt is written by the Stay Positive team and approved by Evelise (founder) before it goes live. No prompt is generated on demand.
- **Retiring:** set `active: false`. A retired prompt disappears from the browser and from new Reset picks, but stays on entries and existing Reset lists that already use it.

Writing guidelines for new prompts:

- One open question per prompt, answerable in a sentence or a page.
- Warm and invitational; no "you should" framing.
- Neutral about life circumstances: don't assume a spouse, children, a job, a home or the ability to travel.
- Deeper reflection stays gentle. Don't ask people to relive trauma, loss or crisis.
- Keep stable IDs independent of wording, so copy edits never break entries.

## Edge cases

| Situation | Behavior |
|---|---|
| First open, offline, nothing cached | "Prompts need a connection the first time." with **Write without a prompt** and **Try again** |
| Collection fails to load | Same as above |
| Selected topic has one active prompt | **Another prompt** keeps showing it; **Surprise me** still works |
| Topic has no active prompts | The topic chip isn't shown |
| Every prompt in the pool seen | Reshuffle silently and continue |
| Prompt retired after an entry used it | Entry still shows its saved prompt text |
| App closed mid-entry | Existing draft behavior; the prompt stays attached to the draft |

No state in this feature blocks writing: every failure still offers a blank entry.

## Streaks

Opening Explore prompts or saving a prompted entry counts toward the streak like any other journal activity (see [Streaks](../Home/Streaks.md)).

## Accessibility

- When a new prompt appears, screen readers announce it with its topic (polite live region).
- Topic chips expose their selected state. Every control has a label and a touch target of at least 48 dp / 44 pt.
- Prompt text supports system font scaling without truncation; the card grows and the page scrolls.
- Meets WCAG 2.1 AA contrast.

## Privacy

Inherits the [Journal privacy rules](../Home/Privacy%20and%20Safety.md#data-rules):

- Entries are readable only by their owner.
- Entry text never appears on Home, in notifications, in analytics or in logs, and is never used for personalization.
- Analytics record prompt IDs and actions only.

## Suggested persistence contract

Adapt to the existing Journal schema rather than creating a separate store of entry text.

**Prompt** — `journalPrompts/{promptId}`, read-only to clients:

| Field | Type | Notes |
|---|---|---|
| `id` | string | Stable ID, e.g. `travel-04` |
| `text` | string | The question shown |
| `topicId` | string | One topic per prompt |
| `active` | boolean | Inactive prompts are hidden |
| `addedAt` | timestamp | For review tooling |

**Topic** — `journalPromptTopics/{topicId}`: `id`, `name`, `order`, `active`.

**Journal entry** — existing fields plus:

| Field | Type | Notes |
|---|---|---|
| `promptId` | string, optional | Set when the entry started from a prompt |
| `promptText` | string, optional | Snapshot of the text when writing started |
| `promptTopicId` | string, optional | Snapshot of the topic |
| `promptSource` | string, optional | `explore` for this feature |

The app caches the collection on first open and refreshes it in the background, so browsing works offline and skipping never waits on the network. Random selection and the no-repeat order run on the device.

## Analytics

Success means more people start and save entries, not more prompts viewed.

| Event | Properties |
|---|---|
| `explore_prompts_opened` | — |
| `prompt_shown` | `promptId`, `topicId`, `trigger` (`open`, `another`, `surprise`, `topic`) |
| `prompt_topic_selected` | `topicId` |
| `prompt_write_tapped` | `promptId`, `skipsBeforeWrite` |
| `prompt_entry_saved` | `promptId`, `topicId`, `promptRemoved` |
| `explore_blank_entry` | `skipsBeforeExit` |

Measures to watch: share of Explore visits that end in a saved entry; median skips before **Write about this**; prompts with many views and few writes (candidates to rewrite or retire).

## Acceptance criteria

- [ ] Explore prompts appears on the Journaling screen without displacing New entry, history or the gratitude card.
- [ ] Opening the browser shows one prompt from the whole collection with its topic label.
- [ ] Another prompt never repeats a prompt until the current pool is exhausted, then continues.
- [ ] Selecting a topic limits prompts to that topic; All and Surprise me return to the whole collection.
- [ ] Write about this opens the existing editor with the prompt shown and removable.
- [ ] Write without a prompt opens a blank entry from the browser.
- [ ] A saved prompted entry appears in Journal history and shows its prompt when reopened.
- [ ] Rewording or retiring a prompt doesn't change entries that used it.
- [ ] Leaving the browser or an empty editor saves nothing.
- [ ] A topic or prompt added in Firestore appears without an app update; inactive ones don't appear.
- [ ] Reset Routine's prompt library and Explore prompts show the same collection.
- [ ] First open offline shows the connection message and still allows a blank entry.
- [ ] Opening Explore or saving a prompted entry counts toward the streak.
- [ ] Screen readers announce each new prompt; large text doesn't truncate prompts.
- [ ] Entry text is excluded from analytics, logs, notifications and Home.

## Decisions

Settled:

- One shared, reviewed collection for Explore prompts and Reset's prompt library; it grows over time.
- Free and Premium, no limits.
- Five launch topics, 20 prompts each.
- A Faith topic plus a light faith touch in other topics.
- The browser always opens on All.
- Entry point: a card beside Talk it through under New entry (Figma › Journaling V3 › Journal tab).
- Evelise approves every new or reworded prompt before it goes live.

No open decisions.

## Phase 2

- Favorite prompts and a saved-prompts list.
- Add a browsed prompt to the Reset journal prompt list.
- Ask Alex for a prompt (Premium), held to the same review rules for tone and safety.
- Mood-aware topic suggestions after a check-in.
- Seasonal collections (Advent, Lent, New Year).

## Related

- [Talk it through](talk-it-through.md) — Premium conversational journaling that can start from a prompt.
- [30 Days of Gratitude](30-days-of-gratitude.md)
- [Journal](../Home/Journal.md)
