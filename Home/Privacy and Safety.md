# Privacy and Safety

Rules that apply across Home and every screen it opens.

## Consent for personalization

- When a user becomes Premium, show a consent screen: "Allow Stay Positive to use your check-ins to choose content for you?" with Allow and Not now.
- Add an on/off switch in Settings ("Use my check-ins to personalize").
- Without consent, Premium users see Today's Verse after check-in, like Free users. Their check-ins are still saved for their own history and streak.
- Turning consent off stops personalization from the next request.

## Data rules

| Data | Rule |
|---|---|
| Mood check-ins | Stored per user. Used for personalization only with consent. Never in logs beyond analytics events. |
| Journal text | Never leaves the journal: not on Home, not in notifications, not in analytics, not used for personalization. Readable only by its owner (Firestore rules). |
| Voice dictation | On-device speech-to-text. Audio never stored or sent. |
| Prayer text | Never in analytics or notifications. |
| Alex conversations | Persist per user, readable only by that user, deletable with "Clear conversation". Never in analytics or notifications. |
| Streak activity | Store activity type and time only. |

## Talk with Alex safety

- Pinned notice at the top of every conversation: "Alex is an AI companion, not a counselor. If you're in crisis, please seek professional help." plus a tappable link: "Find a crisis line in your country".
- Crisis language triggers a fixed safety message instead of a generated reply. It points users to a directory of crisis lines by country (e.g. findahelpline.com) rather than a single number, so it works everywhere. Confirm the directory link works before launch.
- Alex never sends notifications or starts conversations on its own.

## Account deletion

Users can delete their account in the app (required by Google Play). Deleting an account removes **everything**, with nothing kept:

- Check-ins and mood history
- Journal entries
- Alex conversations
- Saved quotes, saved prayers and affirmation favorites
- Streak activity and notification history
- Consent settings and profile

Delete server-side (Cloud Function) so nothing is left in Firestore or Storage.

## Mood language

- Never imply a diagnosis or treatment from a mood.
- Never name the user's mood on Home ("Based on how you've been feeling today.").
- `I don't know` is a valid answer.

## Ads

- Free Home only: banner above the bottom navigation.
- The app never adds ads to meditation, prayer, journaling, Alex or completion screens.
- Meditations are YouTube videos; ads YouTube shows inside them are outside the app's control.