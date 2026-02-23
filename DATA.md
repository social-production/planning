# Social Production Data

## Database Schema and Relationships

### Diagrams

#### Entity Relationship Diagram

```mermaid
erDiagram
    USERS {
        string id PK "device/mobile ID"
        string display_name
        string password_hash
        timestamptz created_at
        timestamptz updated_at
        timestamptz deleted_at
    }

    ASSETS {
        uuid id PK
        string name
        string mime_type
        string owner_id FK "polymorphic"
        string owner_type "user | post"
        timestamptz created_at
        timestamptz updated_at
        timestamptz deleted_at
    }

    CONTENT {
        uuid id PK
        text content
        string parent_type "post | comment | event | update | proposal"
        string parent_id FK "polymorphic"
        timestamptz created_at
        timestamptz updated_at
        timestamptz deleted_at
    }

    VOTES {
        uuid id PK
        string user_id FK
        string indicator "up | down"
        string resource_type "post | comment | council"
        string resource_id FK "polymorphic"
        timestamptz created_at
        timestamptz updated_at
        timestamptz deleted_at
    }

    TAGS {
        uuid id PK
        string name
    }

    POST_TAGS {
        uuid post_id FK
        uuid tag_id FK
    }

    POSTS {
        uuid id PK
        string title
        string project_type "production | service | living_condition"
        string project_location
        string project_status "researching | funding | producing | completed | cancelled | distributed"
        string type "project | post"
        string user_id FK
        timestamptz created_at
        timestamptz updated_at
        timestamptz deleted_at
    }

    POST_UPDATES {
        uuid id PK
        uuid post_id FK
        string user_id FK
        timestamptz created_at
        timestamptz updated_at
        timestamptz deleted_at
    }

    POST_MEMBERS {
        uuid id PK
        string user_id FK
        uuid post_id FK
        string role "manager | member"
        timestamptz created_at
        timestamptz updated_at
        timestamptz deleted_at
    }

    POST_PROPOSALS {
        uuid id PK
        string title
        string user_id FK
        uuid post_id FK
        string status "proposed | approved | not_approved | cancelled"
    }

    POST_EVENTS {
        uuid id PK
        uuid post_id FK
        string status "planned | completed | cancelled"
        text location
        timestamptz start_time
        timestamptz end_time
        timestamptz created_at
        timestamptz updated_at
        timestamptz deleted_at
    }

    RSVPS {
        uuid id PK
        string response "yes | no | maybe"
        string user_id FK
        uuid post_event_id FK
        timestamptz created_at
        timestamptz updated_at
    }

    POST_FUND_DRIVES {
        uuid id PK
        uuid post_id FK
        string title
        string status "funding | funded | cancelled"
        timestamptz start_time
        timestamptz end_time
        timestamptz created_at
        timestamptz updated_at
        timestamptz deleted_at
    }

    POST_FUNDS {
        uuid id PK
        string currency
        decimal amount
        string status "funded | withdrawn | cancelled"
        string user_id FK
        uuid post_fund_drive_id FK
        timestamptz created_at
        timestamptz updated_at
        timestamptz deleted_at
    }

    CHANNELS {
        uuid id PK
        string name
        varchar icon
    }

    CHANNEL_POSTS {
        uuid channel_id FK
        uuid post_id FK
    }

    USERS ||--o{ POSTS : "creates"
    USERS ||--o{ POST_MEMBERS : "joins as"
    USERS ||--o{ POST_UPDATES : "writes"
    USERS ||--o{ POST_PROPOSALS : "submits"
    USERS ||--o{ RSVPS : "makes"
    USERS ||--o{ POST_FUNDS : "contributes"
    USERS ||--o{ VOTES : "casts"

    POSTS ||--o{ POST_MEMBERS : "has"
    POSTS ||--o{ POST_UPDATES : "has"
    POSTS ||--o{ POST_PROPOSALS : "has"
    POSTS ||--o{ POST_EVENTS : "has"
    POSTS ||--o{ POST_FUND_DRIVES : "has"
    POSTS ||--o{ POST_TAGS : "tagged with"

    TAGS ||--o{ POST_TAGS : "applied via"

    POST_EVENTS ||--o{ RSVPS : "receives"
    POST_FUND_DRIVES ||--o{ POST_FUNDS : "collects"

    CHANNELS ||--o{ CHANNEL_POSTS : "contains"
    POSTS ||--o{ CHANNEL_POSTS : "listed in"
```

#### Polymorphic Associations

These three tables use `type`/`id` pairs to associate with multiple parent entities.

