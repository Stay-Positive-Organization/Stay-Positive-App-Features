# Talk It Through

**Status:** Feature specification for implementation; not yet a shipped feature.  
**Location:** Journaling screen / Journal tab.  
**Platforms:** Shared product behavior for Android (Kotlin) and iOS.  
**Plans:** Premium only. Free users who tap it see the full upgrade screen.

## Purpose

Let people journal the way they would talk to someone who listens: they say what's on their heart, a gentle question comes back, and they keep going. Some people find it easier to open up in a conversation than on a blank page.

Two listeners are available:

- **Guided** — pre-written, reviewed follow-up questions. No AI; the text stays in the journal.
- **With Alex** — Alex responds as an attentive listener. Needs a separate consent because the text is sent to an AI service.

People can type or speak in both. The finished conversation is saved as one private journal entry.

**This is not therapy.** The product name and copy never call it therapy, counseling or treatment, and the listener never diagnoses or gives clinical advice. "Therapy" is the internal inspiration only.

This extends the [Journal specification](../Home/Journal.md) and reuses its storage, privacy, edit and delete behavior. Visuals live in the Figma file, [Journaling V3](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=3130-723); this doc covers behavior and copy.

## How it differs from Talk with Alex

Both are Premium and both can involve Alex, so each has a clear job. Talk with Alex is a companion you come back to; Talk it through is a sitting you finish and keep.

| | Talk with Alex | Talk it through (With Alex) |
|---|---|---|
| Lives in | Explore more on Home, Alex pick | Journal tab |
| Alex's role | Companion: encouragement, ideas, suggestions | Listener: reflects back, asks one question, no advice |
| Reply style | Conversational, with quick-reply chips | Under 60 words, at most one question, no chips |
| Conversation | One ongoing thread that persists | A session with a start and an end |
| Result | Stays in the Alex chat | Saved as a private journal entry, or discarded |
| Context Alex sees | The ongoing thread | Only the current session |
| Without AI | Not available | Guided listener |

