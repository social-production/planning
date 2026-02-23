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

    USER_ADDRESSES {
        uuid id PK
        string user_id FK
        string name
        string address_line_1
        string address_line_2
        string city
        string state
        string postal_code
        timestamptz created_at
        timestamptz updated_at
        timestamptz deleted_at
    }

    USER_EMAILS {
        uuid id PK
        string user_id FK
        string name
        string address
        timestamptz created_at
        timestamptz updated_at
        timestamptz deleted_at
    }

    ASSETS {
        uuid id PK
        string name
        string mime_type
        string owner_id FK "polymorphic"
        string owner_type "user | post | product | product_link"
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

    PRODUCTS {
        uuid id PK
        uuid post_id FK "project post"
        string name
        decimal amount
        timestamptz created_at
        timestamptz updated_at
        timestamptz depleted_at
    }

    PRODUCT_LINKS {
        uuid id PK
        string name
        uuid product_id FK
        uuid product_distribution_id FK
        uuid asset_id FK
        boolean downloaded
    }

    PRODUCT_DISTRIBUTIONS {
        uuid id PK
        string user_id FK
        uuid product_id FK
        decimal amount
        timestamptz created_at
        timestamptz updated_at
    }

    PRODUCT_DISTRIBUTION_STATUSES {
        uuid id PK
        uuid product_distribution_id FK
        string status "preparing | shipped | received | downloaded | cancelled | returned"
        timestamptz created_at
    }

    PRODUCT_DISTRIBUTION_ADDRESSES {
        uuid id PK
        uuid product_distribution_id FK
        string addressable_type "user_address | user_email | product_link"
        string addressable_id FK "polymorphic"
    }

    USERS ||--o{ USER_ADDRESSES : "has"
    USERS ||--o{ USER_EMAILS : "has"
    USERS ||--o{ POSTS : "creates"
    USERS ||--o{ POST_MEMBERS : "joins as"
    USERS ||--o{ POST_UPDATES : "writes"
    USERS ||--o{ POST_PROPOSALS : "submits"
    USERS ||--o{ RSVPS : "makes"
    USERS ||--o{ POST_FUNDS : "contributes"
    USERS ||--o{ VOTES : "casts"
    USERS ||--o{ PRODUCT_DISTRIBUTIONS : "receives"

    POSTS ||--o{ POST_MEMBERS : "has"
    POSTS ||--o{ POST_UPDATES : "has"
    POSTS ||--o{ POST_PROPOSALS : "has"
    POSTS ||--o{ POST_EVENTS : "has"
    POSTS ||--o{ POST_FUND_DRIVES : "has"
    POSTS ||--o{ POST_TAGS : "tagged with"
    POSTS ||--o{ PRODUCTS : "produces"

    TAGS ||--o{ POST_TAGS : "applied via"

    POST_EVENTS ||--o{ RSVPS : "receives"
    POST_FUND_DRIVES ||--o{ POST_FUNDS : "collects"

    CHANNELS ||--o{ CHANNEL_POSTS : "contains"
    POSTS ||--o{ CHANNEL_POSTS : "listed in"

    PRODUCTS ||--o{ PRODUCT_LINKS : "has"
    PRODUCTS ||--o{ PRODUCT_DISTRIBUTIONS : "distributed via"
    PRODUCT_LINKS ||--|| ASSETS : "references"

    PRODUCT_DISTRIBUTIONS ||--o{ PRODUCT_LINKS : "assigns"
    PRODUCT_DISTRIBUTIONS ||--o{ PRODUCT_DISTRIBUTION_STATUSES : "tracks"
    PRODUCT_DISTRIBUTIONS ||--o{ PRODUCT_DISTRIBUTION_ADDRESSES : "delivers to"
```

#### Polymorphic Associations

These four tables use `type`/`id` pairs to associate with multiple parent entities.

```mermaid
erDiagram
    ASSETS {
        uuid id PK
        string owner_type "user | post | product | product_link"
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

    PRODUCT_DISTRIBUTION_ADDRESSES {
        uuid id PK
        string addressable_type "user_address | user_email | product_link"
        string addressable_id FK
        uuid product_distribution_id FK
    }

    USERS { string id PK }
    POSTS { uuid id PK }
    POST_UPDATES { uuid id PK }
    POST_PROPOSALS { uuid id PK }
    POST_EVENTS { uuid id PK }
    PRODUCTS { uuid id PK }
    PRODUCT_LINKS { uuid id PK }
    USER_ADDRESSES { uuid id PK }
    USER_EMAILS { uuid id PK }
    PRODUCT_DISTRIBUTIONS { uuid id PK }

    USERS ||--o{ ASSETS : "owns (owner_type=user)"
    POSTS ||--o{ ASSETS : "owns (owner_type=post)"
    PRODUCTS ||--o{ ASSETS : "owns (owner_type=product)"
    PRODUCT_LINKS ||--o{ ASSETS : "owns (owner_type=product_link)"

    POSTS ||--o{ CONTENT : "has (parent_type=post)"
    POST_UPDATES ||--o{ CONTENT : "has (parent_type=update)"
    POST_PROPOSALS ||--o{ CONTENT : "has (parent_type=proposal)"
    POST_EVENTS ||--o{ CONTENT : "has (parent_type=event)"

    POSTS ||--o{ VOTES : "receives (resource_type=post)"
    POST_PROPOSALS ||--o{ VOTES : "receives (resource_type=council)"
    USERS ||--o{ VOTES : "casts"

    PRODUCT_DISTRIBUTIONS ||--o{ PRODUCT_DISTRIBUTION_ADDRESSES : "has"
    USER_ADDRESSES ||--o{ PRODUCT_DISTRIBUTION_ADDRESSES : "used as (addressable_type=user_address)"
    USER_EMAILS ||--o{ PRODUCT_DISTRIBUTION_ADDRESSES : "used as (addressable_type=user_email)"
    PRODUCT_LINKS ||--o{ PRODUCT_DISTRIBUTION_ADDRESSES : "used as (addressable_type=product_link)"
```

#### Product Distributions

How a product created by a project gets distributed to a user.

```mermaid
erDiagram
    POSTS {
        uuid id PK
        string type "project | post"
        string project_status "producing | completed | distributed"
    }

    PRODUCTS {
        uuid id PK
        uuid post_id FK
        string name
        decimal amount
        timestamptz depleted_at
    }

    ASSETS {
        uuid id PK
        string owner_type "product | product_link"
        string owner_id FK
        string name
        string mime_type
    }

    PRODUCT_LINKS {
        uuid id PK
        uuid product_id FK
        uuid product_distribution_id FK
        uuid asset_id FK
        string name
        boolean downloaded
    }

    PRODUCT_DISTRIBUTIONS {
        uuid id PK
        uuid product_id FK
        string user_id FK
        decimal amount
        timestamptz created_at
        timestamptz updated_at
    }

    PRODUCT_DISTRIBUTION_STATUSES {
        uuid id PK
        uuid product_distribution_id FK
        string status "preparing | shipped | received | downloaded | cancelled | returned"
        timestamptz created_at
    }

    PRODUCT_DISTRIBUTION_ADDRESSES {
        uuid id PK
        uuid product_distribution_id FK
        string addressable_type "user_address | user_email | product_link"
        string addressable_id FK
    }

    USER_ADDRESSES {
        uuid id PK
        string user_id FK
        string address_line_1
        string city
        string state
        string postal_code
    }

    USER_EMAILS {
        uuid id PK
        string user_id FK
        string address
    }

    USERS {
        string id PK
    }

    POSTS ||--o{ PRODUCTS : "produces"
    PRODUCTS ||--o{ ASSETS : "has (owner_type=product)"
    PRODUCTS ||--o{ PRODUCT_LINKS : "has"
    PRODUCTS ||--o{ PRODUCT_DISTRIBUTIONS : "allocated via"

    PRODUCT_LINKS ||--|| ASSETS : "references"
    PRODUCT_LINKS ||--o{ PRODUCT_DISTRIBUTION_ADDRESSES : "delivered via (addressable_type=product_link)"

    USERS ||--o{ PRODUCT_DISTRIBUTIONS : "receives"
    USERS ||--o{ USER_ADDRESSES : "has"
    USERS ||--o{ USER_EMAILS : "has"

    PRODUCT_DISTRIBUTIONS ||--o{ PRODUCT_LINKS : "assigns"
    PRODUCT_DISTRIBUTIONS ||--o{ PRODUCT_DISTRIBUTION_STATUSES : "tracks"
    PRODUCT_DISTRIBUTIONS ||--o{ PRODUCT_DISTRIBUTION_ADDRESSES : "delivers to"

    USER_ADDRESSES ||--o{ PRODUCT_DISTRIBUTION_ADDRESSES : "used as (addressable_type=user_address)"
    USER_EMAILS ||--o{ PRODUCT_DISTRIBUTION_ADDRESSES : "used as (addressable_type=user_email)"
```

**Distribution lifecycle** — a status record is appended each time the distribution state changes:

```mermaid
stateDiagram-v2
    [*] --> preparing : distribution created
    preparing --> shipped : physical product dispatched
    preparing --> downloaded : digital product downloaded
    shipped --> received : user confirms receipt
    downloaded --> [*]
    received --> [*]
    preparing --> cancelled : cancelled before dispatch
    shipped --> returned : user returns item
    returned --> [*]
    cancelled --> [*]
```

### Users

- Have
  - An ID using the computer or mobile device ID
  - A display name
  - A password hash
  - A created at timestamp with time zone
  - An updated at timestamp with time zone
  - A deleted at timestamp with time zone

### User Addresses

- Have
  - An ID using UUID
  - A name (optional)
  - An address line 1
  - An address line 2
  - A city
  - A state
  - A postal code
  - A created at timestamp with time zone
  - An updated at timestamp with time zone
  - A deleted at timestamp with time zone

### User Emails

- Have
  - An ID using UUID
  - A name (optional)
  - An address
  - A created at timestamp with time zone
  - An updated at timestamp with time zone
  - A deleted at timestamp with time zone

### Assets

- Have
  - An ID using UUID
  - A name
  - An application mime type
  - An owner ID
  - An owner type (user, post, product, product link)
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

### Products

- Have
  - An ID using UUID
  - A project ID
  - A name
  - An amount
  - A created at timestamp with time zone
  - An update at timestamp with time zone
  - A depleted at timestamp with time zone
  - Many product links
  - Many assets

### Product Links

- Have
  - An ID using UUID
  - A name (optional)
  - A product ID
  - A product distribution ID
  - An asset ID
  - Whether it has been downloaded

### Product Distribution Statuses

- Have
  - An ID using UUID
  - A product distribution ID
  - A status (preparing, shipped, recieved, downloaded, cancelled, returned)
  - A created at timestamp with time zone

### Product Distribution Addresses

- Have
  - An ID using UUID
  - A product distribution ID
  - An addressable type (user address, user email, product link)
  - An addressable ID

### Product Distributions

- Have
  - An ID using UUID
  - A user ID
  - A product ID
  - A project ID through products
  - An amount
  - A created at timestamp with time zone
  - An updated at timestamp with time zone
  - Many product distribution statuses
