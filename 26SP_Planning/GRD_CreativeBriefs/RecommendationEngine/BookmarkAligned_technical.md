# BOOKMARK - Technical Implementation (Parts 5-6)

**Platform:** Recommendation Engine (Preference-Learning System)
**White-Label Application:** Book Recommendations + Reading Journal with Smart Reading Light
**Technical Purpose:** Platform Integration & Cross-Discipline Collaboration Guide
**Target Market:** Regular readers seeking better discovery and reading memory
**Project Classification:** ORANGE Clearance
**Last Updated:** January 2026

---

## ABOUT THIS DOCUMENT

This document is **Part 2 of 2** of the BookmarkAligned brief:

1. **BookmarkAligned_core.md** - Parts 1-4: Creative Brief, Product Deep Dive, User Research, Strategic Guidance
2. **BookmarkAligned_technical.md** (this document) - Parts 5-6: Technical Implementation Context, Cross-Discipline Workflow

**Purpose**: This document provides the technical mapping between Bookmark (the book recommendation system with smart reading light) and the underlying Recommendation Engine Platform built by CTS programming students.

---

# PART 5: TECHNICAL IMPLEMENTATION CONTEXT

## Overview: Bridging Design to Development

This section provides technical implementation guidance for design students working on Bookmark. Understanding how your design decisions map to the underlying Recommendation Engine architecture ensures your creative vision can actually be built—and helps you create more sophisticated, implementation-aware design work.

Bookmark is one of several white-label configurations of the **Recommendation Engine Platform™**, a flexible preference-learning system built by programming students. Your design work will be implemented through configuration, theming, and feature toggles—not custom code.

**Key insight:** Bookmark uses the same database, recommendation logic, and core features as LetsEat!, SkillOptimizer™, EventFlow™, and other applications. What differentiates Bookmark is its literary/sophisticated voice, book-specific tracking, smart reading light IoT integration, source attribution focus, and feeling-based recommendation matching.

---

## 5.1 Engine Capability Mapping

**How Bookmark Features Map to Recommendation Engine Platform Capabilities**

The Recommendation Engine Platform provides a robust preference-learning system. Bookmark doesn't reinvent the wheel—it configures and brands existing capabilities with a book-reading, feeling-focused, source-tracking approach.

### Items → Books

**Platform capability:** CRUD operations for items with attributes, categories, user ratings, and recommendation generation.

**Bookmark mapping:**
- Item = **Book** (physical or digital)
- Standard item fields:
  - `title` → Book title
  - `creator` → Author(s)
  - `item_type` → Book format (hardcover, paperback, ebook, audiobook)
  - `description` → Publisher's description or synopsis
  - `image_url` → Book cover image
  - `external_id` → ISBN, Goodreads ID, or library catalog number
- Additional metadata fields:
  - `genre` (Fiction, Mystery, Sci-Fi, Memoir, History, etc.)
  - `subgenre` (Literary Fiction, Cozy Mystery, Hard Sci-Fi, etc.)
  - `publication_year` (helps filter for recent releases or classics)
  - `publisher`
  - `page_count`
  - `series_info` (if part of series: series name, book number)
  - `reading_level` (Adult, YA, Middle Grade, etc.)
  - `pacing` (Fast-paced thriller, Slow literary, Medium contemporary, etc.)
  - `mood_tags` (Dark, Uplifting, Thoughtful, Escapist, etc.)

**Design implications:**
- Book cards prominently display cover image (covers are crucial for book recognition)
- Typography hierarchy: Book Title (largest), Author (prominent), Genre/Publication Year (subtle)
- Cover images should be high-resolution (users recognize books by cover)
- Genre/mood tags displayed with color coding (consistent across interface)
- Series information visible if applicable ("Book 2 of Trilogy")
- Physical format indicator (hardcover icon, ebook icon, audiobook icon)
- "Added to TBR" timestamp visible ("Added 3 months ago—why did you want this?")

### Ratings → Reading Reflections

**Platform capability:** User ratings with numerical scale, written reviews, timestamps, and recommendation engine learning.

**Bookmark mapping:**
- Rating = **Reading Reflection** (one-sentence feeling capture + context)
- Quick rating (5-star or ❤️/👍/👎 simplified) labeled as "Would you recommend this?"
- **One-sentence feeling** (text field): "Couldn't put down" | "Beautiful sentences" | "Made me cry" | "Slow but worth it"
- **Who'd love this?** (text field): "Anyone who loved [Other Book]" | "Students interested in social justice" | "Readers seeking comfort reads"
- **Mood match** (multi-select tags): Uplifting, Dark, Thought-provoking, Escapist, Beautiful prose, Couldn't-put-down, etc.
- **Reading experience notes** (optional text field): Specific memorable moments or observations
- **Completion date** (when finished—synced from device if physical book, from Kindle/Apple Books if digital)
- **Reading speed** (days to finish—tracked automatically by device)
- **Would re-read?** (boolean)

**Design implications:**
- One-sentence feeling field most prominent (this is the core value)
- "Who'd love this?" prompt encourages thinking about audience/recommendations
- Mood tags displayed as chips/pills (multi-select, visually browsable)
- Quick rating de-emphasized (feeling is more important than stars)
- Reading speed/completion data auto-populated (no manual entry if device synced)
- Visual hierarchy: one-sentence feeling > mood tags > who'd love this > notes
- Reflection capture should feel quick and conversational, not like Goodreads review homework

### Attributes → Book Classifications & Mood Tags

**Platform capability:** Multi-valued attributes that categorize items, enable filtering, and power recommendation similarity matching.

