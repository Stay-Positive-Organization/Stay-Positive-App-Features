# Kindness Bingo

**Status:** Feature specification for implementation; not a claim that the feature has shipped.  
**Platforms:** Android (Kotlin) and iOS product behavior; Android implementation tasks are linked below.  
**Access:** Free and Premium.  
**Board:** Card 01 / version `kindness-v1`; 25 activities, fixed 5 × 5 layout, no free square.

## Purpose

Help users practice small acts of kindness toward themselves and others through a self-paced interactive board. The feature extends the original Stay Positive Kindness Bingo PDF into the app.

The retention and feature-discovery benefits are hypotheses to validate after release, not established outcomes. There are no deadlines, weekly resets, penalties, leaderboards, or financial rewards in this version. Activities are completed in everyday life and marked by the user.

## User flow

1. Discover the Kindness Bingo card on Home.
2. Tap **Start Bingo** to open an untouched board.
3. Tap any square to read the activity.
4. Do the activity outside the app, then return and tap **Mark as complete**.
5. See saved progress on the board and Home.
6. Complete a row, column, or full diagonal to see a Bingo celebration.
7. Optionally preview, personalize, share, or save the Bingo image.
8. Return to the same board and continue at the user's pace.

A user may be new to Bingo while already using the rest of the app. Do not replay account onboarding or add a permissions flow just to start Bingo.

## Home entry card

Add this feature to the existing Home layout without replacing mood check-in, daily content, Stories, Words to carry, Explore more, or the existing bottom navigation. Follow the final Figma placement; the simplified Home/navigation shown in early Bingo mockups does not redefine the main Home screen. See [Home Screen](README.md).

| Element | First use |
|---|---|
| Title | Kindness Bingo |
| Supporting line | Small acts. Meaningful moments. |
| Body | Turn everyday kindness into a little adventure. |
| Illustration | Flowing gold heart |
| Primary action | Start Bingo |
| Progress | Hidden before starting |

Once started, use **Continue Bingo** and show the saved completion count and progress. Starting the board and completing an activity are separate events: a returning user may have started with 0 of 25 completed.

After a win, continue to open the same board. Sharing and celebrating do not clear progress.

## Board screen

| Element | Content / behavior |
|---|---|
| Header | Back action, Kindness Bingo, share icon |
| General subtitle | Spread kindness, one small act at a time. |
| First-use help | Your first kindness adventure |
| Instruction | Tap a square, try the activity, then mark it complete. |
| Progress | {completedCount} of 25 completed, percentage, progress bar |
| Column headings | B · I · N · G · O |
| Grid | 5 rows × 5 columns, fixed order below |
| Rule | Complete a row, column, or diagonal to get Bingo. |
| Reassurance | Go at your own pace. Your progress stays saved. |

Share is disabled or hidden until the current board has a valid completed line. Do not show a successful-win share card before a win.

Progress is unique completed activities divided by 25. Examples: 0 = 0%, 5 = 20%, 6 = 24%, 25 = 100%. Five scattered activities are not necessarily Bingo.

### Square states

| State | Appearance and behavior |
|---|---|
| Uncompleted | Light surface with sage outline and readable dark label |
| Selected | Opens the corresponding bottom sheet; selection alone does not complete it |
| Completed | Sage fill, visible checkmark, readable label, completed accessibility state |
| In a winning line | Completed state plus gold highlighting |
| Completed and reopened | Shows completion and a clear Mark as incomplete action |

Use color plus icons/state labels, never color alone. All 25 tiles remain accessible on small screens and at larger text sizes; scroll instead of clipping.

## Activities: exact content and layout

Read left to right, top to bottom. The center is **High five**, not a free square. IDs are stable persistence keys; do not use display text as a key.

