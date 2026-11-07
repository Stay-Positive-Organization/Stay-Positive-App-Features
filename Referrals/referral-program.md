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

**Pilot offer (decided by Evelise): give 30 days of Premium to the invited friend and 30 days to the inviter after the friend qualifies.** Eligibility, limits and paid-subscriber treatment below are proposals to refine during UX/product work, not final launch terms.

Thirty days gives both people enough time to use Premium as part of a routine, not just sample it. Because the reward is larger, the cap, redemption window and misuse protections below matter more. Whether it improves activation, retention or conversion remains a hypothesis to measure. Do not describe the program as proven growth.

| Participant | Proposed benefit | Proposed trigger |
|---|---|---|
| Invited friend | 30 days of complimentary Premium, once per new account | Creates an eligible new account through the referral |
| Inviter | 30 days of complimentary Premium per qualifying friend | The same referral qualifies; one reward per friend |

**Qualifying action (decided by Evelise): account creation.** A referral qualifies when an eligible new account is created with the referral applied; no check-in or other in-app activity is required. Because this is a low bar for a 30-day reward, the one-reward-per-account rule, inviter cap and duplicate/self-referral protections are what limit misuse. The inviter never sees the friend's moods or other activity.

## Proposed pilot rules
- Free users can invite friends. Premium subscribers may also invite, but reward handling for active paid subscriptions must be resolved before including them in reward eligibility.
- A qualifying friend is a new Stay Positive account with one valid referral applied during sign-up, before the account is created. A code entered after account creation does not qualify. Existing accounts cannot claim a new-user reward.
- Sharing, clicking a link or installing alone does not earn a reward.
- Invited friend reward: one 30-day grant per eligible new account.
- Inviter reward: proposed pilot cap of four qualifying friends (120 reward days total per inviter). Show remaining eligibility clearly; finalize the cap before launch.
- Proposed redemption window: the friend creates their account within 30 days of accepting the invitation. Finalize timing and precise expiry behavior before launch.
- One friend can credit only one inviter; proposed rule is the first valid referral confirmed by the friend. Do not overwrite it silently.
- Self-referrals, duplicate claims and repeated processing must not create additional grants.
- Complimentary access requires no payment details and does not start an automatically renewing subscription.
- When complimentary access ends, return to the user's underlying entitlement. Keep journal entries, favorites and other saved content; gate Premium features according to normal app rules.
- Personalization and device notifications remain separate opt-ins. Receiving Premium must not enable either automatically.
- Rewards are access to features, with no cash value or cash redemption.

## Access timing and existing subscriptions
For a Free user, proposed reward access starts when the referral qualifies. If another referral reward is already active, append days after its expiry rather than running overlapping grants.

An active paid subscription must not be silently paused, canceled, discounted or described as extended. Define a compatible way to deliver an equivalent benefit to paid subscribers before enabling their reward claims. Possible approaches to evaluate include a deferred complimentary-access grant after paid access ends or a supported subscription offer. This is an open product/engineering decision; do not promise a billing credit.

Also resolve interactions with existing trials/promotions, restoring purchases, refunds, account changes and platform changes. Referral access should follow the same account entitlement across supported devices without duplicating rewards.

## Suggested entry point and screens
Suggested entry point: Profile/Settings row **Invite a friend**.

### 1. Main referral screen
Draft copy, conditional on final offer:
- Title: **Share a little encouragement**
- Supporting line: **Invite a friend to Stay Positive. When they create their account, you both get 30 days of Premium.**
- Personal link/code with **Copy link** and **Invite a friend** actions.
- Brief "How it works": share your link → friend creates an account → both receive Premium.
- Reward summary: earned days, active access end date and remaining referral eligibility.
- Program terms link with eligibility, reward cap and expiry details.
- Avoid contact uploads or automatic invitations; open the native share sheet so the person chooses whom to invite.

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
Use aggregate counts/status without exposing friends' moods, journal text, chat, purchases or other private activity. Prefer anonymous referral rows.

### 4. Required UX states
- First use with no referrals.
- Link copied and share-sheet return. Share-sheet return is not proof of a sent invitation.
- Pending referral; qualifying event awaiting processing.
- Reward granted; access expired.
- Invalid/expired code, self-referral, existing account, duplicate claim.
- Reward cap reached, offline/save failure and program unavailable.
- Paid-subscriber eligibility explanation once that policy is resolved.

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
- [ ] Confirm four-referral pilot cap and 30-day redemption window.
- [ ] Resolve paid subscribers, trials and promotion stacking.
- [ ] Finalize rules, terms, entry point and screen copy.
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