**Bookmark mapping:**
- Attributes = **Genres, Subgenres, Mood Tags, Pacing Descriptors, Writing Style Tags**
- **Genre tags:** Fiction, Nonfiction, Mystery, Thriller, Sci-Fi, Fantasy, Literary Fiction, Contemporary, Historical, Memoir, Biography, etc.
- **Mood tags:** Dark, Uplifting, Thoughtful, Escapist, Beautiful prose, Fast-paced, Character-driven, Plot-driven, Atmospheric, Cozy, Intense, etc.
- **Writing style tags:** Lyrical, Spare, Dense, Accessible, Poetic, Conversational, Experimental, etc.
- **Content tags:** LGBTQ+, Diverse authors, Own voices, Translated, Classic, Contemporary, New release, Backlist, etc.
- Each attribute has:
  - `attribute_name` (specific tag like "Beautiful prose")
  - `attribute_category` (genre, mood, style, content)
  - `color_code` (for visual consistency—mood-based color theming)
  - `icon` (visual indicator—heart for emotional, brain for thoughtful, lightning for fast-paced)

**Design implications:**
- Mood tags use feeling-based colors (warm for uplifting, cool for dark, neutral for thoughtful)
- Genre tags use literary design aesthetic (serif fonts, book-cover-inspired colors)
- Tag selection multi-select (books can have multiple moods and genres)
- Mood tags displayed prominently (more important than rigid genre classifications)
- Visual differentiation: genre tags book-inspired, mood tags emotion-colored, style tags neutral
- Tags searchable/filterable: "Show me uplifting memoirs" or "Beautiful prose + sci-fi"
- Discovery Mode uses mood-matching across genres: "You love 'beautiful prose'—try this sci-fi with same descriptor"

### Recommendations → Reading Suggestions

**Platform capability:** Algorithm generates personalized suggestions based on user ratings, attribute preferences, and similarity patterns.

