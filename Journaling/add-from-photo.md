# Add from Photo (Handwritten Notes)

**Status:** Feature specification for implementation; not yet a shipped feature. Tracked in app issue #520.  
**Location:** Reset Routine › Step 6 Journaling (first version).  
**Platforms:** Shared product behavior for Android (Kotlin) and iOS.  
**Plans:** Premium, because Reset Routine is Premium. No extra gate.

## Purpose

Some people journal on paper. Add from photo lets them photograph a handwritten page, or pick a photo they already took, and turn the writing into editable text in their Reset Routine journal entry, without retyping it.

It is transcription into the entry, not a photo attachment. The photo is never saved to the journal.

An optional **Organize with AI** step tidies the transcription (line breaks, paragraphs, spelling) before it's inserted, without changing what the person wrote.

Visuals live in the Figma file, [Reset Routine V3 › Journaling · Add from photo](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H/Stay-Positive-App?node-id=3192-919) (screens 1–11 plus a notes card). This doc covers behavior and copy.

## User story

As someone who prefers writing on paper, I want to photograph or upload my handwritten journal notes so that I can save them as text in Stay Positive and continue my Reset Routine.

> I wrote a page in my notebook before breakfast. In Reset Routine I reach Journaling, tap **Add from photo**, and take a picture. The app reads it, I fix one word it got wrong, tap **Organize with AI** so the lines become paragraphs, and insert it. I tap **Complete Reset**.

## First-version scope

- An **Add from photo** entry in the Reset Routine journaling editor.
- Take a photo or choose one from the device; one page per extraction, repeatable for more pages.
- Preview with rotate, crop and retake.
- Handwriting recognition into editable text, reviewed before insertion.
- Optional **Organize with AI** with a one-time consent and an Original | Organized compare.
- Insert (or append) into the entry with **Undo**.
- Clear states for camera access off, couldn't read, couldn't finish, and offline.

Out of the first version: saving or attaching the photo, several pages in one extraction, using it outside Reset Routine (the main Journal and Gratitude can reuse it later), and AI summaries or rewrites.

## Flow

```text
Reset Routine › Step 6 Journaling
└── Add from photo (pill next to the mic)
      └── Sheet: Take photo / Choose photo ── camera off ─► Camera access is off
            ▼
      Check your page (rotate · crop · retake)
            │ Extract text
            ▼
      Reading your page… ── can't read ─► We couldn't read this page
            │              └─ error / offline ─► We couldn't finish reading
            ▼
      Review your text (editable)
            ├── Organize with AI (optional)
            │     └── consent (first time) ─► Original | Organized
            ▼
      Insert into entry ─► entry updated + "Page added to your entry · UNDO"
```

## Screens and copy

### 1. Entry point

| Element | Copy / behavior |
|---|---|
| Placement | Pill under the journal field, between the word count and the mic |
| Label | 📷 Add from photo |
| Accessibility | "Add text from a photo of handwritten notes" |

Typing and the mic stay available. Opening the camera or picker never clears the draft.

### 2. Choose a source (bottom sheet)

| Element | Copy |
|---|---|
| Title | Add from photo |
| Supporting line | Turn a handwritten page into text you can edit. |
| Option 1 | **Take photo** · Use your camera on one page |
| Option 2 | **Choose photo** · Pick a picture from your phone |
| Privacy line | 🔒 Your photo is private. It isn't saved to your journal. |
| Dismiss | Cancel |

Choose photo uses the system photo picker (no broad storage permission).

### 3. Camera access is off

| Element | Copy |
|---|---|
| Title | Camera access is off |
| Body | To photograph a page, allow camera access in Settings. You can also choose a photo you already took, or keep typing. |
| Actions | **Open Settings** · Choose photo instead · Not now |

### 4. Check your page

| Element | Copy / behavior |
|---|---|
| Title | Check your page |
| Supporting line | Keep the whole page in the frame and the writing easy to see. |
| Tools | Rotate · Crop · Retake (Retake becomes **Change photo** when the photo came from the picker) |
| Hint | One page at a time. You can add more pages after this one. |
| Actions | **Extract text** · Cancel |

### 5. Reading your page

| Element | Copy / behavior |
|---|---|
| Title | Reading your page |
| Progress | Reading your handwriting… · This can take a few seconds. Your entry is safe. |
| Action | Cancel (returns to the journal with the draft intact and discards the temporary image) |

### 6. Review your text

| Element | Copy / behavior |
|---|---|
| Title | Review your text |
| Banner | Handwriting recognition can make mistakes. Check names, dates and anything that matters before you insert. |
| Source row | Page 1 · from your photo · View photo |
| Field | Editable transcription. Words the recognizer is unsure of are underlined in gold. |
| Helper | Tap any word to fix it. Underlined words may be misread. |
| Optional | ✨ **Organize with AI** · Optional. Tidies line breaks, paragraphs and spelling. Never adds or removes ideas. |
| Actions | **Insert into entry** · Cancel |

The transcription keeps reading order and paragraph breaks where it can. It never summarizes, rewrites or fills in missing words.

### 7. Organize with AI — consent (first use)