| ID | Row | Column | Square label | Description | Prompt |
|---|---|---|---|---|---|
| kindness-01 | 1 | 1 | Hug a loved one | Offer a hug to someone you care about, if you both feel comfortable. A kind message counts too. | Who could use a little warmth today? |
| kindness-02 | 1 | 2 | Do a favor | Make someone’s day easier with a small, thoughtful favor. It doesn’t have to cost anything. | What small task could you help with? |
| kindness-03 | 1 | 3 | Help a neighbor | Offer help with a small task, such as carrying groceries or caring for a plant. | What help could you comfortably offer? |
| kindness-04 | 1 | 4 | Greet someone | Say hello or offer a friendly wave to someone you encounter today. | A simple hello can be enough. |
| kindness-05 | 1 | 5 | Give thanks | Take a moment to notice the kindness others have shown you and express your gratitude. | What is one kind act you’re thankful for? |
| kindness-06 | 2 | 1 | Pick up litter | Leave a shared space a little cleaner. Pick up a safe piece of litter and dispose of it properly. | Choose something safe to handle. |
| kindness-07 | 2 | 2 | Say hello | Greet a neighbor or someone you often see but haven’t spoken to. | You can keep it as simple as “Hi!” |
| kindness-08 | 2 | 3 | Call a friend | Reach out to a friend and make space to really listen. A voice message works too. | Who would you enjoy catching up with? |
| kindness-09 | 2 | 4 | Support local | Encourage a local business with an honest review or a kind message. No purchase needed. | Which local place do you appreciate? |
| kindness-10 | 2 | 5 | Write a thank-you | Let someone know how their kindness made a difference. A short message is enough. | Who made your day a little brighter? |
| kindness-11 | 3 | 1 | Leave a kind note | Write an encouraging note and leave it somewhere appropriate for someone to find. | What words would brighten someone’s day? |
| kindness-12 | 3 | 2 | Check on someone | Reach out to someone who may be having a difficult time. Let them know you care. | “Thinking of you. How are you doing?” |
| kindness-13 | 3 | 3 | High five | Celebrate a small win with someone. Offer a high five if welcome, or a cheerful message. | Whose effort could you celebrate? |
| kindness-14 | 3 | 4 | Share a smile | Offer a warm smile to someone you encounter, when it feels comfortable. | Small moments of warmth count. |
| kindness-15 | 3 | 5 | Send a message | Let someone know you’re thinking of them. There doesn’t need to be a special occasion. | Who came to mind today? |
| kindness-16 | 4 | 1 | Thank a coworker | Recognize something a coworker has done. You can also thank a classmate or collaborator. | What effort did you appreciate? |
| kindness-17 | 4 | 2 | Donate items | If you’re able, give useful items you no longer need to a place that accepts them. | What could be useful to someone else? |
| kindness-18 | 4 | 3 | Volunteer | Offer some time to a cause or community you care about, in a way that fits your capacity. | Where could your time make a difference? |
| kindness-19 | 4 | 4 | Leave kind words | Leave a sincere, encouraging comment on something someone has shared. | What did you appreciate about their work? |
| kindness-20 | 4 | 5 | Give a compliment | Offer a genuine compliment about someone’s effort, kindness, or creativity. | What good quality have you noticed? |
| kindness-21 | 5 | 1 | Ask how they feel | Ask a friend how they’ve been feeling and listen without rushing to offer advice. | “How have you really been lately?” |
| kindness-22 | 5 | 2 | Be kind to yourself | Say something gentle and encouraging to yourself, aloud or silently. | “I deserve patience as I learn and grow.” |
| kindness-23 | 5 | 3 | Choose kindness | In a disagreement, pause and respond with care while keeping your boundaries. | Can you be clear and kind at the same time? |
| kindness-24 | 5 | 4 | Share inspiration | Share something uplifting, helpful, or meaningful with someone who might enjoy it. | What encouraged you recently? |
| kindness-25 | 5 | 5 | Hold the door | Hold a door open for someone when it’s safe and practical. | A small courtesy can brighten a moment. |

The examples intentionally allow free alternatives and respect comfort and boundaries. Do not make spending, physical contact, or responding to someone an obligation.

## Activity detail bottom sheet

Use one reusable component populated from the activity catalog:

1. Dimmed board behind a rounded sheet.
2. Drag handle and close X.
3. Activity-specific icon and title.
4. Description from the table.
5. Static suggestion/prompt card from the table.
6. Helper: **Come back after you’ve done it.**
7. Primary action: **Mark as complete**.
8. Footer: **You can undo this anytime.**

The suggestion is not a journal field or text input. No answer is collected. Do not automatically call, message, open contacts, buy, donate, or post on the user's behalf.

Closing, swiping down, or navigating back leaves completion unchanged. Completion is self-reported; no proof or uploads are required.

On successful completion, update the common saved state and check for new winning lines. Reopening a completed activity offers **Mark as incomplete**. Undo removes that activity from the completed set and recalculates all lines.