```mermaid
erDiagram
    ASSETS {
        uuid id PK
        string owner_type "user | post"
        string owner_id FK
    }

    CONTENT {
        uuid id PK
        string parent_type "post | comment | event | update | proposal"
        string parent_id FK
    }

    VOTES {
        uuid id PK
        string resource_type "post | comment | council"
        string resource_id FK
        string user_id FK
    }

    USERS {
        string id PK
    }

    POSTS {
        uuid id PK
    }

    POST_UPDATES {
        uuid id PK
    }

    POST_PROPOSALS {
        uuid id PK
    }

    POST_EVENTS {
        uuid id PK
    }

    POST_FUND_DRIVES {
        uuid id PK
    }

    USERS ||--o{ ASSETS : "owns (owner_type=user)"
    POSTS ||--o{ ASSETS : "owns (owner_type=post)"
    POST_EVENTS ||--o{ ASSETS : "owns (owner_type=post_event)"
    POST_FUND_DRIVES ||--o{ ASSETS : "owns (owner_type=post_fund_drive)"

    POSTS ||--o{ CONTENT : "has (parent_type=post)"
    POST_UPDATES ||--o{ CONTENT : "has (parent_type=update)"
    POST_PROPOSALS ||--o{ CONTENT : "has (parent_type=proposal)"
    POST_EVENTS ||--o{ CONTENT : "has (parent_type=event)"

    POSTS ||--o{ VOTES : "receives (resource_type=post)"
    POST_PROPOSALS ||--o{ VOTES : "receives (resource_type=council)"
    USERS ||--o{ VOTES : "casts"
```

### Users

- Have
  - An ID using the computer or mobile device ID
  - A display name
  - A password hash
  - A created at timestamp with time zone
  - An updated at timestamp with time zone
  - A deleted at timestamp with time zone

### Assets

- Have
  - An ID using UUID
  - A name
  - An application mime type
  - An owner ID
  - An owner type (user, post)
  - A created at timestamp with time zone
  - An updated at timestamp with time zone
  - A deleted at timestamp with time zone

### Content

- Have
  - An ID using UUID
  - A content field using text
  - A parent type (post, comment, event, update, proposal)
  - A parent ID
  - A created at timestamp with time zone
  - An updated at timestamp with time zone
  - A deleted at timestamp with time zone

### Votes

- Have
  - An ID using UUID
  - A user ID
  - An indicator (up, down)
  - A resource type (post, comment, council)
  - A resource ID
  - A created at timestamp with time zone
  - An updated at timestamp with time zone
  - A deleted at timestamp with time zone

### Tags

- Have
  - An ID using UUID
  - A name
  - Many posts

### Posts

- Have
  - An ID using UUID
  - A title
  - A project type (production, service, living condition)
  - A project location
  - A project status (researching, funding, producing, completed, cancelled, distributed)
  - A type (project, post)
  - A created at timestamp with time zone
  - An updated at timestamp with time zone
  - A deleted at timestamp with time zone
  - Many assets
  - Many votes
  - One content
  - A user ID
  - Many tags

### Post Updates

- Have
  - An ID using UUID
  - A post ID
  - A user ID
  - One content
  - A created at timestamp with time zone
  - An updated at timestamp with time zone
  - A deleted at timestamp with time zone

### Post Members

- Have
  - An ID using UUID
  - A user ID
  - A post ID
  - A role (manager, member)
  - A created at timestamp with time zone
  - An updated at timestamp with time zone
  - A deleted at timestamp with time zone

### Post Proposals

- Have
  - An ID using UUID
  - A title
  - A user ID
  - One content
  - Many votes
  - A status (proposed, approved, not approved, cancelled)

### RSVPs

- Have
  - An ID using UUID
  - A response (yes, no, maybe)
  - A user ID
  - A post event ID
  - A created at timestamp with time zone
  - An updated at timestamp with time zone

### Post Events

- Have
  - An ID using UUID
  - A post ID
  - A status (planned, completed, cancelled)
  - A location using text
  - Many RSVPs
  - A created at timestamp with time zone
  - An updated at timestamp with time zone
  - A deleted at timestamp with time zone
  - A start time as a timestamp with time zone
  - An end time as a timestamp with time zone
  - One content
  - Many assets

### Post Funds

- Have
  - An ID using UUID
  - A currency
  - An amount
  - A status (funded, withdrawn, cancelled)
  - A user ID
  - A post fund drive ID
  - A created at timestamp with time zone
  - An updated at timestamp with time zone
  - A deleted at timestamp with time zone

### Post Fund Drives

- Have
  - An ID using UUID
  - A post ID
  - A title
  - A status (funding, funded, cancelled)
  - One content
  - Many assets
  - Many post funds
  - A start timestamp with time zone
  - An end timestamp with time zone
  - A created at timestamp with time zone
  - An updated at timestamp with time zone
  - A deleted at timestamp with time zone

### Channels

- Have
  - An ID using UUID
  - A name
  - An icon using varchar(255)
  - Many posts
