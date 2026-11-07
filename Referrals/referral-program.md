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
- Proposed, to confirm: the inviter's reward is unaffected, because the friend still created an eligible new account.
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
Draft heading: **A little encouragement, shared with you**
Explain the 30-day reward and qualifying action before account creation.
- Link with app installed: open the referral acceptance route.
- Link without the app: show an invitation page with the correct available store destination and a visible code to enter after installation.
- Do not assume referral attribution survives a store install; define and test the link/code handoff. Provide manual code entry as fallback.
- Confirm an applied referral visibly; an invalid code must not prevent ordinary onboarding.
- Apply the referral before account creation, then continue the existing onboarding flow unchanged.
- Record qualification once when the account is created; show the friend's reward confirmation once onboarding allows it.

### 3. Progress and reward confirmation
Draft success title: **Your 30 days of Premium are ready**
Show exact access end date and **Explore Premium**.
Show pending, qualified and reward-granted states as needed.
What the inviter sees (decided by Evelise):
- **Counts and status:** for example "2 friends joined · 2 of 3 rewards earned · Premium until Dec 12".
- **A row per friend with their first name or display name:** for example "Sarah joined · reward granted" or "Sarah joined · no reward (cap reached)".
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

## Developer handoff scope
After the rules and UX are ready, create separate tasks for:
1. Android referral screen, sharing, code entry, routing and onboarding integration.
2. Backend attribution, eligibility, qualification, one-time reward grants, account entitlements and expiry.
3. Invitation web fallback and app/store routing; coordinate iOS when ready.
4. Tests for retries, offline recovery, repeated links, duplicate qualification and purchase/reward interactions.

Use server-side eligibility and reward calculations; never rely on client-only counters. Keep an auditable grant record and make repeated qualification requests idempotent. Use non-identifying random referral codes.

## Measurement
Track referral screen views, share action initiated, invitation landing, referral applied, qualification, reward granted/expired and subsequent Premium purchase. Measure referred-user activation and retention, plus reward cost and misuse, before expanding the offer. Do not send mood values or private content in referral analytics.

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
- [ ] Finalize remaining screen copy and program terms.
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
