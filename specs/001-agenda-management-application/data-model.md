# Data Model: Agenda Management Application

## Entity Definitions

### Event
**Purpose**: Represents a multi-day conference or gathering with automatically generated time slots

**Fields**:
- `id`: Unique identifier (UUID)
- `title`: Event name (required, string, max 200 chars)
- `description`: Detailed event description (required, string, supports Markdown)
- `startDate`: Event start date (required, ISO date format)
- `endDate`: Event end date (required, ISO date format, >= startDate)
- `createdAt`: Creation timestamp (auto-generated)
- `updatedAt`: Last update timestamp (auto-generated)

**Validation Rules**:
- End date must be equal to or after start date
- Title required and non-empty
- Description required and non-empty
- Dates must be valid ISO format

**Relationships**:
- One-to-many with Session
- One-to-many with TimeSlot (auto-generated)

### Session
**Purpose**: Individual presentation or activity within an event

**Fields**:
- `id`: Unique identifier (UUID)
- `title`: Session name (required, string, max 200 chars)
- `description`: Session description (required, string, supports Markdown)
- `date`: Session date (required, ISO date format)
- `eventId`: Reference to parent event (required, foreign key)
- `timeSlotId`: Reference to time slot (required, foreign key)
- `trackId`: Reference to track (required, foreign key)
- `speakerIds`: Array of speaker references (required, min 1 speaker)
- `tagIds`: Array of tag references (optional)
- `createdAt`: Creation timestamp (auto-generated)
- `updatedAt`: Last update timestamp (auto-generated)

**Validation Rules**:
- Session date must be within event's date range
- At least one speaker required
- Time slot must be valid (8am-6pm hourly slots)
- Title and description required and non-empty

**Relationships**:
- Many-to-one with Event
- Many-to-one with TimeSlot
- Many-to-one with Track
- Many-to-many with Speaker
- Many-to-many with Tag

### Speaker
**Purpose**: Person presenting at sessions with professional details

**Fields**:
- `id`: Unique identifier (UUID)
- `name`: Full name (required, string, max 100 chars)
- `jobTitle`: Current position (required, string, max 100 chars)
- `company`: Organization name (required, string, max 100 chars)
- `bio`: Professional biography (optional, string, supports Markdown)
- `profileImageUrl`: Speaker photo URL (optional, valid URL format)
- `socialLinks`: Social media links (optional object)
  - `twitter`: Twitter/X handle or URL (optional, string)
  - `linkedin`: LinkedIn profile URL (optional, valid URL)
  - `github`: GitHub username or URL (optional, string)
- `createdAt`: Creation timestamp (auto-generated)
- `updatedAt`: Last update timestamp (auto-generated)

**Validation Rules**:
- Name, job title, and company required and non-empty
- Profile image URL must be valid URL format if provided
- Social links must be valid URLs if provided
- Bio supports Markdown formatting

**Relationships**:
- Many-to-many with Session

### Track
**Purpose**: Category for organizing parallel sessions with visual color coding

**Fields**:
- `id`: Unique identifier (UUID)
- `name`: Track name (required, string, max 50 chars, unique)
- `description`: Track description (optional, string, max 500 chars)
- `color`: Color code for UI representation (optional, hex color format)
- `createdAt`: Creation timestamp (auto-generated)
- `updatedAt`: Last update timestamp (auto-generated)

**Validation Rules**:
- Name required, non-empty, and unique
- Color must be valid hex format if provided (#RRGGBB)
- Description optional but limited to 500 characters

**Relationships**:
- One-to-many with Session

### Tag
**Purpose**: Flexible labeling system for sessions to enable filtering and search

**Fields**:
- `id`: Unique identifier (UUID)
- `name`: Tag name (required, string, max 30 chars, unique)
- `createdAt`: Creation timestamp (auto-generated)
- `updatedAt`: Last update timestamp (auto-generated)

**Validation Rules**:
- Name required, non-empty, and unique
- Name should be normalized (lowercase, no special chars)

**Relationships**:
- Many-to-many with Session

### TimeSlot
**Purpose**: Hourly intervals automatically generated for each event day

**Fields**:
- `id`: Unique identifier (UUID)
- `eventId`: Reference to parent event (required, foreign key)
- `date`: Slot date (required, ISO date format)
- `startTime`: Start time (required, 24-hour format HH:MM)
- `endTime`: End time (required, 24-hour format HH:MM)
- `slotOrder`: Display order within day (integer, 0-9 for 8am-6pm)
- `createdAt`: Creation timestamp (auto-generated)

**Validation Rules**:
- Date must be within event's date range
- Start time must be between 08:00 and 17:00
- End time must be exactly 1 hour after start time
- Slot order must be 0-9 (representing 10 hourly slots)

**Relationships**:
- Many-to-one with Event
- One-to-many with Session

## Data Relationships

```
Event (1) ----< (many) TimeSlot
Event (1) ----< (many) Session

Session (many) ----< (1) Event
Session (many) ----< (1) TimeSlot  
Session (many) ----< (1) Track
Session (many) ----< (many) Speaker
Session (many) ----< (many) Tag

Speaker (many) ----< (many) Session
Track (1) ----< (many) Session
Tag (many) ----< (many) Session
```

## Business Rules

### Time Slot Generation
- Automatically create 10 hourly slots (08:00-18:00) for each event day
- Slots generated when event is created or date range modified
- Cannot manually create or delete time slots
- Slot deletion only occurs when event is deleted

### Session Scheduling
- Sessions can only be assigned to time slots within their event's date range
- Multiple sessions can be scheduled in the same time slot (parallel tracks)
- Session date must match the time slot's date
- Cannot schedule session without at least one speaker

### Speaker Management
- Speakers are reusable across multiple sessions and events
- Speaker deletion checks for existing session references
- Social links are optional but must be valid URLs if provided
- Profile images are optional with size/format restrictions

### Track and Tag Management
- Track names must be unique within the system
- Tags are globally unique and normalized
- Deleting a track requires reassigning all associated sessions
- Tags can be created dynamically or predefined

## State Transitions

### Event Lifecycle
1. **Draft** → Event created with title and dates
2. **Active** → Time slots generated, sessions can be scheduled
3. **Archived** → Event completed, read-only access

### Session Lifecycle
1. **Draft** → Session created with basic info
2. **Scheduled** → Assigned to time slot and track
3. **Published** → Visible to attendees with all details
4. **Completed** → Session finished, historical record

## Data Integrity Constraints

### Foreign Key Constraints
- Session.eventId → Event.id (CASCADE DELETE)
- Session.timeSlotId → TimeSlot.id (RESTRICT DELETE)
- Session.trackId → Track.id (RESTRICT DELETE)
- TimeSlot.eventId → Event.id (CASCADE DELETE)

### Junction Tables
- **SessionSpeaker**: session_id, speaker_id (composite primary key)
- **SessionTag**: session_id, tag_id (composite primary key)

### Indexes
- Event.startDate, Event.endDate (for date range queries)
- Session.eventId, Session.date (for agenda queries)
- TimeSlot.eventId, TimeSlot.date (for schedule lookups)
- Speaker.name (for search functionality)
- Track.name, Tag.name (for filtering operations)