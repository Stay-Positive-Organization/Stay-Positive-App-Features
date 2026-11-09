# Virtual Library: Book notes (V3)

Formatted book notes and "Organize my notes" for books in **Currently Reading** and **Finished Reading**. GitHub issue #511.

Virtual Library is Premium. Access rules don't change: Free users tap it and get the full upgrade screen, so they never reach notes or the AI action.

**Source of truth:** the Figma file (frames to be added from the V3 mockup). This doc describes behavior, copy and product decisions; fonts, sizes and spacing live in Figma.

| Part | Status |
|---|---|
| Markdown notes | Ready to build |
| Organize my notes (AI) | Decisions made; builds after Markdown |

## Where it starts

No new notes destination. Notes stay on the existing book cards.

```text
My Books
├── Currently Reading card ─┐
└── Finished Reading card ──┴─► Notes for {book title}   (list of that book's notes)
                                 ├── note ─► Note editor (opens in Preview)
                                 └── New note ─► Note editor (opens in Edit)
```

- Cards keep their current notes panel: populated shows `Notes · {count}` and the latest note's first line with **View & Edit Notes**; empty shows "No notes yet. Tap to add one." with **Add a Note**.
- Notes list empty state: "No notes for this book yet" / "Capture ideas, quotes and reflections as you read." / **New note**.
- The book title is in the header of the notes list, the editor and the AI review screen. Long titles truncate; the full title is the accessible name.

## Note editor

```text
┌────────────────────────────────────┐
│ ‹  NOTE · JAMES ALLEN      ⋮ [Save]│
│    As a Man Thinketh               │
│    ● Unsaved changes               │
│ [ Edit | Preview ]  Organize my notes
│────────────────────────────────────│
│ ## Chapter 1                       │
│ **The mind shapes character.**     │
│ - thoughts become habits           │
│────────────────────────────────────│
│  H   B   I   •≡  ☑  🔗  ···        │  ← toolbar, Edit only
└────────────────────────────────────┘
```

- **Edit** is a plain multiline text field. Markdown symbols stay visible as typed (`**This matters**` shows the asterisks). Monospace text so symbols are easy to see.
- **Preview** renders the current draft, saved or not. Read-only in this version: checklist items can't be ticked there; users switch to Edit.
- Switching tabs never saves or discards. The draft is held in memory across both tabs.
- New notes open in Edit. Saved notes reopen in Preview.
- Live, Notion-style block editing is out of scope.

### Supported Markdown

| Element | Syntax |
|---|---|
| Headings | `# `, `## `, `### ` |
| Bold, italic | `**text**`, `_text_` (`*text*` also renders italic) |
| Bullet list | `- ` or `* ` |
| Numbered list | `1. ` |
| Checklist | `- [ ] ` / `- [x] ` |
| Quote | `> ` |
| Link | `[text](https://…)` |
| Paragraph break | Blank line |

Anything else shows as plain text. No HTML, no images (remote images never load), no embeds, no scripts. Pasted content is inserted as plain text. Links open in the browser only when tapped in Preview.

### Formatting toolbar

Shown only in Edit, docked directly above the keyboard (at the bottom of the screen when the keyboard is closed). Hidden in Preview and for plain-text notes.

| Control | Accessible label | Behavior |
|---|---|---|
| H | Heading | Menu: Heading 1, Heading 2, Heading 3, Normal text. Sets the prefix on the current line, replacing any list, quote or heading prefix. Choosing the current level again removes it. |
| B | Bold | Selection: wraps in `**`. Already wrapped: unwraps. No selection: inserts `****` with the cursor in the middle. |
| I | Italic | Same as Bold with `_`. |
| Bullets | Bullet list | Toggles `- ` on the current line. |
| Checklist | Checklist | Toggles `- [ ] ` on the current line. |
| Link | Insert link | Opens the link sheet. |
| ··· | More formatting | Menu: Numbered list (`1. `), Quote (`> `). Both apply to the current line. |

"Current line" is the line holding the cursor (the start of the selection). After any action, focus returns to the text field with the cursor or selection kept in place.

**Link sheet:** "Add a link" with **Text to show** (pre-filled with the selected text) and **Link (URL)**. **Insert link** stays disabled until there's a URL. A URL without a scheme gets `https://`. Empty text shows the URL itself. Inserts `[text](url)` in place of the selection. Helper: "Leave the text empty to show the link itself. Links open only when you tap them in Preview."

### Note options (⋮)

- **Copy as Markdown:** copies the raw text of the current draft, including unsaved changes. Toast: "Copied as Markdown".
- **Restore original:** only while a pre-AI version exists (see AI section).

