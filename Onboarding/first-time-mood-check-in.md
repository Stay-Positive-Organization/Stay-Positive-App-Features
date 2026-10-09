# First-Time Mood Check-In and Bible Verse

## Purpose

Give new users a welcoming, meaningful moment before they reach Home. The experience should communicate: **Come as you are. Your feelings are welcome here, and you can start with one small step.**

After account creation, users can choose their mood and receive a Bible verse from a curated collection that matches their selection.

This experience is free for everyone. Users can become Premium later; onboarding does not branch by subscription and does not include an upgrade prompt.

## User flow

1. Complete account creation and any required account setup.
2. Open the first-time mood check-in.
3. Select one mood and tap **Continue**, or tap **Skip for now**.
4. Show **A verse for this moment**.
5. Tap **Continue to Home** to finish onboarding.

Existing users signing in should go through their usual login flow rather than repeat first-time onboarding. Store completion per account so the introduction does not reappear on every launch.

## Screen 1 — Mood check-in

| Element | Content / behavior |
|---|---|
| Small heading | A moment for you |
| Main title | How are you feeling today? |
| Supporting text | Whatever you’re feeling, you’re welcome here. Choose what feels closest to you. |
| Mood grid | Two columns, three rows; an icon and visible label on each card |
| Mood options | Happy, Peaceful, Okay, Sad, Anxious, Overwhelmed |
| Additional option | Full-width **I don’t know** card beneath the grid |
| Primary action | **Continue**; disabled until an option is selected |
| Secondary action | **Skip for now**; always available |

### Selection

- No mood is selected by default.
- Select exactly one option, including **I don’t know**.
- Tapping another card replaces the current selection.
- Use a sage-tinted fill, stronger border, and small checkmark for the selected card.
- Do not rely on color alone. Announce the label and selected state to screen readers.
- Selecting a card alone does not advance the screen.
- Do not add notes, follow-up questions, notification permissions, or Premium setup to this step.

## Screen 2 — Bible verse

| Element | Content / behavior |
|---|---|
| Small heading | A moment of encouragement |
| Main title | A verse for this moment |
| Main content | One Bible verse in a prominent, softly rounded card |
| Attribution | Scripture reference and Bible translation beneath the verse |
| Primary action | Continue to Home |
| Back action | Return to the mood screen to change the selection |

### Verse selection

Use a simple mapping from the explicitly selected mood to an editorially curated verse collection. This feature does not require AI, behavioral analysis, or a Premium subscription.

| Selection | Suggested collection theme |
|---|---|
| Happy | Joy and thanksgiving |
| Peaceful | Peace and trust |
| Okay | Everyday encouragement |
| Sad | Comfort and hope |
| Anxious | Reassurance and trust |
| Overwhelmed | Rest and strength |
| I don’t know | General hope and reassurance |
| Skip for now | General hope and reassurance; no mood recorded |

Themes guide content curation; the final verse collections must be reviewed before release. Use approved Scripture text and always display the reference and translation. Do not generate or rewrite a passage and present it as Scripture.

### Initial mood-to-verse content

Use the following fixed mapping for the first release. All passages use **King James Version (KJV)**. Display the full text below, reference, and translation; do not modernize or paraphrase Scripture in the verse card.

| Selection | Reference | Verse text (KJV) |
|---|---|---|
| Happy | Psalm 118:24 | This is the day which the Lord hath made; we will rejoice and be glad in it. |
| Peaceful | Psalm 29:11 | The Lord will give strength unto his people; the Lord will bless his people with peace. |
| Okay | Psalm 121:2 | My help cometh from the Lord, which made heaven and earth. |
| Sad | Psalm 34:18 | The Lord is nigh unto them that are of a broken heart; and saveth such as be of a contrite spirit. |
| Anxious | Psalm 56:3 | What time I am afraid, I will trust in thee. |
| Overwhelmed | Matthew 11:28 | Come unto me, all ye that labour and are heavy laden, and I will give you rest. |
| I don’t know / Skip for now | Psalm 46:1 | God is our refuge and strength, a very present help in trouble. |

- **I don’t know** and **Skip for now** share a verse but remain distinct responses: skipping records no mood.
- Use Psalm 46:1 (KJV) as the fallback if a mood’s verse cannot be loaded.
- Begin with one verse per mood. Additional reviewed verses can be added to each collection later.
- These mappings provide encouragement; they do not diagnose a mood or promise a particular outcome.