Each points to the other (see [Cross-links](#cross-links)).

## User story

As a Premium member, when I have something on my mind, I want to talk it through as if someone were listening and asking me good questions, so I can understand what I feel without staring at a blank page.

> It's been a heavy week. I open Journal, tap **Talk it through**, and choose **Guided**. It asks "What's on your heart today?" I tap the mic and talk for a minute. It asks what happened next, then how that felt. Ten minutes later I tap **I'm done**, save it, and it's in my journal like any entry.

## First-version scope

- A **Talk it through** entry on the Journaling screen (Premium).
- Mode choice at the start of each session: **Guided** or **With Alex**.
- A conversation page: the person writes or speaks; the listener replies with one short question or reflection.
- Voice input with on-device speech-to-text, and an optional **Read replies aloud** setting.
- Save the conversation as one private journal entry, or discard it.
- Start from an [Explore prompts](explore-prompts.md) prompt as the opening question.
- A visible not-therapy notice and crisis support in both modes.

Out of the first version: switching mode mid-session, Alex using past entries or check-ins as context, summaries of a session, scheduled sessions or reminders, and talking to a named persona other than Alex.

## Flow

```text
Journal tab
└── Talk it through (Premium; Free → upgrade screen)
      └── Choose a listener
            ├── Guided ───────────────────────────────┐
            └── With Alex ─► Alex consent (first time) ┤
                                                       ▼
                                             Conversation page
                                     you write/speak ⇄ listener replies
                                                       │
                                                  I'm done
                                                       ▼
                                     Save to journal  /  Discard
```

From Explore prompts, Premium members see a **Talk it through** action on the prompt card; it skips straight to choosing a listener, with the prompt as the opening question.

## Journaling entry point

| Element | Copy |
|---|---|
| Placement | Card on the Journal tab, beside Explore prompts, under New entry |
| Title | Talk it through |
| Supporting line (Premium) | Say what's on your heart. A gentle question comes back. |
| Supporting line (Free) | Premium: say what's on your heart. A gentle question comes back. |
| Badge (Free only) | 🔒 PREMIUM, gold, top-right of the card. Tapping the card opens the full upgrade screen. Premium members see no badge. |

## Choose a listener

| Option | Copy |
|---|---|
| Guided | **Guided** · Thoughtful questions to help you keep going. Everything stays in your journal. |
| With Alex | **With Alex** · Alex listens and responds to what you share. |

The last choice is pre-selected next time. Both lead to the same conversation page.

Under the options, a quiet link: "Looking for encouragement or ideas? **Talk with Alex**", opening Talk with Alex.

## Alex consent

Shown the first time someone chooses **With Alex**, and again only if they turned it off. This consent is separate from personalization consent.

> **Talk it through with Alex**
>
> To respond, Alex needs to read what you share in this conversation.
>
> - Your words are sent to our AI service only to write Alex's replies.
> - They're never used for personalization, ads or analytics.
> - The conversation is saved only in your private journal.
>
> Alex is an AI companion, not a counselor.
>
> **Continue with Alex** · **Use Guided instead**

The choice is remembered per account and can be changed in Settings › Privacy (**Let Alex read Talk it through conversations**). Turning it off takes effect for the next session.

## Conversation page

| Element | Content / behavior |
|---|---|
| Header | **Talk it through**, listener label (Guided or Alex), **I'm done** |
| Notice | Pinned, collapsible after first view: "A private space to talk things through. It isn't therapy or a substitute for professional care." + **Find a crisis line in your country** |
| Opening question | "What's on your heart today?", or the Explore prompt if started from one |
| Composer | Text field, mic, Send |
| Listener reply | One short question or reflection per message, shown as a bubble |
| Skip | **Ask me something else** under the latest listener reply |

Behavior:

- The person sends a message; the listener replies once. The listener never sends two replies in a row or starts a conversation on its own.
- Messages can be edited until the next reply arrives; after that they're edited in the saved entry.
- There's no minimum length or number of turns. **I'm done** is always available.
- The draft saves automatically after each message, so closing the app doesn't lose it.

### Guided listener

Replies come from the curated follow-up set below. No text leaves the device for this.

- Follow-ups move through stages in order: **Explore → Feelings → Meaning → Next step → Close**. Each message moves one stage forward.
- **Ask me something else** gives another follow-up from the same stage.
- No follow-up repeats within a session. After Close, the listener cycles back to Explore if the person keeps going.
- A faith follow-up appears in the Meaning stage about one session in three, and only once per session.

### Alex listener

Uses the same AI service as [Talk with Alex](../Home/Pick%20destinations.md#3-talk-with-alex), with its own instructions so it behaves as a listener rather than a companion. Alex's instructions for this mode:

- Listen first. Reply with one short reflection and at most one question, under 60 words.
- Mirror the person's words; don't rush to fix, advise or quote Scripture unless they bring up faith.
- Never diagnose, label a condition, or suggest medication or treatment.
- Never claim to be a person or a therapist.
- Only this session's messages are sent as context. No past entries, check-ins or other conversations.
- If the service fails, show "Alex couldn't reply just now." with **Try again** and **Continue with Guided**, which hands the session to the Guided listener.

#### Daily limit

- 50 Alex replies per member per day, resetting at midnight local time.
- Failed requests and fixed safety messages don't count.
- When the limit is reached, show "You've reached today's replies from Alex. You can keep going with Guided, or come back tomorrow." with **Continue with Guided**. The session and its messages stay intact.
- Starting a new session after the limit is reached offers Guided only, with the same line under the With Alex option.

### Voice

- The mic uses on-device speech-to-text, like the existing journal dictation. Audio is never stored or sent.
- Speech appears in the composer for review before sending.
- **Read replies aloud** (off by default, toggle in the conversation menu) speaks listener replies with on-device text-to-speech.
- Footer while dictating: "Voice isn't recorded."

## Ending a session

**I'm done** opens a sheet:

> **Save this conversation?**  
> It will be saved privately in your journal.  
> **Save to journal** · **Keep talking** · **Discard**

- **Save to journal** saves one entry and opens it. Optional mood, like any entry.
- **Discard** asks once more ("Discard this conversation? It can't be recovered.") and deletes the draft.
- A session with no messages from the person closes without asking.

## Saved entry

- One journal entry labeled **Talk it through**, with the listener (Guided or Alex), date and optional mood.
- The entry view shows the whole conversation: listener questions in a quieter style, the person's words in the main style.
- History preview shows the person's first message, never a listener reply.
- Edit lets the person change their own words; listener replies stay as they were. Delete uses the existing confirmation flow.

## Cross-links

| From | Link | Opens |
|---|---|---|
| Talk it through, Choose a listener | "Looking for encouragement or ideas? **Talk with Alex**" | Talk with Alex |
| Talk with Alex, menu | **Reflect in your journal** | Talk it through, Choose a listener |

The links open the other feature fresh; no messages carry over between them.

## Safety

Applies in both modes.

- The not-therapy notice and crisis-line link stay one tap away for the whole session.
- **Crisis language** in a message triggers the same fixed safety message used in Talk with Alex, with a link to a crisis-line directory by country, instead of a normal reply.
  - Guided: detected on the device with a reviewed phrase list, so no text is sent anywhere.
  - Alex: detected before a reply is generated, as in Talk with Alex.
- After the safety message, the person can keep writing. The session isn't ended or locked.
- The listener never sends notifications or follow-ups outside the session.
- No ads anywhere in this feature.

## Privacy

| Data | Rule |
|---|---|
| Conversation text | Saved as a journal entry, readable only by its owner. Never on Home, in notifications, analytics, logs or personalization. |
| Text sent to Alex | Only with Alex consent, only the current session, only to write the reply. Confirm the provider doesn't retain or train on it. |
| Voice | On-device speech-to-text and text-to-speech. Audio never stored or sent. |
| Alex consent | Stored per account, separate from personalization consent. |

This adds one exception to "journal text never leaves the journal": with consent, With Alex sends the current session to the AI service. Update [Privacy and Safety](../Home/Privacy%20and%20Safety.md) when this ships.

Account deletion removes these entries with the rest of the journal.

## Streaks

Saving a Talk it through entry counts as journal activity, like any entry.

## Accessibility

- Each new listener reply is announced by screen readers (polite live region).
- Speaker roles are exposed ("You said…", "Question…"), not just shown by style.
- Text-to-speech and screen readers don't talk over each other: Read replies aloud pauses while a screen reader is active.
- Touch targets at least 48 dp / 44 pt; large text wraps without clipping; WCAG 2.1 AA contrast.

## Suggested persistence contract

Adapt to the existing Journal schema.

- Entry type: `talk_it_through`.
- `listener`: `guided` | `alex`.
- `messages`: ordered list of `{ role: "user" | "listener", text, followUpId?, createdAt }`. `followUpId` is set for Guided replies.
- `promptId` / `promptText` when started from Explore prompts.
- Draft and saved state follow the existing journal model; one draft per session.
- Alex consent: `consents.talkItThroughAlex = { granted, updatedAt }`.

## Guided follow-ups

Stable IDs, reviewed like the [prompt collection](prompt-collection.md).

| Stage | ID | Follow-up |
|---|---|---|
| Explore | `tit-explore-01` | Tell me more about that. |
| Explore | `tit-explore-02` | What happened next? |
| Explore | `tit-explore-03` | What part of this is on your mind the most? |
| Explore | `tit-explore-04` | When did you first notice this? |
| Feelings | `tit-feel-01` | How did that feel for you? |
| Feelings | `tit-feel-02` | Where do you feel that most right now? |
| Feelings | `tit-feel-03` | If you could name the feeling underneath, what would it be? |
| Feelings | `tit-feel-04` | What was hardest about that moment? |
| Meaning | `tit-mean-01` | What do you think this is telling you? |
| Meaning | `tit-mean-02` | What do you need most right now? |
| Meaning | `tit-mean-03` | What would you say to a friend going through this? |
| Meaning | `tit-mean-04` | Where do you sense God in this, if anywhere? *(faith)* |
| Next step | `tit-next-01` | What's one small thing that might help? |
| Next step | `tit-next-02` | Who could you reach out to about this? |
| Next step | `tit-next-03` | What would you like to remember from this conversation? |
| Close | `tit-close-01` | Is there anything else you'd like to say before we close? |
| Close | `tit-close-02` | What's one kind thing you can tell yourself right now? |

## Analytics

Never message text or anything derived from it.

| Event | Properties |
|---|---|
| `tit_opened` | `plan` |
| `tit_listener_chosen` | `listener` |
| `tit_alex_consent` | `granted` |
| `tit_message_sent` | `listener`, `input` (`typed`, `voice`) |
| `tit_skip_tapped` | `stage` |
| `tit_ended` | `listener`, `turns`, `outcome` (`saved`, `discarded`) |
| `tit_safety_shown` | `listener` |
| `tit_alex_error` | — |
| `tit_alex_limit_reached` | — |

## Acceptance criteria

- [ ] Premium members see Talk it through on the Journaling screen; Free users get the full upgrade screen.
- [ ] Choosing With Alex the first time shows the Alex consent; declining switches to Guided.
- [ ] Guided replies follow the stage order, never repeat in a session, and send no text off the device.
- [ ] Ask me something else returns another follow-up from the same stage.
- [ ] Alex replies use only the current session, stay under 60 words and ask at most one question.
- [ ] An Alex failure offers Try again and Continue with Guided without losing messages.
- [ ] After 50 Alex replies in a day, the session hands off to Guided without losing messages; failed requests and safety messages don't count; the count resets at local midnight.
- [ ] Voice input transcribes on the device and stores no audio.
- [ ] Read replies aloud is off by default and speaks replies when on.
- [ ] The not-therapy notice and crisis-line link are available throughout the session.
- [ ] Crisis language shows the fixed safety message in both modes; the person can keep writing.
- [ ] Save to journal creates one entry that shows the full conversation; Discard removes the draft.
- [ ] Closing the app mid-session keeps the draft.
- [ ] Starting from an Explore prompt uses it as the opening question.
- [ ] Choose a listener links to Talk with Alex, and Talk with Alex's menu links to Talk it through; neither carries messages over.
- [ ] Saving counts toward the streak.
- [ ] Conversation text never appears in analytics, logs, notifications, Home or personalization.
- [ ] Another account cannot read these entries.

## Decisions

Settled:

- Premium only, including voice.
- Two listeners: Guided (curated follow-ups) and With Alex.
- One shared prompt collection with Explore prompts and Reset.
- Name: **Talk it through**. "Therapy" stays out of the app and store listing.
- 50 Alex replies per day, resetting at local midnight.
- Read replies aloud ships in the first version, off by default.
- Lives in Journaling, alongside Talk with Alex. With Alex here is a listener, not a companion, and each feature links to the other.

Still to confirm:

- Alex AI service terms: no retention or training on Talk it through text.

## Phase 2

- A short end-of-session summary the person can keep or edit.
- Talk it through as a prayer: speaking to God, with Scripture-based follow-ups.
- Alex optionally using past Talk it through entries, with separate consent.
- Natural voice for Alex replies.
