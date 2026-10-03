# Decisions

Every product decision behind the Home docs, plus what's still open.

## Still open

| # | Area | Question | Proposed |
|---|---|---|---|
| G | Journal | Search (find old entries by word) and lock (passcode or fingerprint to open the Journal tab) | Phase 2 |

## Decided

### Naming and Home behavior
- The daily personalized card is **"For your heart today"** with "Chosen for you". "Reset" refers only to **Reset Routine**, which already exists.
- Premium users who haven't checked in see Today's Verse. The pick appears only after a check-in.
- If the mood changes later the same day, a new pick replaces the first only if the first wasn't opened.
- No completed state on the card; it stays as is after the pick is finished.
- "Take a moment to check in with God and yourself." shows until the user checks in, then disappears (Free and Premium).
- Mood tiles are sand before check-in and pastel after. The selected tile gets an outline in its mood color (specified in docs, not designed in Figma).
- A picked mood stays selected for the day; tapping another mood changes it.
- The "why" line is general ("Based on how you've been feeling today.") and never names the mood.
- Five pick types: meditation, affirmation, prayer, Talk with Alex, journaling. Virtual Library (reading) is not part of the picks.
- The affirmation pick has no button; the heart saves it.
- The Alex pick shows a message bubble from Alex, only inside the card.
- Home order: header, check-in, daily card, Stories, Words to carry, Explore more, ad banner (Free), bottom navigation. No Journal section on Home.

### Plans
- Free: Today's Verse, Stories, Words to carry, check-in, streaks, notifications, and the Meditations, Affirmations, Journal and Prayer tabs with no limits.
- Premium only: For your heart today, Reset Routine, Virtual Library, Talk with Alex, no ads.
- Tapping a Premium feature as a Free user opens the full upgrade screen.
- Free ad banner sits above the bottom navigation, on Home only.

### Content
- "Read full chapter" opens an in-app Bible reader.
- Phase 1 picks use rules (mood → ordered types); learned personalization comes later, once there's enough analytics.
- Meditations stay YouTube videos. The app adds no ads to meditative screens; YouTube's own in-video ads are accepted.
- Only the featured Story on Home.
- **No comments** on Stories or quotes in MVP. Stories have Like and Share.
- Quotes all come from Seeds for Life. "See more" opens https://www.instagram.com/seedsforlife1111/.
- Saved quotes go to their own Quotes favorites list. No screen to view them yet (Phase 2).
- Prayer: no voice toggle; end screen buttons "Done" and "Read full chapter". Phase 1 prayers are text only: Play moves through the lines on a timer. Narration is Phase 2. Saved prayers can be used in Reset Routine.
- Meditation player: no category label.
- Alex suggests new quick replies as the conversation goes; conversations persist. The Alex menu has only "Clear conversation" for now (no report option yet).
- Stories: no like count shown to users; Share appears in both the top bar and the bottom bar.
- Talk with Alex composer has a mic and Send.

### Streaks
- Any activity counts, including opening or viewing (verse, affirmation, Story, meditation, prayer).
- Streak screen as in Figma: hero card and calendar only.
- Grace day: Phase 2.

### Notifications
- Maximum two a day, quiet hours 10 PM–7 AM, nothing during meditation, prayer or journaling.
- Alex never sends notifications.
- Defaults: daily reminder 8 AM on; evening prayer off; streak reminder off until the first 3-day streak; new stories on.
- No streak-broken notification. No comment notifications.

### Privacy and safety
- Premium users see a consent screen for using check-ins; on/off in Settings.
- Journal text never leaves the journal.
- Alex replies to crisis language with a fixed safety message linking to a crisis-line directory by country.
- Consent screen wording: "Allow Stay Positive to use your check-ins to choose content for you?" [Allow] [Not now].
- Deleting an account deletes all user data, with nothing kept.

### Wrap-up decisions
- Figma text updates done (Done for today, streak wording, comment icons removed).
- Share icon: keep the Figma icon on all platforms.
- Upgrade screen: already exists; Premium badges open it.
- In-app Bible reader: already exists; Read full chapter opens it.
- Mood → pick type table in daily-content-module.md: approved.
- Analytics: keep `heart_pick_completed`, `upgrade_screen_viewed`, `ad_banner_viewed` / `ad_banner_clicked`.