## Saving

Use the app's existing note save and offline sync. Formatting needs no internet; saving behaves as it does today.

| State | Status line (under the title) | Save button |
|---|---|---|
| New, empty | New note · not saved yet | Disabled |
| Edited | Unsaved changes | Save |
| Saving | Saving… | Saving… (disabled) |
| Saved | Saved · {time}, plus toast "Note saved" | Disabled |
| Failed | Couldn't save. Your draft is still here. **Retry** | Retry |

The status line is announced to screen readers. A failed save never clears the draft.

**Leaving with unsaved changes** (back arrow or system back):

> **Save your changes?**
> You have changes to this note that aren't saved yet.
> **Save and leave** · **Discard changes** · **Keep editing**

If the save fails from this dialog, the user stays in the editor with the draft.

Saved notes keep their Markdown text, so formatting is intact on reopen and the note stays editable.

## Existing plain-text notes

Existing notes must look exactly as they do today. `#`, `*` and `_` must not suddenly turn into formatting.

- Add a `format` field to notes: `plain` or `markdown`. Every existing note is migrated as `plain`; every new note is created as `markdown`. A note without the field is treated as `plain`.
- Plain notes: Preview shows the text exactly as typed, whitespace kept. No toolbar.
- Banner on plain notes: "**Plain-text note.** Symbols like # and * show exactly as you typed them." with **Enable formatting**.
- **Enable formatting** opens:

> **Turn on formatting for this note?**
> Formatting reads Markdown symbols. Symbols already in your note, like # at the start of a line, \*stars\* or \_underscores\_, may change how it looks in Preview. Your words stay exactly the same.
> Now: `*re-read the first chapter*` → After: *re-read the first chapter*
> **Enable formatting** · **Cancel, keep as plain text**

- The example uses the first line of the note that contains a Markdown symbol. If none does, hide the example.
- Enabling only changes `format`; the text is untouched. It's an unsaved change until Save (toast: "Formatting on. Save to keep this change."). Cancel changes nothing.

## Organize my notes (AI)

Groups the open note's points under headings. **Organize only**: no summaries, suggested actions or reflection prompts (possible future modes).

### Decisions

| Topic | Decision |
|---|---|
| Provider | Google Gemini |
| What's sent | Only the open note's current text, including unsaved changes. Never journal entries, prayers, Alex chats or other notes. |
| Data | Stay Positive doesn't store the text sent. Confirm Google's handling under our Gemini API plan before launch. |
| Daily limit | 30 per user per day, resetting at midnight in the user's time zone. Organize, Organize latest version and Regenerate each count as one. Failed requests don't count. |
| Entitlement | Premium only, through Virtual Library access. No separate AI entitlement state. |
| Restore original | Available for 1 hour after Apply. |

AI is never required: writing, formatting and saving work without it, including offline.

### Entry

**Organize my notes** sits next to the Edit / Preview tabs, in both tabs.

| Situation | Result |
|---|---|
| Note is empty | Dialog: "**Add some notes first** · Organize my notes works with what you've written. Type or paste your notes for this book, then try again." **Start writing**. No request sent. |
| Note is plain text | The Enable formatting dialog first. |
| Daily limit reached | Dialog (below). No request sent. |
| First use | First-use sheet (below). |
| Otherwise | Starts organizing. |

### First-use sheet

Shown before the user's first request only. Remember the choice per account.

> **Organize my notes**
> AI will group your points under clear headings. It keeps your words, quotes and page numbers. It won't summarize, shorten or add anything new.
> Nothing changes in your note until you review the result and tap **Apply**.
>
> WHAT WILL BE SENT
> *(scrollable box with the exact note text)*
>
> Only this note for **{book title}** is sent, including changes you haven't saved. Your journal, prayers, chats with Alex and other notes are never included.
> Your note is sent to **Google Gemini** to organize it. Stay Positive doesn't keep a copy of what's sent. It's used only to create your organized draft.
> Up to 30 organizes a day · **{n} left today**
>
> **Continue** · **Not now**

### While organizing

Non-blocking banner under the tabs; the note stays readable and editable.

> **Organizing your notes…** You can keep reading or editing. We won't overwrite anything you change. **Cancel**

- Cancel: stop and discard the request. Toast: "Canceled. Your note hasn't changed." Whether a canceled request counts toward the limit follows the server: if it reached Gemini, it counts.
- Save stays available while organizing.

**Note changed during the request:** compare the note text with the text that was sent. If they differ, drop the result and show:

> **Your note changed while we were organizing**
> We didn't replace your newer edits. You can organize the latest version of your note instead.
> **Organize latest version** · **Keep editing**

**Request failed** (network, timeout, provider error):

> **Couldn't organize your notes.** Your note hasn't changed. Check your connection and try again. **Try again** · **Dismiss**

**Daily limit reached:**

> **You've reached today's limit**
> You can organize notes up to 30 times a day. Your limit resets tomorrow.
> You can still write, edit and save your notes anytime.
> **OK**

Enforce the limit on the server; the app shows the remaining count it returns.

### Output rules (prompt requirements)

- Group related points under useful headings. Keep the user's wording, voice, quotes, verses, references and page numbers. Light cleanup only (capitalization, punctuation).
- Use these sections only when the content supports them: **Main ideas**, **Quotes and references**, **My reflections**, **Actions to try**, **Questions to revisit**. Actions become `- [ ]` items.
- Chapter headings only when the user wrote chapter information.
- Never: summarize or shorten, add facts about the book, invent quotes or chapter/page numbers, or create empty sections.
- Output Markdown using only the supported elements above. Validate before showing: strip HTML and images.

### Review screen

Full screen. Header: **Cancel** · "Organized draft" · book title.

- **Original / Organized** toggle (opens on Organized). Original shows exactly what was sent.
- Hint: "Review before applying. Nothing in your note changes until you tap Apply."
- **Regenerate:** organizes the same source text again. Counts toward the limit. Replaces the current draft, including edits made to it.
- **Edit draft:** switches the draft to a Markdown text field; the button becomes **Preview draft**. Hint: "Editing the organized draft. Your note stays unchanged until you apply."
- **Apply to note**, with: "Applying replaces your draft in the editor. You'll still need to save."
- **Cancel:** back to the editor, nothing changed. Toast: "Draft discarded. Your note hasn't changed."

### Apply is not Save

Apply replaces the editor's draft only:

1. Keep the pre-AI text (the text that was sent) as `preAiText` with `preAiAt`.
2. Put the organized draft in the editor, open Preview, status **Unsaved changes**.
3. Toast: "Draft applied. Save to keep it."
4. Banner: "**Organized draft applied.** It isn't saved yet. You can restore the original for 1 hour. **Restore original**"

The banner disappears once the note is saved. The note isn't saved until the user taps Save, and leaving triggers the unsaved-changes dialog as usual.

### Restore original

Available for 1 hour after Apply, from:

- the **Restore original** link in the "applied" banner (until the note is saved), and
- ⋮ → **Restore original** · "Available for 1 hour after organizing".

> **Restore your original note?**
> This replaces what's in the editor with your note as it was before you organized it.
> The organized version and any edits you made after organizing will be removed.
> **Restore original** · **Keep current version**

- Restoring puts `preAiText` back in the editor as an unsaved change. Toast: "Original restored. Save to keep it."
- Clear `preAiText` / `preAiAt` after a restore, or 1 hour after `preAiAt`. Store them with the note so the option survives leaving and reopening within the hour.

## Data

Add to each note (existing note fields unchanged):

| Field | Type | Notes |
|---|---|---|
| `format` | `"plain"` \| `"markdown"` | Existing notes migrate to `plain`. Missing = `plain`. |
| `preAiText` | string, optional | Pre-AI text after Apply. Cleared on restore or after 1 hour. |
| `preAiAt` | timestamp, optional | When Apply happened. |

Daily usage is tracked on the server per user per local day.

## Accessibility

- Text meets 4.5:1 contrast; touch targets at least 48dp.
- Every icon button has a label (see the toolbar table; plus "Back to notes", "More note options").
- Rendered headings are real headings for TalkBack; checklist items announce "Done" or "Not done".
- Status line and toasts are announced. Dialogs trap focus and return it to the control that opened them.
- Layouts grow with larger text: headers wrap, banners expand, review actions stack.
- Loading spinners slow down when reduce motion is on.

## Analytics

| Event | When |
|---|---|
| `book_note_opened` | Note opens (`format`, `has_text`) |
| `book_note_saved` | Save succeeds (`format`, `source`: `manual` or `leave_dialog`) |
| `book_note_save_failed` | Save fails |
| `book_note_format_enabled` | Enable formatting confirmed |
| `book_note_copied` | Copy as Markdown |
| `book_note_organize_started` | Request sent (`first_use`, `remaining`) |
| `book_note_organize_result` | Result shown, failed, canceled or dropped as changed |
| `book_note_organize_applied` | Apply (`edited_draft`, `regenerations`) |
| `book_note_restored` | Restore original confirmed |

Never log note text.
