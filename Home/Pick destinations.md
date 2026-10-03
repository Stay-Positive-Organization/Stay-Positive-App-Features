# Pick Destinations

Screens opened from the For your heart today card (and from the matching bottom-nav tabs). The app never adds its own ads to any of these screens, including completion screens. Meditations are YouTube videos; ads YouTube shows inside a video are outside the app's control and accepted.

| Figma frame | Section |
|---|---|
| Meditation Play | [1. Meditation player](#1-meditation-player) |
| Prayer, Prayer - Done | [2. Guided prayer](#2-guided-prayer) |
| Discuss with Alex | [3. Talk with Alex](#3-talk-with-alex) |
| Journaling (×4) | [4. Journaling](#4-journaling) |

---

Visual details for every screen below are in Figma.

## 1. Meditation player

```text
‹                NOW PLAYING
┌──────────────────────────────┐
│     [ YouTube video ]        │
└──────────────────────────────┘
Title of the video
Channel Name | YouTube
(♡)   (▶ YouTube)          (share)
0:00 ━━━●────────────── 10:24
     (↺)    ( ▶ )    (↻)
```

| Element | Spec |
|---|---|
| Top bar | Back, centered "NOW PLAYING" |
| Video | YouTube video, full width, 16:9-ish with rounded corners |
| Title | Video title |
| Source | "{Channel name} \| YouTube", sage-muted |
| Actions | Save (heart), Open in YouTube (forest circle), Share |
| Progress | Elapsed and total time, gold-forest progress bar with thumb |
| Controls | Back 10s, Play/Pause (forest circle), Forward 10s |

YouTube requirements (must be checked before build):
- Play through the official YouTube player (Android: YouTube IFrame Player in a WebView or the YouTube Android Player API). Do not extract audio or hide YouTube branding.
- Custom controls may drive the official player, but the player itself must stay visible while playing.
- Background or screen-off playback is not allowed by YouTube's terms.
- YouTube may show its own ads inside videos. Accepted: the app keeps using YouTube for meditations.

No category label.

Opening a meditation counts as streak activity. It counts as finished (`heart_pick_completed`) at 90% of its length.

---

## 2. Guided prayer

### Prayer screen (light)

| Element | Spec |
|---|---|
| Top bar | Back; centered "Guided Prayer" with the duration below ("2 min") |
| Label | Gold line + "For your heart today" (only when opened from the Home card) |
| Title | Prayer title, e.g. "A prayer for a quiet mind" |
| Prayer text | One line per row. Current line in ink, upcoming lines in light sage. Current line auto-scrolls into view. |
| Decoration | Sprig illustration bottom-right |
| Player | Progress bar with elapsed/total; controls: Back 10s, Play/Pause, Save (heart) |
| Save | Saves the prayer so the user can use it in **Reset Routine** |

Behavior:
- **Phase 1: text only, no audio.** Play moves through the lines on a timer (prayer duration ÷ number of lines), highlighting each line in turn.
- Phase 2: optional recorded narration, with lines highlighting in sync with the audio.
- Tapping a line jumps to it.
- Reaching the end opens Prayer - Done.

### Prayer - Done (forest)

```text
(×)          Guided Prayer          (♡)
— Done for today
A prayer for you

Amen.
Take one slow breath before you go.
│ "The Lord is nigh unto them that are of a broken heart."
│ Psalm 34:18

[ Done ]   ( Read full chapter )
```

| Button | Action |
|---|---|
| Done | Return to where the prayer was opened (Home or Prayer tab) |
| Read full chapter | Opens the Bible chapter of the closing verse |

---

## 3. Talk with Alex

Premium only. Opened from the Alex pick ("Reply to Alex") or the Talk with Alex tool. Free users tapping the tool see the upgrade screen.

| Element | Spec |
|---|---|
| Header | Back, "A" avatar (gold circle), "Alex" with "Here to listen" |
| Safety notice | Pinned at the top of every conversation, small and centered: "Alex is an AI companion, not a counselor. If you're in crisis, please seek professional help." Add a tappable link: "Find a crisis line in your country", opening a crisis-line directory (e.g. findahelpline.com). |
| Day label | "Today" |
| Alex messages | Sand bubble, left |
| User messages | Sage bubble, right, with "Just now" under the latest |
| Quick replies | Right-aligned outline chips. Alex suggests new ones after each reply (up to 3, short). On first open: "It's been a heavy week", "I don't know where to start". |
| Composer | Rounded field "Share what's on your heart", mic icon, "Send" button (forest pill) |

Quick reply rules:
- Generated with Alex's reply; at most 3, each under ~40 characters.
- Never suggested after a crisis safety message; show only the fixed resources.

Conversation history:
- The conversation persists and is there when the user returns.
- Stored per user, readable only by that user.
- "Clear conversation" in the menu deletes it. It is the only menu option for now; reporting a reply comes later.

Opening message when coming from the Home card: "Hi {firstName}. It sounds like this week has been a lot. I'm here if you want to talk it through."

The mic uses the same dictation as journaling (see 4): on-device speech-to-text, no audio stored, text goes into the composer for the user to review before sending.

Safety requirements (ship with Alex):
- Detect crisis language and respond with a fixed safety message pointing to the crisis-line directory, not a generated reply (see privacy-and-safety.md).
- Alex never sends push notifications or starts conversations outside the Home card.
- No ads. Chat text never goes to analytics.

---

## 4. Journaling

Flow: Home card → Editor → (Listening) → Complete → Home.

### Editor

| Element | Spec |
|---|---|
| Top bar | Back (left), "Done" (sage pill, right; disabled while empty) |
| Label | Gold line + "For your heart today" |
| Title | "Your page is ready" |
| Date | Small, muted |
| Mood | From the Home card (always after a check-in): removable mood chip, e.g. "≋ Overwhelmed ×". From the Journal tab with no check-in today: the mood grid, optional. |
| Page | Ruled lines, placeholder "Today, I…". No title field, no prompt, no word count. |
| Footer | Lock icon + "Saved privately. Voice isn't recorded." |

Saving: draft saves automatically while typing. Back keeps the draft for later the same day. Done saves the entry and opens Complete (first time today) or returns Home (when editing again).

### Listening

The footer becomes a listening bar: gold sound-bars icon, "Listening…", "Speak freely. Tap when you're done.", and a mic button on the right that stops listening.

- Words appear on the page as they're recognized, after any existing text.
- Leaving the screen stops listening.
- Use Android `SpeechRecognizer` with on-device recognition. Never store audio; "Voice isn't recorded" is a promise.
- First use: show a short rationale, then the system permission ("Stay Positive uses your microphone only to turn your words into text. Audio isn't saved.").
- Permission denied: toast "Microphone is off. You can turn it on in Settings."

### Complete (forest)

```text
(×)            Journaling
— Done for today

Your page is saved.
Thank you for making space for your heart today. Whatever you wrote,
God already knows it and holds it with care.

┌ 🔥 5-day streak ─────────────────────────┐
│ You've shown up five days in a row.       │
└───────────────────────────────────────────┘

[ Back to Home ]   ( Open journal )
```

Streak line: "You've shown up {n} days in a row."

Shown only the first time the journaling pick is completed that day.

---

## Acceptance criteria

- [ ] No app ads on any screen in this document.
- [ ] Meditation plays through the official YouTube player; save, open in YouTube and share work.
- [ ] Guided prayer highlights the current line, supports tap-to-jump, and ends on Prayer - Done.
- [ ] Alex shows the safety notice, quick replies, and a working mic + Send composer.
- [ ] Journaling shows the mood chip or the mood grid depending on today's check-in.
- [ ] Dictation appends text, can be stopped, and stores no audio.
- [ ] Complete screens appear once per day.