**Bookmark mapping:**
- Recommendation = **Reading Suggestion** with feeling-based reasoning
- Recommendation reasoning displayed: "You loved 6 books you described as 'couldn't put down'—try this"
- **Feeling-pattern matching:** Analyzes your one-sentence feelings to find books other readers described similarly
- **Source-based suggestions:** "Books recommended by Forever35 podcast (your 85% hit rate source)"
- **Mood-matching:** "You're seeking uplifting—here are books readers described that way"
- **Genre diversity mode (Discovery Mode):** Intentionally suggests books outside usual genres but matching your feeling preferences
- **Pacing match:** Device data shows you prefer books you finished in 2-4 days → suggests fast-paced books
- **Reading streak suggestions:** If you're on a reading streak, suggest shorter books to maintain momentum
- Recommendations include:
  - Book cover, title, author
  - **Why this recommendation** ("Same feeling pattern as books you loved")
  - **Feeling descriptors** (what other readers with similar taste said)
  - **Source context** (if from a trusted recommender in your network)
  - **Estimated reading time** (based on your reading speed and book length)
  - **Your TBR status** (if you've already added it: "You added this 6 months ago because [reason]")
  - **Library availability** (if integrated: "Available now at your library")

**Design implications:**
- "Discover Your Next Read" button prominent on home screen (primary action)
- Recommendation reasoning given visual emphasis (not fine print—this is the value)
- Feeling descriptors displayed as pull quotes: *"Couldn't put down"*
- Source attribution visible: "Recommended by Forever35 podcast"
- Discovery Mode toggle easy to access ("Show me something different")
- Visual language: sophisticated, literary, not algorithm-corporate
- Easy actions: "Add to TBR" | "Already Read" | "Not Interested" | "Tell Me More"
- Book covers large and prominent (users browse visually)

### Sources → Recommendation Sources

**Platform capability:** Track where items come from, analyze source reliability, filter by source.

**Bookmark mapping:**
- Source = **Recommendation Source** (who suggested this book)
- Source types:
  - **Podcasts** (Forever35, What Should I Read Next, Currently Reading, etc.)
  - **Book Influencers** (BookTok accounts, Bookstagram, YouTube BookTubers)
  - **Friends** (individual people in your network)
  - **Book Clubs** (specific groups)
  - **Publications** (New York Times Book Review, Paris Review, literary magazines)
  - **Authors** (author recommendations from interviews, newsletters)
  - **Bookstores** (indie bookstore staff picks)
  - **Algorithms** (Goodreads, Amazon, Literal suggestions—tracked to show how they compare)
- Source tracking data:
  - `source_name` (specific podcast, friend name, influencer handle)
  - `source_type` (podcast, friend, influencer, publication, etc.)
  - `recommendation_count` (how many books from this source you've tried)
  - `hit_rate` (what % of their recommendations did you love)
  - `alignment_score` (how well their taste matches yours, calculated from rating patterns)
  - `last_hit` (most recent book from this source you loved—keeps source attribution fresh)
  - `discovery_method` (how you found this source)

**Design implications:**
- Source attribution displayed on every TBR entry: "Recommended by [Source]"
- Source analysis dashboard: "Your Top Sources" with hit rate percentages
- Visual source ranking: Green checkmark for 70%+ hit rate, yellow for 40-70%, red for <40%
- Source detail pages: "Forever35 Podcast: 17 recommendations, 85% hit rate, last hit: [Book Title]"
- Add-to-TBR flow requires source tagging: "Where did you hear about this?"
- Easy source selection: Recent sources quick-select, plus search for new sources
- Source comparison: "Forever35: 85% | BookTok Account: 20%" helps prioritize
- Discovery insight: "You discover your favorite books through podcasts"

### User Profiles → Reading Profiles

**Platform capability:** User accounts with preferences, history, and personalization data.

**Bookmark mapping:**
- User Profile = **Reading Profile** (your complete reading identity)
- Profile contains:
  - **Reading history** (all completed books, synced from device + digital accounts)
  - **TBR list** (books you want to read, with source and reason captured)
  - **Currently reading** (active books, with progress synced from device/Kindle)
  - **Feeling patterns** (your most-used descriptors: "beautiful sentences" "couldn't put down")
  - **Genre distribution** (pie chart: 40% literary fiction, 30% memoir, 20% mystery, 10% sci-fi)
  - **Source performance** (ranked list of recommendation sources with hit rates)
  - **Reading pace** (average books per month, reading speed trends)
  - **Reading goals** (monthly/yearly targets, genre diversity goals)
  - **Trusted circle** (friends/sources you follow for recommendations)
  - **Privacy settings** (reading history private by default, optional sharing with book clubs)
  - **Device sync status** (connected reading light, connected Kindle/Apple Books accounts)
- Connected accounts:
  - Bluetooth device pairing (smart reading light)
  - Kindle account sync
  - Apple Books account sync
  - Kobo account sync (if supported)
  - Google Play Books sync (if supported)
  - Library card integration (if supported)

**Design implications:**
- Dashboard shows reading profile at-a-glance: current reads, recent completions, top sources
- "Your Reading Patterns" visualizations: genre distribution, feeling patterns, reading pace
- Device connection status visible: "Reading Light Connected" with battery indicator
- Digital account sync status: "Syncing with Kindle" or "Last synced 2 hours ago"
- Privacy controls prominent: "Who can see your reading history?" with clear options
- Reading goals progress: "7 of 50 books this year" with encouraging messaging
- Genre diversity tracking: "You've read 5 different genres this month—keep exploring!"
- Source analysis accessible: "See which recommenders match your taste"

---

## 5.2 Database Entity Alignment

**Key Database Entities for Bookmark Implementation**

The Recommendation Engine database schema supports all white-label configurations. Here's how Bookmark specifically uses these entities:

### Books (Items Table)

```sql
CREATE TABLE items (
    id SERIAL PRIMARY KEY,
    title VARCHAR(500) NOT NULL,
    creator VARCHAR(300),  -- Author(s)
    description TEXT,
    image_url VARCHAR(500),  -- Book cover
    external_id VARCHAR(100),  -- ISBN or Goodreads ID
    item_type VARCHAR(50),  -- 'hardcover', 'ebook', 'audiobook'
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);
```

**Bookmark-specific fields** (JSON metadata or separate columns):
- `genre` (Fiction, Mystery, Memoir, etc.)
- `subgenre` (Literary Fiction, Cozy Mystery, etc.)
- `publication_year`
- `publisher`
- `page_count`
- `series_info` (JSON: {series_name, book_number})
- `pacing` (Fast-paced, Slow, Medium)
- `mood_tags` (Array: ['Dark', 'Uplifting', 'Thoughtful'])

### Reading Reflections (Ratings Table)

```sql
CREATE TABLE ratings (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    item_id INT REFERENCES items(id),  -- Book
    rating_value DECIMAL(2,1),  -- 1.0 to 5.0 stars
    review_text TEXT,  -- One-sentence feeling
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);
```

**Bookmark-specific extensions**:
- `one_sentence_feeling` TEXT  -- Primary field: "Couldn't put down"
- `who_would_love_this` TEXT  -- Audience recommendation
- `mood_tags` JSONB  -- Array of mood descriptors
- `reading_experience_notes` TEXT  -- Optional detailed thoughts
- `completion_date` DATE
- `days_to_finish` INT  -- Calculated from device data or manual entry
- `would_reread` BOOLEAN
- `synced_from_device` BOOLEAN  -- True if completion detected by smart reading light

### Recommendation Sources (Sources Table)

```sql
CREATE TABLE sources (
    id SERIAL PRIMARY KEY,
    source_name VARCHAR(200) NOT NULL,  -- "Forever35 Podcast"
    source_type VARCHAR(50),  -- 'podcast', 'friend', 'influencer'
    user_id INT REFERENCES users(id),  -- Who tracks this source
    created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE item_sources (
    id SERIAL PRIMARY KEY,
    item_id INT REFERENCES items(id),  -- Book
    source_id INT REFERENCES sources(id),  -- Source that recommended it
    user_id INT REFERENCES users(id),
    recommended_date DATE,
    context_note TEXT,  -- Why it sounded good, which episode, etc.
    created_at TIMESTAMP DEFAULT NOW()
);
```

**Bookmark-specific analytics** (calculated fields or aggregations):
- `recommendation_count` (how many books from this source tried)
- `hit_rate` (% of recommendations from this source that were loved)
- `alignment_score` (taste match percentage)
- `last_hit_book_id` (most recent book from this source that was loved)

### Reading Device Sync (New Table for IoT Integration)

```sql
CREATE TABLE reading_devices (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    device_type VARCHAR(50),  -- 'bookmark_reading_light', 'kindle', 'apple_books'
    device_identifier VARCHAR(200),  -- Bluetooth MAC address, account ID
    is_connected BOOLEAN DEFAULT false,
    last_sync TIMESTAMP,
    created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE reading_sessions (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    device_id INT REFERENCES reading_devices(id),
    item_id INT REFERENCES items(id),  -- Book being read
    session_start TIMESTAMP,
    session_end TIMESTAMP,
    pages_start INT,
    pages_end INT,
    reading_speed_wpm DECIMAL(6,2),  -- Words per minute (calculated)
    created_at TIMESTAMP DEFAULT NOW()
);
```

**Device sync enables**:
- Automatic "currently reading" status updates
- Reading progress tracking without manual entry
- Completion detection (when user finishes last page)
- Reading pace analysis (time spent reading, pages per session)
- Recommendation refinement (fast readers get fast-paced books suggested)

### TBR Management (User Wishlists)

```sql
CREATE TABLE wishlists (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    item_id INT REFERENCES items(id),  -- Book on TBR list
    source_id INT REFERENCES sources(id) NULLABLE,  -- Who recommended
    reason_added TEXT,  -- Why it sounded good
    priority VARCHAR(20),  -- 'high', 'medium', 'low'
    mood_seeking VARCHAR(100),  -- What mood/feeling seeking when added
    added_date DATE DEFAULT NOW(),
    started_reading_date DATE NULLABLE,
    created_at TIMESTAMP DEFAULT NOW()
);
```

**TBR-specific features**:
- Source attribution tracked at time of adding
- "Why did you add this?" prompt captures context
- Mood seeking helps with later filtering: "Show me TBR books for uplifting mood"
- Priority tagging helps sort: "Show me high-priority TBR"
- Time-since-added visible: "You added this 6 months ago"

---

## 5.3 Configuration Layer (YAML for White-Label Theming)

**Bookmark-Specific Configuration File**

The Recommendation Engine uses YAML configuration files to differentiate white-label applications. Here's Bookmark's configuration:

```yaml
# config/bookmark.yml
application:
  name: "Bookmark"
  tagline: "Remember the feeling, not just the title"
  logo_url: "/assets/bookmark-logo.svg"
  primary_color: "#2C3E50"  # Deep blue-gray (literary sophistication)
  accent_color: "#E67E22"   # Warm orange (bookish warmth)
  font_primary: "Freight Text Pro, Georgia, serif"  # Headlines
  font_secondary: "Inter, system-ui, sans-serif"    # Body text

item_config:
  item_name_singular: "book"
  item_name_plural: "books"
  creator_label: "author"
  default_image: "/assets/default-book-cover.png"
  required_fields: ['title', 'creator', 'genre']
  optional_fields: ['series_info', 'publication_year', 'page_count', 'pacing']

rating_config:
  rating_scale: "stars"  # 1-5 stars or hearts
  rating_label: "Would you recommend this?"
  review_prompt: "One sentence about how it felt:"
  secondary_prompts:
    - label: "Who'd love this?"
      field: "who_would_love_this"
    - label: "Reading experience notes"
      field: "reading_experience_notes"
      optional: true
  enable_mood_tags: true
  mood_tag_options:
    - "Uplifting"
    - "Dark"
    - "Thoughtful"
    - "Escapist"
    - "Beautiful prose"
    - "Couldn't put down"
    - "Slow but worth it"
    - "Character-driven"
    - "Plot-driven"
    - "Atmospheric"

source_config:
  enable_source_tracking: true
  require_source_on_add: true  # Must tag source when adding to TBR
  source_types:
    - "Podcast"
    - "Friend"
    - "Book Influencer"
    - "Book Club"
    - "Publication"
    - "Author"
    - "Bookstore Staff Pick"
    - "Algorithm (Goodreads/Amazon)"
  show_source_analytics: true  # Display hit rate percentages

device_integration:
  enable_iot_devices: true
  supported_devices:
    - type: "bookmark_reading_light"
      name: "Bookmark Smart Reading Light"
      connection: "bluetooth"
      auto_sync: true
    - type: "kindle"
      name: "Amazon Kindle"
      connection: "api"
      auto_sync: true
    - type: "apple_books"
      name: "Apple Books"
      connection: "api"
      auto_sync: true
  sync_frequency: "real-time"  # For Bluetooth devices
  completion_detection: "automatic"  # Device detects when book finished

recommendation_config:
  algorithm_mode: "feeling_pattern_matching"  # Match mood descriptors, not just genres
  enable_discovery_mode: true  # Suggest cross-genre based on feeling match
  recommendation_reasons: true  # Always show "why we're suggesting this"
  source_based_suggestions: true  # Suggest books from high-hit-rate sources
  pacing_match: true  # Use reading speed data to match book pacing
  diversification_prompt: true  # Encourage genre diversity

privacy_config:
  default_privacy: "private"  # Reading history private by default
  social_features: "opt-in"  # No public sharing unless user chooses
  data_export: true  # Users can export all their data
  data_deletion: true  # Users can delete their data
  camera_privacy: "ocr_only"  # Device camera only captures text for OCR, no images stored

ui_customizations:
  home_screen_widgets:
    - "currently_reading"
    - "tbr_quick_add"
    - "recent_completions"
    - "recommendations"
    - "source_analytics"
  navigation_items:
    - label: "Discover"
      route: "/recommendations"
    - label: "My Reading"
      route: "/reading-history"
    - label: "TBR List"
      route: "/wishlist"
    - label: "Sources"
      route: "/sources"
    - label: "Devices"
      route: "/devices"
  button_labels:
    add_item: "Add to TBR"
    rate_item: "Capture Feeling"
    view_recommendations: "Discover Your Next Read"
    enable_discovery: "Show Me Something Different"
```

**Design implications**:
- Configuration drives UI labels, button text, and prompts
- Color scheme defined here (designers provide hex codes)
- Typography choices specified (designers provide font families)
- Feature toggles enable/disable capabilities (source tracking, device sync)
- Mood tag options customizable (designers can propose additional tags)
- Privacy defaults set to "private" (reinforces trust positioning)

---

## 5.4 Asset Delivery Specifications

**What Design Students Deliver to Programming Students**

To implement Bookmark's visual identity in the Recommendation Engine platform, design students provide:

### Brand Identity Assets

**Logo Files**:
- `bookmark-logo-full.svg` (wordmark + logomark, vector)
- `bookmark-logo-icon.svg` (logomark only, for app icon)
- `bookmark-logo-horizontal.svg` (horizontal lockup for headers)
- `bookmark-logo-vertical.svg` (vertical lockup for splash screens)
- All provided as SVG (scalable) and PNG (1x, 2x, 3x for mobile)

**Color Palette**:
- `colors.json` with hex codes for all brand colors:
  ```json
  {
    "primary": "#2C3E50",
    "accent": "#E67E22",
    "success": "#27AE60",
    "warning": "#F39C12",
    "error": "#E74C3C",
    "neutral_dark": "#34495E",
    "neutral_medium": "#95A5A6",
    "neutral_light": "#ECF0F1",
    "background": "#FFFFFF",
    "text_primary": "#2C3E50",
    "text_secondary": "#7F8C8D"
  }
  ```

**Typography**:
- Font files (if custom fonts): `.woff`, `.woff2`, `.ttf`
- `typography.css` with font-face declarations and hierarchy:
  ```css
  /* Headlines */
  h1, h2, h3 { font-family: 'Freight Text Pro', Georgia, serif; }

  /* Body text */
  body, p { font-family: 'Inter', system-ui, sans-serif; }

  /* Book titles */
  .book-title { font-family: 'Freight Text Pro', serif; font-weight: 500; }

  /* One-sentence feelings (user quotes) */
  .feeling-quote { font-family: 'Freight Text Pro', serif; font-style: italic; }
  ```

### UI Component Library

**Icon Set**:
- All icons as SVG (24x24px, 48x48px)
- Icons needed:
  - `icon-book.svg` (book item)
  - `icon-add-tbr.svg` (add to TBR action)
  - `icon-heart.svg` (favorite/love)
  - `icon-reading-light.svg` (device indicator)
  - `icon-bluetooth.svg` (device connection)
  - `icon-battery.svg` (device battery status)
  - `icon-source.svg` (recommendation source)
  - `icon-mood-uplifting.svg`, `icon-mood-dark.svg`, etc. (mood tags)
  - `icon-genre-fiction.svg`, `icon-genre-mystery.svg`, etc. (genre tags)
  - `icon-discover.svg` (Discovery Mode)
  - `icon-search.svg`, `icon-filter.svg`, `icon-sort.svg` (navigation)

**Mood Tag Visual System**:
- Each mood tag has:
  - Icon (SVG)
  - Color code (hex)
  - Typography style
- Example:
  ```json
  {
    "tag_name": "Uplifting",
    "icon": "icon-mood-uplifting.svg",
    "color": "#F39C12",
    "text_color": "#FFFFFF"
  }
  ```

**Button Styles**:
- Primary button (Add to TBR): Background color, hover state, active state
- Secondary button (Already Read): Border style, hover state
- Tertiary button (Not Interested): Text-only, hover state
- Component CSS or design tokens

**Card Designs**:
- Book card (for browsing): Layout specs, spacing, typography
- Recommendation card (with reasoning): Layout emphasizing "why" explanation
- Source card (source analytics): Hit rate visualization, alignment score display
- TBR card (with source attribution): Source tag prominent, reason visible

**Form Elements**:
- Text input (for one-sentence feeling, search)
- Textarea (for reading notes)
- Multi-select tags (for mood tags)
- Rating input (star rating or simplified)
- Device connection UI (Bluetooth pairing flow)

### Device-Specific Assets

**Smart Reading Light Branding**:
- Logo file for device surface printing: `bookmark-device-logo.svg`
- Packaging design files: Box exterior, interior, insert cards
- Quick Start Guide: PDF print-ready file
- App pairing screens: UI designs for "Connect Your Device" flow

**App Icon**:
- iOS app icon: 1024x1024px PNG
- Android app icon: 512x512px PNG, adaptive icon components
- Favicon: 32x32px, 16x16px

### Marketing Assets (Optional, if chosen as deliverable)

- Social media templates (Instagram post, Story)
- Email templates (onboarding series)
- Website landing page mockup (Figma/XD file)
- Print ad layouts (if chosen deliverable)

**File Delivery Format**:
- All assets in `/assets/bookmark/` folder
- Organized subdirectories: `/logos`, `/icons`, `/images`, `/fonts`, `/styles`
- `README.md` explaining file structure and usage guidelines
- Design tokens JSON file for easy programmatic access

---

## 5.5 API Integration Points

**How Bookmark Connects to External Services**

Bookmark's unique value is **unified reading profile** (physical + digital books tracked together). This requires API integrations with:

### Smart Reading Light (Bluetooth IoT Device)

**Connection Method**: Bluetooth Low Energy (BLE)

**Data Flow**:
1. User pairs device with app (one-time setup)
2. Device remains connected during reading sessions
3. Device sends reading data to app in real-time:
   - Book recognized (OCR captures title/author)
   - Pages read (tracks progress)
   - Reading speed (time per page)
   - Session duration (start/end times)
   - Quote flagged (user taps touch panel)
4. App stores data, updates "currently reading" status

**Technical Requirements for Design Students**:
- Design Bluetooth pairing flow: "Turn on device → Open app → Tap Connect → Confirm pairing"
- Design book recognition confirmation: "Reading: [Book Title] by [Author]" notification
- Design sync status indicator: "Last synced 2 minutes ago"
- Design low battery warning: "Reading Light: 15% battery"
- Design connection lost state: "Reconnecting to device..."

**Programming Student Needs**:
- UI screens for pairing flow
- Visual feedback for successful book recognition
- Error state designs (book not recognized, connection lost)
- Battery indicator placement and style
- Privacy indicator (camera active light—designed into physical device)

### Amazon Kindle API

**Connection Method**: OAuth 2.0 authentication to link Kindle account

**Data Retrieved**:
- Books in Kindle library
- Currently reading books with progress percentage
- Finished books with completion dates
- Highlights and notes (if user grants permission)

**Data Flow**:
1. User authorizes Bookmark to access Kindle account (one-time OAuth)
2. App periodically syncs Kindle data (every 6 hours or on-demand)
3. Books read on Kindle automatically appear in Bookmark reading history
4. Completion detected when book progress = 100%

**Technical Requirements for Design Students**:
- Design account linking flow: "Connect Kindle Account" button → OAuth screen
- Design sync status: "Syncing with Kindle..." → "Last synced 2 hours ago"
- Design Kindle book indicator: Icon showing "Read on Kindle"
- Design conflict resolution: User finished book on device AND Kindle (how to handle?)

### Apple Books API

**Connection Method**: Similar to Kindle (OAuth or Apple ID sign-in)

**Data Retrieved**:
- Books in Apple Books library
- Reading progress
- Completion status
- Highlights/notes

**Data Flow**: Same as Kindle

### Kobo / Google Play Books APIs (If Supported)

**Connection Method**: OAuth

**Data Retrieved**: Same as Kindle/Apple Books

**Design Implication**: Need unified "Connected Accounts" settings page showing all linked services

### Library Catalog Integration (Stretch Goal)

**Connection Method**: OverDrive API or library-specific APIs

**Data Retrieved**:
- Book availability at user's local libraries
- Wait times for popular books
- One-click borrow/hold placement

**Design Requirement**: "Available at [Library Name]" badge on book cards, "Borrow Now" action button

### Indie Bookstore Affiliate Links (Bookshop.org API)

**Connection Method**: Affiliate API

**Data Retrieved**:
- Purchase links for books
- Availability status
- Pricing

**Design Requirement**: "Buy from Indie Bookstore" button with Bookshop.org logo, revenue share messaging

### Book Metadata APIs (For TBR Adding)

**Connection Method**: Google Books API, Open Library API, or Goodreads API (for book cover images, descriptions, ISBN lookup)

**Use Case**: When user adds book to TBR by title search, app fetches:
- Book cover image
- Author
- Publication year
- Genre
- Synopsis

**Design Requirement**: Search interface with autocomplete, book detail preview before adding to TBR

---

# PART 6: CROSS-DISCIPLINE WORKFLOW

## Overview: Working with Programming Students

Bookmark is a **collaborative project** between design students (you) and programming students (CTS 285). You design the brand, user experience, and visual interface. They build the Recommendation Engine platform, IoT device integration, and implement your designs.

**Success requires**: Regular communication, mutual respect for expertise, and understanding of each other's constraints.

---

## 6.1 Sprint Touchpoints & Collaboration Ceremonies

**ORANGE Clearance projects use Agile/Scrum methodology**. You'll participate in sprint ceremonies alongside programming students.

### Sprint Structure (2-Week Sprints)

**Week 1**:
- Sprint Planning (Monday): Define what gets built this sprint
- Design-Dev Sync (Wednesday): Share mockups, discuss feasibility
- Mid-Sprint Check-in (Friday): Review progress, address blockers

**Week 2**:
- Design Review (Monday): Get feedback on latest designs
- Integration Testing (Wednesday): Test implemented designs in app
- Sprint Review (Friday): Demo completed work to stakeholders
- Sprint Retrospective (Friday): What went well, what to improve

### Your Role in Each Ceremony

**Sprint Planning**:
- **You present**: Completed designs ready for implementation (mockups, assets, specifications)
- **You discuss**: Design priorities for this sprint (what's most important to implement first?)
- **You learn**: Technical constraints that might affect design decisions

**Design-Dev Sync (Mid-Week)**:
- **You share**: Work-in-progress mockups, get early feedback on feasibility
- **You ask**: "Can the device API provide this data in real-time?" "Is this animation performance-feasible?"
- **They share**: Implementation challenges, technical alternatives
- **Goal**: Prevent "we can't build this" surprises at the end of sprint

**Sprint Review (Demo Day)**:
- **You present**: Design rationale (why you made specific decisions)
- **They present**: Working features (your designs implemented in code)
- **Together**: Demo to instructor, get user feedback
- **You observe**: How users interact with your designs (are they intuitive?)

**Sprint Retrospective**:
- **You reflect**: What design-dev collaboration went well? What needs improvement?
- **You propose**: Process improvements ("Let's share mockups earlier" or "Need clearer asset naming conventions")

---

## 6.2 Design Handoff Process

**How You Deliver Designs to Programming Students**

### Phase 1: Low-Fidelity Wireframes (Week 1-2)

**What you create**:
- Sketches or low-fi wireframes (Figma, paper, Balsamiq)
- Show screen layouts, navigation flow, key interactions
- Focus on structure and functionality, not visual polish

**What you deliver**:
- PDF or Figma link with annotated wireframes
- User flow diagrams (how users move through app)

**Why this matters**:
- Gets early feedback on information architecture
- Programming students can start planning database structure
- Cheaper to change wireframes than high-fi mockups

### Phase 2: High-Fidelity Mockups (Week 3-5)

**What you create**:
- Visual designs with brand identity applied
- Typography, colors, spacing, imagery
- Multiple screen states (empty state, loading, error, success)
- Responsive designs (mobile, tablet, desktop)

**What you deliver**:
- Figma/XD file with organized artboards
- Design specs: Spacing (8px grid?), font sizes, color codes
- Interactive prototypes (if helpful for showing transitions)

**Programming students need**:
- Pixel-perfect measurements (use Figma's inspect mode)
- All screen states documented (not just the "happy path")
- Accessibility notes (color contrast ratios, text sizes)

### Phase 3: Asset Export (Week 6)

**What you deliver**:
- All logos, icons, images as SVG and PNG
- Color palette JSON file
- Typography CSS or design tokens
- Component library (buttons, cards, form elements styled)

**File organization**:
```
/assets/bookmark/
  /logos/
    bookmark-logo-full.svg
    bookmark-logo-icon.svg
  /icons/
    icon-book.svg
    icon-add-tbr.svg
  /images/
    default-book-cover.png
  /fonts/
    FreightTextPro-Regular.woff2
  /styles/
    colors.json
    typography.css
```

**Naming conventions**:
- Use kebab-case: `icon-reading-light.svg` (not `Icon Reading Light.svg`)
- Be descriptive: `button-primary-hover-state.png`
- Include dimensions in filename if multiple sizes: `app-icon-512x512.png`

### Phase 4: Design QA (Week 7+)

**What you do**:
- Review implemented designs in the app
- Compare to your mockups: Are colors right? Spacing correct? Typography matching?
- Document discrepancies: "Button text should be Inter 16px, currently showing 14px"
- Provide feedback in sprint review or GitHub issues

**How to give feedback**:
- Screenshot actual vs. expected: "Mockup shows 24px spacing, implementation shows 16px"
- Be specific: Not "This looks wrong" but "Text color should be #2C3E50, currently #000000"
- Prioritize: Mark critical issues (broken functionality) vs. nice-to-haves (minor spacing tweaks)

---

## 6.3 Communication Protocols

**How to Collaborate Effectively**

### Design Questions to Ask Programming Students

**Early in project (Sprint 1-2)**:
- "Can the Bluetooth device API provide real-time book recognition, or is there a delay?"
- "Which digital reading platforms have APIs we can actually integrate with?" (Kindle yes, Kobo maybe, Audible no?)
- "How accurate is the book recognition technology? Should I design error states for 'book not recognized'?"
- "Does the device battery data update continuously or every few minutes?"

**Mid-project (Sprint 3-4)**:
- "This animation I mocked up—is it performance-feasible on mobile?"
- "I designed a 'source hit rate' percentage—can we calculate that from the data we have?"
- "Can we sync Kindle data in real-time, or is there a delay/frequency limit?"

**Late project (Sprint 5-6)**:
- "The spacing looks off in this implementation—can we adjust to match the mockup?"
- "This button color isn't accessible (contrast ratio too low)—can we use [alternative color]?"

### Programming Questions You'll Receive

**From them**:
- "What should the error message say if the device can't recognize the book?"
- "How should we handle a user who finishes a book on both the device AND Kindle (duplicate completion)?"
- "You designed a 'one-sentence feeling' prompt—is there a character limit?"
- "This design has 8px spacing here and 12px spacing there—is that intentional or should it be consistent?"

**How to respond**:
- Be specific: "Character limit for one-sentence feeling: 280 characters (like a tweet)"
- Provide design rationale: "8px spacing within a card, 12px between cards—creates visual grouping"
- Design for edge cases: "If duplicate completion detected, show: 'You finished this on [Device] and Kindle. Which date to keep?'"

### Where to Communicate

**Discord** (quick questions, daily updates):
- #orange-clearance channel (whole class sees)
- #bookmark-team channel (just your project team)

**GitHub Issues** (design feedback, bug reports):
- Create issue: "Button text color doesn't match mockup"
- Attach screenshot showing expected vs. actual
- Tag with `design-feedback` label

**Sprint Ceremonies** (structured collaboration):
- Use these for bigger discussions, not quick questions
- Come prepared with specific questions and mockups to review

**Email/Slack** (async detailed explanations):
- When you need to send multiple design files
- When explaining complex design rationale

---

## 6.4 Technical Constraints That Affect Design

**What Programming Students Might Tell You**

### IoT Device Constraints

**"Book recognition isn't instant—there's a 2-3 second delay while the camera processes OCR."**
- **Design impact**: Add loading state: "Recognizing book..." with spinner
- **User experience**: Set expectation that recognition takes a moment (not instant magic)

**"Bluetooth connection drops if user moves >30 feet from phone."**
- **Design impact**: Connection status indicator needed: "Device Connected" vs. "Reconnecting..."
- **User experience**: Design reconnection flow that's automatic and non-intrusive

**"Device battery lasts 20 hours, but continuous Bluetooth drains it faster."**
- **Design impact**: Battery indicator on home screen, low-battery warning
- **User experience**: Charging reminder when battery <15%

**"Camera can't recognize books in low light or if pages are wrinkled/damaged."**
- **Design impact**: Error state design: "Can't recognize book. Try better lighting or enter title manually"
- **User experience**: Fallback to manual entry always available

### API Constraints

**"Kindle API only syncs every 6 hours, not real-time."**
- **Design impact**: "Last synced 4 hours ago" timestamp, manual sync button
- **User experience**: Manage expectations—not instant like Bluetooth device

**"Apple Books API doesn't provide reading speed data, only completion status."**
- **Design impact**: Reading speed stats only available for device-tracked books, not Apple Books
- **User experience**: Explain data limitations in UI

**"We can't access Audible data—their API doesn't allow third-party apps."**
- **Design impact**: Audiobooks must be manually logged
- **User experience**: Manual entry form for audiobooks

### Database Performance

**"Querying 10,000 books for recommendation matching takes 3-5 seconds."**
- **Design impact**: Loading state for "Discover Your Next Read" button
- **User experience**: Skeleton screen or progress indicator while recommendations load

**"Recommendation algorithm needs at least 5 completed books to generate good suggestions."**
- **Design impact**: Empty state design: "Complete 5 books to unlock personalized recommendations"
- **User experience**: Show progress: "2 of 5 books completed"

---

## 6.5 Success Metrics for Bookmark Project

**How We Know Bookmark Succeeded**

### Design Quality Metrics

**Brand Identity Cohesion**:
- ✅ Logo, colors, typography consistent across all deliverables
- ✅ Visual identity feels sophisticated, not cozy-cute or corporate-sterile
- ✅ Brand Guidelines document clearly explains usage rules

**User Experience**:
- ✅ User can add book to TBR with source attribution in <30 seconds
- ✅ Device pairing flow takes <2 minutes
- ✅ One-sentence feeling capture feels quick, not burdensome
- ✅ Source analytics (hit rate) immediately understandable

**Accessibility**:
- ✅ All text meets WCAG AA contrast ratios (4.5:1 minimum)
- ✅ Font sizes readable on mobile (16px minimum body text)
- ✅ Interactive elements (buttons, links) have clear focus states

**Implementation Accuracy**:
- ✅ 90%+ of design specs implemented correctly (colors, spacing, typography match mockups)
- ✅ All designed screen states exist in app (empty, loading, error, success)
- ✅ Responsive design works on mobile, tablet, desktop

### Functional Success Metrics (Collaborative)

**Device Integration**:
- ✅ Smart reading light pairs with app successfully
- ✅ Book recognition works with >80% accuracy in good lighting
- ✅ Reading progress syncs automatically during sessions

**Recommendation Quality**:
- ✅ Users discover books outside their usual genres (Discovery Mode working)
- ✅ Source hit rate analysis accurately reflects recommendation success
- ✅ Feeling-based matching shows books readers with similar descriptors loved

**User Engagement** (if tested with real users):
- ✅ Users complete 5+ books (unlocking recommendation engine)
- ✅ Users tag recommendation sources when adding to TBR (source tracking adoption)
- ✅ Users write one-sentence feelings (not skipping reflection capture)

---

## 6.6 Troubleshooting Common Collaboration Challenges

### "Programming students say they can't build my design"

**Possible reasons**:
1. **Technical limitation**: API doesn't provide that data, device can't do that
2. **Time constraint**: It's technically possible but would take too long for this sprint
3. **Misunderstanding**: They misunderstood what you designed

**How to resolve**:
- Ask: "What's the specific constraint? Is it impossible or just time-intensive?"
- Offer alternatives: "If real-time sync isn't possible, can we do every 10 minutes?"
- Simplify if needed: "Can we launch with manual entry and add device sync in v2?"

### "My designs look different when implemented"

**Common causes**:
1. **Missing specs**: You didn't specify exact spacing/colors/fonts
2. **Asset quality**: Icons exported at wrong size, colors not exact
3. **Responsive issues**: Design looks good on desktop, breaks on mobile
4. **Time crunch**: They implemented quickly without checking mockups

**How to fix**:
- Provide clearer specs: Use Figma's Inspect mode for exact measurements
- Export assets correctly: SVG for scalability, PNG at 1x/2x/3x for mobile
- Design responsive layouts: Show mobile, tablet, desktop versions
- Do design QA: Review implemented work each sprint, give feedback early

### "We're not communicating enough"

**Symptoms**:
- Surprises at sprint review ("I didn't know you were designing that!")
- Duplicate work (you both designed the same screen)
- Misaligned expectations (you thought they were building X, they built Y)

**Solution**:
- **Daily standups** (5-minute check-ins): "What I'm working on today"
- **Shared workspace**: Figma file they can view anytime
- **Mid-sprint sync**: Show work-in-progress, don't wait until sprint review

---

## 6.7 Project Timeline & Milestones

**Recommended Schedule for Bookmark Project (8-Week Timeline)**

### Week 1-2: Discovery & Low-Fi Design
- **Design students**: Research competitors, create wireframes, define user flows
- **Programming students**: Set up Recommendation Engine platform, database schema
- **Together**: Sprint Planning, define MVP features
- **Milestone**: Wireframes approved, user flows documented

### Week 3-4: High-Fi Design & Asset Creation
- **Design students**: Apply brand identity to wireframes, create high-fi mockups, begin asset export
- **Programming students**: Build core CRUD (Create Read Update Delete) functionality for books, ratings, TBR
- **Together**: Design-Dev Sync (review mockups for feasibility)
- **Milestone**: High-fi mockups approved, brand identity finalized

### Week 5-6: Implementation & Device Integration
- **Design students**: Finish asset export, create component library, design device pairing flow
- **Programming students**: Implement designs, integrate Bluetooth device API, build recommendation engine
- **Together**: Daily check-ins as implementation happens
- **Milestone**: Core app implemented with brand identity, device pairing functional

### Week 7: Integration & Testing
- **Design students**: Design QA (compare implementation to mockups), create error state designs
- **Programming students**: Bug fixes, integrate Kindle/Apple Books APIs
- **Together**: User testing sessions (if available), Sprint Review demos
- **Milestone**: All major features working, design closely matches mockups

### Week 8: Polish & Launch Prep
- **Design students**: Create marketing materials (if part of deliverables), finalize Brand Guidelines
- **Programming students**: Performance optimization, final bug fixes
- **Together**: Final Sprint Review, project presentation, retrospective
- **Milestone**: Bookmark ready for portfolio, documented for handoff

---

## 6.8 Final Deliverables Checklist

**What Design Students Must Deliver by End of Project**

### Brand Identity Package
- ✅ Logo files (SVG, PNG at multiple sizes)
- ✅ Color palette (JSON file with hex codes)
- ✅ Typography system (CSS or design tokens)
- ✅ Brand Guidelines document (2-3 pages, shows proper usage)

### UI Design Files
- ✅ High-fidelity mockups (Figma/XD file, organized and labeled)
- ✅ All screen states designed (empty, loading, error, success)
- ✅ Responsive layouts (mobile, tablet, desktop)
- ✅ Component library (buttons, cards, forms styled)

### Exported Assets
- ✅ Icon set (all icons as SVG)
- ✅ App icons (iOS 1024x1024, Android 512x512)
- ✅ Mood tag icons and colors
- ✅ Device branding assets (logo for reading light)

### Design Specifications
- ✅ Typography specs (font sizes, weights, line heights)
- ✅ Spacing system (8px grid documented)
- ✅ Color usage guidelines (when to use primary vs. accent)
- ✅ Accessibility notes (contrast ratios verified)

### Optional Deliverables (If Chosen)
- ✅ Industrial design mockup (smart reading light product design)
- ✅ Packaging design (retail box for device)
- ✅ Marketing materials (print ads, social campaign, website landing page, etc.)
- ✅ Multi-page layout (user guide, pitch deck, brand manifesto, etc.)

### Documentation
- ✅ README file explaining asset organization
- ✅ Design rationale document (why you made key decisions)
- ✅ Known issues / future improvements list

---

**END OF TECHNICAL IMPLEMENTATION GUIDE**

For creative brief content, see **BookmarkAligned_core.md** (Parts 1-4).
