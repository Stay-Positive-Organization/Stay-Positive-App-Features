# Referral program — share Stay Positive

**Status:** Product proposal for UX design; not implemented or scheduled.
**Owner:** Evelise (@evydsg).
**Planning task:** [Android #493](https://github.com/Stay-Positive-Organization/Stay-Positive-Kotlin-App/issues/493).
**Figma:** To be added by Evelise.

## Purpose and user stories
Help people introduce someone they care about to Stay Positive and experience Premium together.

- As an existing user, I want to share a personal invitation so a friend can discover the app and we can earn Premium access.
- As an invited person, I want to understand the offer and any conditions before creating an account.
- As a participant, I want to know whether my referral qualified and when my free Premium access ends.

## Reward direction and proposed starting offer
Evelise supports offering free Premium access as a referral reward.

**Pilot offer (decided by Evelise): give 30 days of Premium to the invited friend and 30 days to the inviter after the friend qualifies.** Decided rules are marked below; anything still marked proposed is open for refinement during UX/product work.

Thirty days gives both people enough time to use Premium as part of a routine, not just sample it. Because the reward is larger, the cap, redemption window and misuse protections below matter more. Whether it improves activation, retention or conversion remains a hypothesis to measure. Do not describe the program as proven growth.

| Participant | Proposed benefit | Proposed trigger |
|---|---|---|
| Invited friend | 30 days of complimentary Premium, once per new account | Creates an eligible new account through the referral |
| Inviter | 30 days of complimentary Premium per qualifying friend | The same referral qualifies; one reward per friend |

**Qualifying action (decided by Evelise): account creation.** A referral qualifies when an eligible new account is created with the referral applied; no check-in or other in-app activity is required. Because this is a low bar for a 30-day reward, the one-reward-per-account rule, inviter cap and duplicate/self-referral protections are what limit misuse. The inviter never sees the friend's moods or other activity.

## Proposed pilot rules
- Who can invite (decided by Evelise): everyone, Free and paid Premium. In the pilot, only inviters without an active paid subscription earn the inviter reward. A paid subscriber's invited friends still receive their 30 days.
- Inviter eligibility is checked when the friend qualifies. A referral that qualifies while the inviter has an active paid subscription earns no inviter reward and does not use one of their three reward slots.
- A qualifying friend is a new Stay Positive account with one valid referral applied during sign-up, before the account is created. A code entered after account creation does not qualify. Existing accounts cannot claim a new-user reward.
- Sharing, clicking a link or installing alone does not earn a reward.
- Invited friend reward: one 30-day grant per eligible new account.
- Inviter reward: pilot cap of three qualifying friends (decided by Evelise), so at most 90 reward days per inviter. Show remaining eligibility clearly, for example "2 of 3 rewards left".
- Redemption window (decided by Evelise): the friend creates their account within 30 days of accepting the invitation. After that the invitation expires and neither person is rewarded for it.
- One friend can credit only one inviter; proposed rule is the first valid referral confirmed by the friend. Do not overwrite it silently.
- Self-referrals, duplicate claims and repeated processing must not create additional grants.
- Complimentary access requires no payment details and does not start an automatically renewing subscription.
- When complimentary access ends, return to the user's underlying entitlement. Keep journal entries, favorites and other saved content; gate Premium features according to normal app rules.
- Personalization and device notifications remain separate opt-ins. Receiving Premium must not enable either automatically.
- Rewards are access to features, with no cash value or cash redemption.

## Access timing and existing subscriptions
For a Free user, proposed reward access starts when the referral qualifies. If another referral reward is already active, append days after its expiry rather than running overlapping grants.

An active paid subscription must not be silently paused, canceled, discounted or described as extended. For the pilot, paid subscribers do not receive an inviter reward (see rules above). A paid-subscriber reward, such as a deferred complimentary-access grant after paid access ends or a supported Google Play subscription offer, can be considered after the pilot. Do not promise a billing credit.

Trials and other free access (decided by Evelise):
- If the invited friend already has an active free trial or paid subscription when the referral qualifies, the friend receives no referral reward. Referral days are never stacked on top of a Play trial.
- The inviter's reward is unaffected, because the friend still created an eligible new account (decided by Evelise).
- A Free member's referral rewards run back to back (three friends gives up to 90 consecutive days).

Still to resolve with engineering: restoring purchases, refunds, account changes and platform changes. Referral access should follow the same account entitlement across supported devices without duplicating rewards.

## Entry points and screens
Entry points (decided by Evelise):

1. **Sign-up: "Have a referral code?"** For the invited friend. An optional field in the sign-up flow, prefilled when the invitation link carries the code. The code must be applied before the account is created.
2. **After sign-up or login: invite prompt.** For existing and new users, inviting them to share Stay Positive. Opens the main referral screen.
3. **Profile/Settings row: Invite a friend.** The permanent home of the referral screen.
4. **One prompt after finishing an activity.** A contextual invite shown after completing any activity, such as a meditation, the Reset flow, affirmations, a journal entry or a 30 Days of Gratitude day (decided by Evelise). It appears after the activity's own completion screen, never during the activity, and never covers the user's content.
5. **Home screen spot.** A card or banner that opens the main referral screen.

Prompt frequency (decided by Evelise):
- **Activity prompt:** at most once every 7 days, with **Not now** and **Don't show again**.
- **After-login prompt:** once only, on the first login after the feature launches, and on a new user's first sign-up.
- **Home screen spot:** stays until dismissed; after dismissal it returns only when something changes, such as a friend joining.
- **Across all prompts:** at most one invite prompt per session. Stop prompting once a Free member has used all three rewards; paid subscribers can still be prompted because their friends still receive 30 days. Hide all prompts while the program is unavailable. The Profile/Settings row is always available.

### 1. Main referral screen
Final copy (approved by Evelise, Nov 2026). Text in `[brackets]` is filled in by the app.

**Header**
- Title: **Share a little encouragement**
- Subtitle: **Invite a friend to Stay Positive. When they create their account, you each get 30 days of Premium.**

**Your invite**
- Label: **Your invite code**
- Code: `[SP-7K4Q]` (non-identifying random code)
- Primary button: **Invite a friend**, which opens the native share sheet
- Secondary button: **Copy link**, which shows the toast **Link copied**

**Share message** (prefilled in the share sheet)
> I've been using Stay Positive for daily encouragement and thought of you. Join with my link and we'll both get 30 days of Premium: [link]
> Or enter my code when you sign up: [SP-7K4Q]

**How it works**
1. **Share your link** with someone you care about.
2. **They create an account** within 30 days using your link or code.
3. **You both get 30 days of Premium.**

**Your rewards** (card content by state)
- No referrals yet: **No friends have joined yet. You can earn up to 3 rewards.**
- Some earned: **[2] of 3 rewards earned · Premium until [Dec 12, 2026]**
- All used: **You've earned all 3 rewards. Thank you for sharing! Friends who join still get 30 days of Premium.**
- Paid subscriber: **You're already a Premium member. Friends who join with your link still get 30 days of Premium.**

**Friends** (shown only once someone has joined)
- **[Sarah] joined · 30 days added**
- **[A friend] joined · Reward pending**
- **[Sarah] joined · Thanks for sharing** (friend joined after the cap was reached, or while the inviter was a paid subscriber)

**Footer**
- Link: **Program terms**

Notes:
- Avoid contact uploads or automatic invitations; the native share sheet lets the person choose whom to invite.
- Rows never say "no reward"; "Thanks for sharing" keeps a non-rewarded referral from reading as a loss.
- No faith language on this screen, so the share message works for any friend.

### 2. Friend invitation and acceptance
Final copy (approved by Evelise, Nov 2026). Text in `[brackets]` is filled in by the app.

**A. Invitation web page** (parked for the pilot; the link redirects to the Play Store instead. Keep this copy for a later page.)
- Heading: **A little encouragement, shared with you**
- Body: **[Sarah] invited you to Stay Positive. Create your account within 30 days and you'll both get 30 days of Premium.**
- Button: **Get it on Google Play**
- Code box: **Your invite code: [SP-7K4Q]** with a **Copy** button
- Helper line: **If the code doesn't appear when you sign up, enter it on the "Have a referral code?" step.**
- The page shows the inviter's first name to anyone with the link; it shows nothing else about them.

**B. In-app invitation** (app installed and link opened, before sign-up)
- Heading: **A little encouragement, shared with you**
- Body: **[Sarah] invited you. Create your account and you'll both get 30 days of Premium. No payment details needed.**
- Button: **Create my account**
- Text link: **I already have an account**

**C. Sign-up: "Have a referral code?"**
- Field label: **Referral code (optional)**, prefilled when the link carried the code
- Applied: **✓ Code applied. You'll get 30 days of Premium when your account is created.**
- Name notice under the applied code: **[Sarah] will see your first name when you join.**
- Errors never block sign-up:
  - Invalid: **We couldn't find that code. Check it and try again, or continue without one.**
  - Expired: **This invitation has expired. You can still create your account.**
  - Own code: **This is your own invite code. Share it with a friend instead.**

**D. Existing account opens a link**
- **You already have an account, so this invitation can't be used. Want to share Stay Positive yourself?** Button: **Invite a friend**

**E. Friend's reward confirmation** (after onboarding finishes)
- Title: **Your 30 days of Premium are ready**
- Body: **Thanks to [Sarah], you have Premium until [Dec 7, 2026]. Nothing renews and no payment is needed.**
- Button: **Explore Premium**
- Friend already had a trial or paid subscription: **Welcome! Your current plan stays as it is, and [Sarah] has been thanked for inviting you.**

Implementation notes:
- Do not assume referral attribution survives a store install; define and test the link/code handoff. Manual code entry is the fallback.
- Apply the referral before account creation, then continue the existing onboarding flow unchanged.
- Record qualification once when the account is created.

### 3. Inviter confirmation, prompts and reward lifecycle
Final copy (approved by Evelise, Nov 2026). Text in `[brackets]` is filled in by the app.

**F. Inviter's reward confirmation** (next app open after a friend joins)
- Title: **[Sarah] joined Stay Positive!**
- Body: **You've earned 30 days of Premium. You now have Premium until [Jan 6, 2027].**
- Button: **Explore Premium** · Text link: **Invite another friend**
- Cap reached or paid subscriber: **[Sarah] joined Stay Positive! Thank you for sharing. They now have 30 days of Premium.**

**G. Prompt after sign-up/login** (bottom sheet, shown once)
- Title: **Know someone who'd love this?**
- Body: **Invite a friend and you'll each get 30 days of Premium.**
- Buttons: **Invite a friend** · **Not now**

**H. Prompt after finishing an activity** (at most once every 7 days, after the activity's completion screen)
- Title: **Feeling encouraged? Pass it on.**
- Body: **Invite a friend to Stay Positive and you'll each get 30 days of Premium.**
- Buttons: **Invite a friend** · **Not now** · **Don't show again**

**I. Home screen card** (stays until dismissed)
- Title: **Share a little encouragement**
- Body: **Invite a friend. You'll each get 30 days of Premium.**
- Button: **Invite** · close icon (✕)

**J. Reward expiring and expired** (in-app only; device notifications remain opt-in)
- 3 days before: **Your Premium from referrals ends on [date]. Your journal entries and favorites are always kept.**
- After it ends: **Your referral Premium has ended. Everything you saved is still here.** Button: **See Premium plans**

**K. Error states**
- Offline: **You're offline. Your invite code will appear when you're back online.**
- Program unavailable: **Invites aren't available right now. Please check back later.**

What the inviter sees (decided by Evelise):
- **Counts and status:** for example "2 friends joined · 2 of 3 rewards earned · Premium until Dec 12".
- **A row per friend with their first name or display name:** for example "Sarah joined · 30 days added" or "Sarah joined · Thanks for sharing" (see the main screen copy).
- The invited friend is told during sign-up, next to the referral code, that their inviter will see their first name or display name. If no name is available, the row shows "A friend".
- Proposed, to confirm during UX: the friend can choose to show as "A friend" instead of their name.
- The inviter never sees the friend's moods, journal text, chat, activity, purchases or any other private information.

### 4. Required UX states
- First use with no referrals.
- Link copied and share-sheet return. Share-sheet return is not proof of a sent invitation.
- Pending referral; qualifying event awaiting processing.
- Reward granted; access expired.
- Invalid/expired code, self-referral, existing account, duplicate claim.
- Reward cap reached, offline/save failure and program unavailable.
- Paid subscriber on the referral screen: they can share, and the screen explains that their friend gets 30 days of Premium while inviter rewards are for Free members during the pilot.

Match Stay Positive colors and typography. Support text scaling, screen readers, clear selected/focus states and accessible touch targets.

## Program terms (user-facing)
Approved draft (Nov 2026), shown behind the **Program terms** link. Needs legal review before launch.

> **Stay Positive Referral Program: Terms**
> *Last updated: [launch date]*
>
> **How it works**
> Share your personal invite link or code. When a friend creates a new Stay Positive account using it, you each receive 30 days of Premium.
>
> **Who can take part**
> - Anyone with a Stay Positive account can invite friends.
> - Your friend must create a **new** account and apply your link or code during sign-up. Codes entered after an account already exists can't be used.
> - Your friend must create their account within **30 days** of opening your invitation.
> - You can't use your own code.
>
> **Rewards**
> - **Your friend:** 30 days of Premium, once per new account.
> - **You:** 30 days of Premium for each friend who joins, up to **3 friends** (90 days in total).
> - If you earn more than one reward, the days are added one after another.
> - During this program, inviter rewards are for members without an active paid subscription. If you're a paying Premium member, your friends still receive their 30 days.
> - If your friend already has an active free trial or paid subscription when they join, they won't receive the referral reward, but you still will.
>
> **About your free Premium**
> - No payment details are needed, and nothing renews automatically.
> - When your free Premium ends, your account returns to its previous plan. Your journal entries, favorites and saved content are always kept.
> - Rewards have no cash value and can't be transferred or exchanged.
>
> **Your privacy**
> - The person who invited you will see your first name or display name and that you joined.
> - They will **never** see your moods, journal entries, activity or purchases.
> - Taking part doesn't turn on notifications or personalization; those remain your choice.
>
> **Fair use**
> We may withhold or remove rewards gained through duplicate or fake accounts, self-referrals, or other misuse.
>
> **Changes**
> We may change or end this program at any time. Rewards already granted will be honored.
>
> **Questions?** Contact us at hello@staypositiveapp.com.

## Routing, attribution and entitlements (approved Nov 2026)
Based on the current Android app and Cloud Functions.

Current state:
- Verified App Links already exist on `https://staypositive.app` (`/story/` on `StoryDetailActivity`).
- Firebase Dynamic Links was shut down by Google in August 2025; do not use it.
- The app does not yet include the Play Install Referrer library.
- Premium comes only from billing: `BillingManager` sets `isPremium`, and `googlePlayWebhook` writes `isPremium: false` on expiry or revocation.
- Existing functions are HTTP `onRequest` endpoints; the app already uses App Check with Play Integrity.

### Links
- Invite link: `https://staypositive.app/invite/{code}`, added to the verified App Link intent filter.
- **App installed:** the link opens the in-app invitation (screen B); the code is held until sign-up.
- **App not installed (decided by Evelise):** `staypositive.app/invite/{code}` redirects straight to `https://play.google.com/store/apps/details?id=com.app.staypositive&referrer=ref%3D{code}`. No web invitation page in the pilot; a page can replace the redirect later without changing shared links.
- **First launch after install:** read the Play Install Referrer once and prefill the sign-up code. Manual code entry is always available as the fallback.

### Separate referral entitlement
- Store `referralPremiumUntil` (server time) on the user in Firestore, separate from paid `isPremium`.
- The app treats a user as Premium when paid `isPremium` is true **or** `referralPremiumUntil` is in the future.
- `googlePlayWebhook`, `verifySubscription`, `restoreSubscription` and client purchase restore never change `referralPremiumUntil`.

### Server-side rules
Callable Cloud Functions, requiring Firebase Auth and App Check:
- `applyReferralCode`: validates a code at sign-up; returns the inviter's first name or an error reason (invalid, expired, own_code).
- `qualifyReferral`: runs once when the account is created. Checks the new-account rule, 30-day window, cap of three, and both people's paid or trial status, then grants rewards. Idempotent: repeat calls never grant twice.
- `referrals` collection: one audit record per friend (inviter, friend, status, timestamps), written only by the server.
- Codes are random and non-identifying; each inviter keeps one code.

### Tests
Link install vs. Play Store install, manual code entry, retried or duplicate `qualifyReferral`, offline at sign-up, webhook expiring a paid plan while referral days remain, and purchase restore.

## Developer handoff scope
After the rules and UX are ready, create separate tasks for:
1. Android referral screen, sharing, code entry, routing and onboarding integration.
2. Backend attribution, eligibility, qualification, one-time reward grants, account entitlements and expiry.
3. Invite link redirect to the Play Store and App Link routing (folded into the backend friend-journey ticket); coordinate iOS when ready.
4. Tests for retries, offline recovery, repeated links, duplicate qualification and purchase/reward interactions.

Use server-side eligibility and reward calculations; never rely on client-only counters. Keep an auditable grant record and make repeated qualification requests idempotent. Use non-identifying random referral codes.

## Measurement
Analytics events (approved by Evelise, Nov 2026), Firebase Analytics naming:

| Event | When it fires | Parameters |
|---|---|---|
| `referral_entry_point_shown` | A prompt or the Home card is displayed | `entry_point` (signup_login, activity, home_card) |
| `referral_entry_point_tapped` | The user opens the referral screen from any entry point | `entry_point` (adds settings_row) |
| `referral_prompt_dismissed` | Not now, Don't show again, or ✕ on the Home card | `entry_point`, `action` |
| `referral_screen_view` | The main referral screen opens | `inviter_status` (free, paid, cap_reached) |
| `referral_share_tapped` | Invite a friend or Copy link is tapped | `method` (share_sheet, copy_link) |
| `referral_invite_landing` | The redirect is hit or the in-app invitation opens | `surface` (redirect, app) |
| `referral_code_applied` | A valid code is applied at sign-up | `source` (link, manual) |
| `referral_code_error` | A code is rejected | `reason` (invalid, expired, own_code, existing_account) |
| `referral_qualified` | The friend's account is created (server-side) | none |
| `referral_reward_granted` | A reward is granted (server-side) | `recipient` (friend, inviter) |
| `referral_reward_expired` | Referral Premium ends (server-side) | `recipient` |
| `premium_purchase` | Existing event, plus a referral flag | `had_referral_reward` (true/false) |

What to watch in the pilot:
- **Funnel:** referral screen views → shares → invite landings → codes applied → accounts created.
- **Value:** how many referred friends and inviters buy Premium after their 30 days end.
- **Cost:** total free Premium days granted.
- **Abuse:** code errors by reason, and spikes in accounts per inviter.

Never sent: names, codes, moods, journal content, or any friend's identity. Rewards and qualification are counted server-side; a share tap is never counted as a referral.

## Decisions to finalize with Evelise
- [x] Confirm reward length: 30 days for both people (decided Nov 2026; previously proposed 7).
- [x] Qualifying action: account creation (decided Nov 2026; previously proposed first check-in).
- [x] Inviter cap: three rewarded referrals, up to 90 days (decided Nov 2026; previously proposed four).
- [x] Redemption window: 30 days (decided Nov 2026).
- [x] Paid subscribers: can invite; no inviter reward in the pilot; their friends still get 30 days (decided Nov 2026).
- [x] Trials and stacking: no friend reward if a trial or paid subscription is already active; inviter rewards run back to back (decided Nov 2026).
- [x] Entry points: sign-up code field, after sign-up/login prompt, Profile/Settings row, one contextual prompt, Home screen spot (decided Nov 2026).
- [x] Contextual prompt moment: after finishing any activity (decided Nov 2026).
- [x] Prompt frequency and guardrails (decided Nov 2026).
- [x] Inviter visibility: counts and status plus each friend's first or display name, with notice at sign-up (decided Nov 2026).
- [x] Main referral screen copy (approved Nov 2026).
- [x] Invited friend's journey copy (approved Nov 2026).
- [x] Inviter confirmation, prompts, expiry and error copy (approved Nov 2026).
- [x] Program terms drafted and approved (Nov 2026).
- [ ] Legal review of program terms before launch.
- [ ] Complete Figma designs and link them here.
- [ ] Create implementation subtasks and determine rollout.

## Acceptance criteria for the future implementation
- [ ] Terms and reward eligibility are visible before participation.
- [ ] The invitation reaches the correct screen with installed/uninstalled paths and manual-code fallback.
- [ ] A qualifying referral grants each eligible reward once, including under retries.
- [ ] Access expiry and cap behavior match final program rules.
- [ ] Existing billing and subscriptions remain accurate; no unintended charge or renewal.
- [ ] Personalization consent stays separate and private activity is not disclosed.
- [ ] Error, expiration, duplicate and paid-subscriber cases follow the completed UX.
