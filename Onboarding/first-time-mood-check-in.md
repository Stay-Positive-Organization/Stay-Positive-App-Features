# First-Time Onboarding: Date of Birth, Mood Check-In and Bible Verse

> **Source of truth:** the Figma file [Stay-Positive-App](https://www.figma.com/design/IICrUhTo29kVu3ANnwPG9H), section **Version 3.0**, frames **Enter DOB**, **Mood Check-In**, **Mood Check-In Selected** and **A verse for this moment**. If this document and Figma disagree, Figma wins; update this document to match.
>
> **Bible translation:** all Scripture in this flow uses the **New International Version (NIV)**.

## Purpose

Give new users a welcoming, meaningful moment before they reach Home. The experience should communicate: **Come as you are. Your feelings are welcome here, and you can start with one small step.**

After account creation, users enter their date of birth, choose their mood, and receive a Bible verse from a curated collection that matches their selection.

This experience is free for everyone. Users can become Premium later; onboarding does not branch by subscription and does not include an upgrade prompt.

## User flow

```
Create account (email or Google) → Date of Birth → Mood Check-In → A verse for this moment → Home
```

1. Create an account with email (**Create Account** screen) or Google (**Sign up with Google**).
2. Enter date of birth and tap **Save & Continue**.
3. Select one mood and tap **Continue**, or tap **Skip intro**.
4. Show **A verse for this moment**.
5. Tap **Continue to Home →** to finish onboarding.

### Who sees it

| User | Flow |
|---|---|
| New email account | Full flow |
| New Google account (first sign-up, `isNewUser == true`) | Full flow |
| Returning Google user | Straight to Home |
| Existing user logging in (email or Google) | Straight to Home |
| Account that already completed onboarding | Straight to Home |

Store completion per account so the flow does not reappear on every launch or after sign-out/sign-in. Keep this completion state separate from the pre-signup welcome-introduction pager (Welcome Screens 6–10).

## Screen 1 — Date of Birth

| Element | Content / behavior |
|---|---|
| Small heading | PROFILE SETUP |
| Main title | Date of Birth |
| Supporting text | Help us personalize your wellness journey. |
| Picker | Three wheels: MONTH, DAY, YEAR |
| Primary action | **Save & Continue** |
| Secondary action | None in the design; there is no skip on this screen |

- Reuse the existing `dialog_enter_dob.xml` layout and picker logic from `EnterDobBottomSheet`, presented as a full screen in this flow (the Profile page keeps using the bottom sheet).
- Save to the same `dob` field the Profile page uses (`MM/DD/YYYY`) so both places stay in sync.
- The day wheel adjusts to the selected month and year (no invalid dates such as February 31).
- If saving fails, show a clear retry message and stay on the screen.

## Screen 2 — Mood check-in

| Element | Content / behavior |
|---|---|
| Small heading | A moment for you |
| Main title | How are you feeling today? |
| Supporting text | Whatever you’re feeling, you’re welcome here. Choose what feels closest to you. |
| Mood grid | Three columns, two rows; an icon and visible label on each card |
| Mood options (grid order) | Anxious, Discouraged, Overwhelmed, Okay, Peaceful, Grateful |
| Additional option | Full-width **I don’t know** card beneath the grid |
| Primary action | **Continue**; disabled until an option is selected (see **Mood Check-In** vs **Mood Check-In Selected** in Figma) |
| Secondary action | **Skip intro**; always available |

These are the same seven moods as the Home mood check-in and the `Mood` enum (`ANXIOUS`, `DISCOURAGED`, `OVERWHELMED`, `OKAY`, `PEACEFUL`, `GRATEFUL`, `UNKNOWN`). Onboarding and Home share one mood model; no mapping between different labels is needed.

### Selection

- No mood is selected by default.
- Select exactly one option, including **I don’t know**.
- Tapping another card replaces the current selection.
- Use the mood’s tinted fill, stronger border and bold label for the selected card, as in **Mood Check-In Selected**.
- Do not rely on color alone. Announce the label and selected state to screen readers.
- Selecting a card alone does not advance the screen.
- Do not add notes, follow-up questions, notification permissions, or Premium setup to this step.

## Screen 3 — Bible verse

| Element | Content / behavior |
|---|---|
| Small heading | A moment of encouragement |
| Main title | A verse for this moment |
| Supporting text | Take a breath and let these words meet you where you are. |
| Main content | One verse card (dark green, quote mark, branch illustration) with the verse text |
| Attribution | Reference and translation beneath the verse, e.g. **Psalm 46:1 · NIV** |
| Card action | **Read full chapter >** opens the in-app Bible reader at that chapter |
| Primary action | **Continue to Home →** |
| Back action | Return to the mood screen to change the selection |

The Figma frame shows the **I don’t know / skipped** example (Psalm 46:1). There is one verse card on this screen; it is not the Home **Today’s Verse**.

### Mood-to-verse content

Fixed mapping for the first release. All passages are **NIV**. Display the full text below, the reference and the translation; do not modernize or paraphrase Scripture.

| Selection | Theme | Reference | Verse text (NIV) |
|---|---|---|---|
| Anxious | Reassurance and trust | Psalm 56:3 | When I am afraid, I put my trust in you. |
| Discouraged | Hope when downcast | Psalm 42:11 | Why, my soul, are you downcast? Why so disturbed within me? Put your hope in God, for I will yet praise him, my Savior and my God. |
| Overwhelmed | Rest and strength | Matthew 11:28 | Come to me, all you who are weary and burdened, and I will give you rest. |
| Okay | Everyday encouragement | Psalm 121:2 | My help comes from the Lord, the Maker of heaven and earth. |
| Peaceful | Peace and trust | Psalm 29:11 | The Lord gives strength to his people; the Lord blesses his people with peace. |
| Grateful | Thanksgiving | Psalm 107:1 | Give thanks to the Lord, for he is good; his love endures forever. |
| I don’t know / Skip intro | General hope and reassurance | Psalm 46:1 | God is our refuge and strength, an ever-present help in trouble. |

- **I don’t know** and **Skip intro** share a verse but remain distinct responses: skipping records no mood.
- Use Psalm 46:1 (NIV) as the fallback if a mood’s verse cannot be loaded.
- Begin with one verse per mood. Additional reviewed verses can be added later.
- Use approved Scripture text only. Do not generate or rewrite a passage and present it as Scripture.
- These mappings offer encouragement; they do not diagnose a mood or promise an outcome.
- Returning to the mood screen and submitting a different selection updates the verse. Keep the displayed verse stable while the user stays on the screen.

#### Scripture verification sources

- Anxious: [Psalm 56:3 (NIV)](https://www.biblegateway.com/passage/?search=Psalm%2056%3A3&version=NIV)
- Discouraged: [Psalm 42:11 (NIV)](https://www.biblegateway.com/passage/?search=Psalm%2042%3A11&version=NIV)
- Overwhelmed: [Matthew 11:28 (NIV)](https://www.biblegateway.com/passage/?search=Matthew%2011%3A28&version=NIV)
- Okay: [Psalm 121:2 (NIV)](https://www.biblegateway.com/passage/?search=Psalm%20121%3A2&version=NIV)
- Peaceful: [Psalm 29:11 (NIV)](https://www.biblegateway.com/passage/?search=Psalm%2029%3A11&version=NIV)
- Grateful: [Psalm 107:1 (NIV)](https://www.biblegateway.com/passage/?search=Psalm%20107%3A1&version=NIV)
- I don’t know / Skip intro: [Psalm 46:1 (NIV)](https://www.biblegateway.com/passage/?search=Psalm%2046%3A1&version=NIV)

## Relationship to Home and Premium

- This is a **first-time onboarding response**, separate from the daily Home content rules.
- The mood-based onboarding verse is free.
- **Today’s Verse** remains on Home and keeps rotating morning and night. The onboarding verse does not replace it.
- The onboarding mood is a real check-in: it uses the same storage as the [Home Mood Check-In](../Home/mood-check-in.md) with source `ONBOARDING`, so Home shows it as today’s mood.
- Premium’s **For your heart today** can be introduced after an upgrade, with the existing personalization consent.
- Choosing a mood here must not automatically enable future personalization or set the Premium consent switch.

## Visual design

Match Figma **Version 3.0** and the existing welcome and account screens:

- Warm cream background, sage green accents, dark green text, and subtle gold details.
- Fonts: Alegreya for titles and verse text, Montserrat for body text, Cormorant Garamond Bold for buttons.
- Rounded cards, gentle line icons, and generous spacing.
- Keep the main choices and actions visible on typical phone sizes; support scrolling on smaller screens or with larger text.
- Touch targets at least 48 × 48 dp, accessible contrast, and support for enlarged text.
- No ads or upgrade prompts on any of these screens.

## Persistence and integration

- Mark first-time onboarding complete when **Continue to Home →** is tapped.
- If the app is closed mid-flow, the next launch resumes at the first unfinished step (DOB if no `dob` is saved, otherwise the mood check-in).
- A skipped check-in must not create a mood entry or be treated as **I don’t know**.
- A submitted mood is saved with its timestamp and `source = ONBOARDING`, reusing the check-in storage; retries must not create duplicate entries.
- Follow the existing [Privacy and Safety](../Home/Privacy%20and%20Safety.md) rules for mood storage, account deletion, and future personalization.

## Loading and failure states

- Bundle the seven verses in the app so a network failure never blocks the verse screen.
- If saving the mood fails, show a clear retry message and never present an unsaved check-in as saved. Users must still be able to reach Home.
- Disable duplicate submissions while an action is processing.

## Acceptance criteria

- [ ] New email accounts and new Google accounts see DOB → Mood Check-In → Verse before Home.
- [ ] Existing users logging in, returning Google users and completed accounts go straight to Home.
- [ ] DOB is saved to the same `dob` field used by the Profile page.
- [ ] All six mood cards and **I don’t know** are selectable; only one at a time; state is visually and accessibly clear.
- [ ] Continue requires a selection; **Skip intro** is always available and records no mood.
- [ ] Each response shows its mapped NIV verse, full text, reference and “NIV” label.
- [ ] Back lets the user change their mood and see the matching verse.
- [ ] **Continue to Home →** completes onboarding and opens Home.
- [ ] The onboarding mood appears as today’s mood on Home.
- [ ] Home’s morning/night Today’s Verse is unchanged.
- [ ] No Premium purchase or personalization consent is required or automatically enabled.
- [ ] Save and content failures do not prevent entry to Home.
