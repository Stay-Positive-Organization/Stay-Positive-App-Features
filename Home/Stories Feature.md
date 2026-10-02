## 3.3 Story Interactions

Users should be able to interact with Stories through:

- Like
- Comment
- Share

### Like

Users can like a Story to show that the Story resonated with them.

Requirements:

- A signed-in user can like a Story.
- A user can only have one active like per Story.
- Tapping Like again removes the user's like.
- The Story should display the total number of likes.
- The user's Like state should persist across sessions.
- Like counts should update appropriately when a Like is added or removed.

### Comments

Users can leave comments on Stories.

Requirements:

- Signed-in users can post comments.
- Comments should be associated with both the Story and the user.
- Users should be able to view comments left on a Story.
- Each comment should display:
  - User display name
  - Comment text
  - Timestamp
- Users should be able to delete their own comments.
- Comments should be displayed in a consistent order.
- Empty comments should not be accepted.
- Appropriate validation should be applied before a comment is submitted.

### Community Safety

Because comments introduce user-generated content, the implementation should account for moderation and community safety.

At minimum:

- Users should be able to report inappropriate comments.
- Stay Positive should be able to remove comments.
- Stay Positive should be able to disable comments on an individual Story if necessary.
- Deleted or moderated comments should no longer appear publicly.

More advanced moderation can be introduced as the community grows.

---

## 6. Content Model

A Story should support at least the following fields:

| Field | Type | Required | Description |
|---|---|---|---|
| `id` | String | Yes | Unique Story identifier |
| `title` | String | Yes | Story title |
| `content` | String | Yes | Full Story content |
| `excerpt` | String | Yes | Short Home Screen preview |
| `imageUrl` | String / null | No | Story image |
| `authorName` | String / null | No | Public-facing author name |
| `publishedAt` | Timestamp | Yes | Publication date |
| `isPublished` | Boolean | Yes | Controls visibility |
| `isFeatured` | Boolean | No | Allows editorial featuring |
| `commentsEnabled` | Boolean | Yes | Determines whether users can comment |
| `createdAt` | Timestamp | Yes | Creation timestamp |
| `updatedAt` | Timestamp | Yes | Last update timestamp |

### Story Like

A Like should associate:

- `storyId`
- `userId`
- `createdAt`

The backend should prevent duplicate active Likes from the same user on the same Story.

### Story Comment

A Comment should support:

| Field | Type | Required | Description |
|---|---|---|---|
| `id` | String | Yes | Unique comment identifier |
| `storyId` | String | Yes | Story being commented on |
| `userId` | String | Yes | User who created the comment |
| `content` | String | Yes | Comment text |
| `createdAt` | Timestamp | Yes | Creation timestamp |
| `updatedAt` | Timestamp | No | Last edit timestamp, if editing is later supported |
| `isDeleted` | Boolean | Yes | Controls whether the comment remains visible |

---

## 9. Analytics

Analytics should be implemented from the first release so engagement and retention can be evaluated.

### Recommended Events

| Event | Trigger |
|---|---|
| `story_impression` | Story card becomes visible |
| `story_open` | User opens a Story |
| `story_like` | User likes a Story |
| `story_unlike` | User removes their Like |
| `story_comment_create` | User posts a comment |
| `story_comment_delete` | User deletes their comment |
| `story_comment_report` | User reports a comment |
| `story_share_tap` | User taps Share |
| `story_share_link_open` | Shared Story link is opened |
| `story_read_complete` | User reaches a defined completion threshold |
| `story_deep_link_open` | App opens directly to a Story from a link |

---

## 11. MVP Scope

### Include

- Stories section on Home Screen
- Featured Story card
- Story detail screen
- Published Story retrieval
- Daily/dynamic Story rotation
- Like Stories
- Unlike Stories
- Like count
- View Story comments
- Add comments
- Delete own comments
- Report inappropriate comments
- Admin ability to remove comments
- Ability to disable comments on a Story
- Share button
- Unique Story links
- App deep-link handling
- Web/fallback handling for recipients without the app
- Core analytics events
- Team-managed Story content

### Not Required for MVP

- AI-generated Stories
- Personalized Story recommendations
- User-generated Story publishing
- Comment replies/threads
- Following users/authors
- Direct messaging
- Social feeds
- Complex recommendation algorithms
- Premium-only Story personalization

---

## 12. Acceptance Criteria

The feature is ready for initial release when:

1. A published Story appears in the Home Screen Stories section.
2. The user can open and read the complete Story.
3. The featured Story rotates according to the defined cadence.
4. The Story does not unexpectedly change during the same daily period.
5. Unpublished Stories are never displayed.
6. A signed-in user can Like and Unlike a Story.
7. A user cannot create duplicate Likes on the same Story.
8. The correct Like count is displayed.
9. A signed-in user can post a valid comment.
10. Users can view comments on a Story.
11. Users can delete their own comments.
12. Users cannot delete another user's comments.
13. Users can report inappropriate comments.
14. Stay Positive can remove inappropriate comments.
15. Comments can be disabled for an individual Story.
16. The user can share a Story through the native share sheet.
17. Every shareable Story has a unique link.
18. A Story link opens the corresponding Story in Stay Positive when supported.
19. A recipient without the app receives a functional fallback experience.
20. Core Story analytics events are recorded.
21. Free and Premium users can access the core Stories experience.