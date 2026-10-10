# Privacy and Safety

Rules that apply across Home and every screen it opens.

## Consent for personalization

Personalization is optional, available to Premium users, and separate from device notification permission. Consent starts off unless a previously recorded valid consent exists.

### Consent screen copy

STAY POSITIVE PREMIUM

**Support for your heart**

Would you like suggestions based on your mood check-ins?

**What personalization means**

- Use your mood check-ins to suggest verses and activities.
- Journal and prayer text stay out of personalization.
- You can turn this off any time in Settings.

You can still check in and read Today’s Verse without personalization.

**Enable personalization**

The latest design has one primary button. Provide a visible Back/close route so users can leave without enabling personalization and continue using the app.

### When to show it

- Newly upgraded Premium users: after upgrade confirmation and before their first personalized recommendation.
- Existing Premium users without a recorded choice: the first time they use the new “For your heart today” feature, before a personalized-content request.
- Free users do not see this screen.
- Remember the choice per account, including leaving without enabling personalization; do not repeatedly prompt.
- Respect previously recorded valid consent. A copy update alone does not require another invitation.
- Users who leave without enabling personalization may enable it later in Settings.

### Settings copy

**Personalization**

**Use my check-ins to personalize**

Get verse and activity suggestions based on your mood check-ins.

Journal and prayer text are never used for personalization.

Turn this off to receive Today’s Verse instead.

You’re in control. Change this any time.

### Settings and consent behavior

- Show the Personalization section for Premium users.
- Reflect the saved consent value in the switch; default to off when consent has not been granted.
- **Enable personalization** and explicitly switching the Settings control on record consent.
- Without consent, Premium users see Today's Verse after check-in, like Free users. Check-ins are still saved for their own history and streak.
- With consent, Premium users see Today's Verse before check-in and “For your heart today” after check-in.
- Turning consent off stops personalization from the next request and replaces the personalized Home card with Today's Verse.
- Journal and prayer text are never used for personalization.
- Persist the choice across relaunch and account sign-in.
- Show clear save-error feedback. Do not present an unsaved choice as successful or request personalized content before consent is confirmed.

## Data rules

| Data | Rule |
|---|---|
| Mood check-ins | Stored per user. Used for personalization only with consent. Never in logs beyond analytics events. |
| Journal text | Never leaves the journal: not on Home, not in notifications, not in analytics, not used for personalization. Readable only by its owner (Firestore rules). |
| Voice dictation | On-device speech-to-text. Audio never stored or sent. |
| Prayer text | Never in analytics or notifications, and never used for personalization. |
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

## Personalization implementation issues

- [Kotlin consent screen and Settings #414](https://github.com/Stay-Positive-Organization/Stay-Positive-Kotlin-App/issues/414)
- [iOS consent screen and Settings #53](https://github.com/Stay-Positive-Organization/StayPositive-IOS/issues/53)
- [Kotlin consent storage and enforcement #429](https://github.com/Stay-Positive-Organization/Stay-Positive-Kotlin-App/issues/429)
- [iOS consent storage and enforcement #68](https://github.com/Stay-Positive-Organization/StayPositive-IOS/issues/68)