#### Scripture verification sources

- Happy: [Psalm 118:24 (KJV)](https://www.biblegateway.com/passage/?search=Psalm%20118%3A24&version=KJV)
- Peaceful: [Psalm 29:11 (KJV)](https://www.biblegateway.com/passage/?search=Psalm%2029%3A11&version=KJV)
- Okay: [Psalm 121:2 (KJV)](https://www.biblegateway.com/passage/?search=Psalm%20121%3A2&version=KJV)
- Sad: [Psalm 34:18 (KJV)](https://www.biblegateway.com/passage/?search=Psalm%2034%3A18&version=KJV)
- Anxious: [Psalm 56:3 (KJV)](https://www.biblegateway.com/passage/?search=Psalm%2056%3A3&version=KJV)
- Overwhelmed: [Matthew 11:28 (KJV)](https://www.biblegateway.com/passage/?search=Matthew%2011%3A28&version=KJV)
- I don’t know / Skip for now: [Psalm 46:1 (KJV)](https://www.biblegateway.com/passage/?search=Psalm%2046%3A1&version=KJV)

Returning to the mood screen and submitting a different selection updates the verse. Keep the displayed verse stable while the user remains on that screen.

## Relationship to Home and Premium

- This is a **first-time onboarding response**, separate from the daily Home content rules.
- The mood-based onboarding verse is free.
- **Today’s Verse** remains available on Home and continues rotating morning and night.
- Completing onboarding does not replace Today’s Verse with the onboarding verse.
- The existing daily [Home Mood Check-In](../Home/mood-check-in.md) remains its own interaction.
- Premium’s **For your heart today** can be introduced after an upgrade, with the existing personalization consent.
- Choosing a mood here requests a verse for this moment. It must not automatically enable future personalization or set the Premium consent switch.

## Visual design

Match the existing welcome and account screens:

- Warm cream background, sage green accents, dark green text, and subtle gold details.
- Elegant serif headings and readable sans-serif body text.
- Rounded cards, gentle line icons, and generous spacing.
- Keep the main choices and actions visible on typical phone sizes; support scrolling on smaller screens or with larger text.
- Touch targets at least 44 × 44, accessible contrast, and support for enlarged text.
- No ads or upgrade prompts on either screen.

## Persistence and integration

- Store whether first-time onboarding has been completed; mark it complete when **Continue to Home** is tapped.
- A skipped check-in must not create a mood entry or be treated as **I don’t know**.
- If saving a submitted mood, store its timestamp and onboarding origin and reuse the app’s check-in persistence rather than creating duplicate entries on retry.
- Coordinate the shared mood model with Home before implementation: Home currently uses **Grateful** and **Discouraged**, while this onboarding design uses **Happy** and **Sad**. These labels must not be silently treated as equivalent. Ensure the final model and same-day Home display handle onboarding selections consistently.
- Follow the existing [Privacy and Safety](../Home/Privacy%20and%20Safety.md) rules for mood storage, account deletion, and future personalization.

## Loading and failure states

- If a collection has no available verse, use an approved general encouragement verse.
- Prefer bundled or cached approved content so a network failure does not block the verse screen.
- If no verse can be displayed, offer **Retry** and keep **Continue to Home** available.
- If saving fails, show a clear retry message and never present an unsaved check-in as saved. Users must still be able to reach Home.
- Disable duplicate submissions while an action is processing.

## Acceptance criteria

- [ ] New users see the mood screen after account setup and before Home.
- [ ] Everyone receives the same free onboarding experience.
- [ ] All six mood cards and **I don’t know** are selectable.
- [ ] Only one option can be selected; its state is visually and accessibly clear.
- [ ] Continue requires a selection; Skip remains available.
- [ ] A selected mood produces a verse from the matching approved collection.
- [ ] Unknown and skipped responses show a general verse; skipping records no mood.
- [ ] Verse text, reference, and translation appear together.
- [ ] Back allows the user to change their mood and receive the corresponding verse.
- [ ] Continue to Home completes onboarding and opens Home.
- [ ] Onboarding does not repeat for a completed account.
- [ ] Home’s morning/night Today’s Verse remains available.
- [ ] No Premium purchase or future-personalization consent is required or automatically enabled.
- [ ] Save and content failures do not prevent entry to Home.
- [ ] Shared mood identifiers and same-day Home behavior are resolved before implementation.