> **Organize with AI?**
>
> - Only the text is sent — never your photo.
> - It's processed to tidy your writing, then deleted. It isn't saved by our AI provider or used to train AI.
> - You'll compare before anything changes, and you can keep your original.
>
> Privacy details
>
> **Organize my text** · Not now

Remembered per account. Can be turned off in Settings › Privacy (**Let AI organize text from photos**); turning it off brings the consent back next time.

### 8. Original | Organized

| Element | Copy / behavior |
|---|---|
| Toggle | Original \| Organized (Organized selected after running) |
| Badge | ✨ AI |
| Field | Organized text, editable |
| Note | Only spacing, paragraphs and spelling changed. Read it over and edit anything before you insert. |
| Actions | **Insert into entry** · Use original instead · Cancel |

### 9. Inserted

The text is added to the entry and the field scrolls to it.

| Element | Copy |
|---|---|
| Snackbar | Page added to your entry · **UNDO** |

The Add from photo pill stays, so the next page can be added the same way.

### 10. We couldn't read this page

Shown when no text is found or confidence is too low to be useful. No partial or invented text is shown.

| Element | Copy |
|---|---|
| Title | We couldn't read this page |
| Body | The writing may be faint, blurry or at an angle. Nothing was added to your entry. |
| Tips | For a clearer photo: Use bright, even light — avoid shadows · Fit one whole page in the frame · Hold your phone flat above the page |
| Actions | **Retake photo** · Choose another photo · Type instead |

### 11. We couldn't finish reading

| Case | Title / body |
|---|---|
| Error or timeout | We couldn't finish reading · Something interrupted us. Your photo and your entry are still here. |
| Offline (only if extraction needs internet) | You're offline · Connect to the internet to read this page. |
| Unsupported or too-large image | This photo can't be used · Try a JPG or PNG under 15 MB. |

Actions: **Try again** · Choose another photo · Type instead.

## Organize with AI rules

- Runs only when the person taps it. Never automatic, never a default.
- Sends the extracted text only, through our backend (no API key in the app). The image is never sent for this step.
- Allowed: line breaks, paragraphs, punctuation, capitalization, obvious spelling.
- Not allowed: summarizing, rewording, reordering, adding or removing ideas, adding a title, changing names or dates.
- A validation check compares the output with the input; if words were dropped or added beyond spelling fixes, the app keeps the original and shows "We couldn't organize this page. Your original text is unchanged."
- Offline: the chip is disabled with "Needs internet". The plain transcription can always be inserted.
- The provider's retention and no-training terms must match the consent copy before this ships.

## Insert rules

- Empty entry: the reviewed text becomes the entry.
- Entry with text: append after a blank line. Never overwrite.
- Typing during extraction is kept. Insert applies to the latest text, not a snapshot from before extraction.
- **Insert into entry** disables after the first tap. **Undo** removes only that inserted page.
- Several pages append in the order they're inserted.
- Previewing, extracting or organizing never marks journaling complete. Completion still happens through **Complete Reset** and the existing save flow.

## Privacy

- Photos and extracted text are private journal content.
- The photo is processed and then the app's temporary copy is deleted, including on cancel. The person's original gallery photo is never touched.
- Inserted text is saved through the existing private journal storage and owner-only access rules.
- Photos and text never appear in analytics, crash reports or logs, and are never used for personalization.
- On-device recognition is preferred if it reads handwriting well enough. If recognition has to be remote, the provider, retention and deletion are documented, and the person agrees before an image is sent. The privacy line on the source sheet changes to match.

## Accessibility

- All icon buttons have labels (Rotate, Crop, Retake, Close, Undo).
- The progress state is announced ("Reading your handwriting").
- Gold underlines for uncertain words are paired with a text hint, not color alone.
- Layouts reflow at large font sizes and on small screens; action buttons stay reachable.

## Acceptance criteria

- [ ] A person can capture or choose a photo of a handwritten page and get editable text in the Reset Routine journal.
- [ ] Recognition is evaluated on cursive, faint or blurry writing, rotated pages and mixed printed/handwritten pages; quality and limits are recorded here.
- [ ] Text is reviewed and editable before insertion.
- [ ] Existing text and edits survive capture, cancel, errors and insertion.
- [ ] Multiple pages append in order without duplicates; Undo removes only the last inserted page.
- [ ] Inserted text saves, reopens and completes Reset Routine through the existing flow.
- [ ] Organize with AI runs only after a tap and accepted consent; the image is never sent for it.
- [ ] Organized text keeps every idea from the original; the person can switch back before inserting.
- [ ] Offline, Organize with AI is unavailable and the plain transcription can still be inserted.
- [ ] No photo or text appears in logs or analytics; temporary images are cleaned up.

## Open questions

- Recognition approach and where it runs (on-device vs remote) — decided after testing real handwriting samples.
- Supported languages for recognition and for Organize with AI.

## Related

- [Journal](../Home/Journal.md) — storage, privacy and edit behavior this reuses.
- [Talk it through](talk-it-through.md) — same pattern for AI consent.
- App issues: #520 (this feature), #439 (Reset Routine journaling screen), #518 (journal microphone bug).