Prevent duplicate actions from rapid taps. Present pending/error states honestly and allow retry without discarding previously saved progress.

## Saved progress and account behavior

Use the existing app state/storage architecture rather than introducing a separate backend by default.

Persist:
- Board ID/version.
- Whether the board has been started.
- A unique set of completed activity IDs.
- Acknowledged winning-line identifiers / celebration history.
- Name-sharing preference if that preference is retained.

Restore after navigation, process restart, date changes, and normal app upgrades. Never initialize over an existing board. Isolate account data; switching users must not expose the previous user's progress.

Follow the app's existing local/offline synchronization behavior. Keep pending changes recoverable, show retry on a failed save, and avoid claiming remote sync has completed while offline. Exact storage mechanics and guest-account migration, if relevant to the existing app, are engineering integration decisions; no new authentication step is part of this feature.

Board content updates must preserve or explicitly migrate stable IDs. No silent daily or weekly reset.

## Bingo rules and celebration

There are **12 possible lines**: five rows, five columns, and two complete corner-to-corner diagonals. A line qualifies only when all five of its squares are completed.

On a completion that creates a previously unacknowledged winning line:
- Highlight its squares in gold.
- Show one celebration sheet, even if the action creates multiple lines.
- Keep the original board and completion count.

### Celebration copy

| Element | Copy |
|---|---|
| Illustration | Flowing gold heart with sage/gold confetti |
| Heading | Bingo! |
| Supporting line | Five small acts. A little more kindness. |
| Row body | You completed a row on your Kindness Bingo board. Take a moment to celebrate the care you shared. |
| Column body | You completed a column on your Kindness Bingo board. Take a moment to celebrate the care you shared. |
| Diagonal body | You completed a diagonal on your Kindness Bingo board. Take a moment to celebrate the care you shared. |
| Multiple-line body | You completed multiple lines on your Kindness Bingo board. Take a moment to celebrate the care you shared. |
| First-win chip | Your first Bingo |
| Primary action | Share your Bingo |
| Secondary action | Keep spreading kindness |
| Saved-state footer | Your progress is saved. |

Use the first-win chip only for the first achievement. Later wins must not repeatedly claim to be the first. Show saved-state reassurance only when the persistence state supports it.

After dismissal, the board has a success banner: **Bingo! A little kindness goes a long way.** Supporting text adapts to the line type; row example: **You completed a row. Keep spreading kindness at your own pace.** Include **Share your Bingo** while a valid line exists.

Dismiss via X, back, or Keep spreading kindness without changing completion. Do not replay acknowledged celebrations on screen recomposition, reopening, or relaunch. Undo invalidates affected current lines and highlighting. Historical acknowledgement prevents farming repeated celebrations by undoing and redoing the same line.

At 25/25, keep the full board saved and shareable. This release does not add a reset, new-board flow, or separately designed full-board reward.

## Share preview screen

Accessible from the celebration and the winning-board share actions.

| Element | Content |
|---|---|
| Header | Back action; Share your Bingo |
| Subtitle | A little kindness is worth sharing. |
| Main area | Preview of the actual image that will be exported |
| Preference | Include my first name |
| Name-on helper | Your first name will appear on the shared image. |
| Name-off helper | Your name won’t appear on the shared image. |
| Primary action | Share image |
| Secondary action | Save image |

The preview updates immediately with the switch and must match export. A safe implementation default is name hidden for the first share, retaining an explicit choice if supported; this default was proposed in the Android task and remains subject to product confirmation. The user's ability to switch it on/off is required.

Use only an explicit existing first-name field. Do not derive names from email addresses or guess from full names. If unavailable, use the neutral title and disable/hide the switch with a short explanation. Handle long names by wrapping/scaling within accessible limits rather than clipping.

### Shared image content

The export is a branded image, not a screenshot containing app controls.

| Element | Content |
|---|---|
| Background and decoration | Light brand surface, fine gold border, flowing heart, restrained confetti |
| Main heading | Bingo! |
| Name on | {firstName}’s Kindness Bingo |
| Name off | Kindness Bingo |
| Supporting line | Small acts. Meaningful moments. |
| Achievement text | I completed a line on my Kindness Bingo board. |
| Mini-board | 5 × 5 grid reflecting actual current completion and winning-line position |
| Brand | STAY POSITIVE |
| Footer | Spread kindness, one small act at a time. |

Do not hardcode a top-row win: rows, columns, diagonals, intersecting lines, and other completed tiles must match current state. Activity labels are omitted from the mini-board. No surname, email, journal, mood, prayer text, or activity descriptions appear in the export. Do not invent a website URL or QR code.

### Platform sharing and saving

**Android:** Open the native Android Sharesheet with an image/png content URI and temporary read permission, using FileProvider or the project's equivalent. Save via the appropriate Android media API and minimum required permissions for supported OS versions.

**iOS:** Use the native iOS share sheet and platform-appropriate image-saving behavior when implementing iOS. Early mockups showing AirDrop are iOS examples, not Android requirements.

The user chooses the recipient/app and completes sharing in the operating system. No automatic posting. A canceled share is not a successful post. Report save success only after the image is actually saved. Handle export failure, unavailable targets, retry, and repeated taps without changing board progress.

## Visual system and accessibility

Follow [design-tokens.md](design-tokens.md), current Figma styles, and the app's existing navigation. Early generated mockup hex values are illustrative; current shared tokens take precedence.

- Headings: **Cormorant Garamond**. Supporting/body text: **Montserrat**.
- Use `forest` for primary text/buttons, `warmWhite` and `surface` for backgrounds, `sage` for decorative/completion fills, and `gold` (#B8976A) for decorative accents.
- Do not use sage or decorative gold for small text on light surfaces. Use contrast-safe text tokens, including `goldText` when appropriate.
- On sage-completed squares, choose readable dark labels/checkmarks; do not copy low-contrast white-on-sage text from a concept image.
- Preserve transparent vector assets when converting to Android Vector Drawables.
- Provide accessible button labels, selected/completed square state, and completion announcements.
- Respect platform touch targets, screen-reader focus/dismissal, larger type, and reduced motion.
- Use a static celebration when reduced motion is enabled.

Mockups and SVG assets were created in the design conversation; no canonical Figma URL has been supplied in this specification. Use Eve's final Figma frames/assets for visual handoff. Do not link chat-local filesystem paths in app code or assume they are accessible to developers.

## Verification and acceptance

- [ ] Free and Premium users can start the same 25-activity feature.
- [ ] First-use, started 0/25, partial progress, winning, and 25/25 states work.
- [ ] Every square maps to the correct content and stable ID.
- [ ] Dismissing an activity never completes it.
- [ ] Complete/undo update Home, board, detail, highlights, and export consistently.
- [ ] Saved progress survives next-day use and relaunch without resets.
- [ ] Account switching and failed/offline saves are handled correctly.
- [ ] All 12 lines are detected; four-of-five and scattered-five cases do not win.
- [ ] Multiple simultaneous lines produce one celebration; acknowledged wins do not replay.
- [ ] Name-on/off preview matches export; missing and long names are supported.
- [ ] Export accurately depicts the actual board and excludes private activity content.
- [ ] Native share, cancel, save, failure, retry, and repeated-tap paths are verified.
- [ ] Small-screen, font scaling, contrast, screen-reader, and reduced-motion checks pass.

## Android implementation tasks

| Task | Issue |
|---|---|
| Catalog and visual assets | [#444](https://github.com/Stay-Positive-Organization/Stay-Positive-Kotlin-App/issues/444) |
| Saved progress and completion state | [#445](https://github.com/Stay-Positive-Organization/Stay-Positive-Kotlin-App/issues/445) |
| Home card and board screens | [#446](https://github.com/Stay-Positive-Organization/Stay-Positive-Kotlin-App/issues/446) |
| Activity bottom sheets and undo | [#447](https://github.com/Stay-Positive-Organization/Stay-Positive-Kotlin-App/issues/447) |
| Winning lines and celebration | [#448](https://github.com/Stay-Positive-Organization/Stay-Positive-Kotlin-App/issues/448) |
| Share preview, optional first name, export, and native sharing | [#449](https://github.com/Stay-Positive-Organization/Stay-Positive-Kotlin-App/issues/449) |

App publishing remains with Eve. This document does not create iOS implementation issues or claim that they already exist.

## Remaining handoff details

- Link final Figma frames and production icon assets when available.
- Confirm exact Home card placement in Figma without changing other Home modules.
- Confirm the initial first-name toggle default; the capability to include/hide the name is already specified.
