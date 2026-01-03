# LET'SEAT! - Technical Implementation (Parts 5-6)

**Platform:** Recommendation Engine (Preference-Learning System)
**White-Label Application:** Restaurant Discovery + Smart Dining Card
**Technical Purpose:** Platform Integration & Cross-Discipline Collaboration Guide
**Target Market:** Diners struggling with "what to eat?" decision fatigue
**Project Classification:** ORANGE Clearance
**Last Updated:** January 2026

---

## ABOUT THIS DOCUMENT

This document is **Part 2 of 2** of the LetsEatAligned brief:

1. **LetsEatAligned_core.md** - Parts 1-4: Creative Brief, Product Deep Dive, User Research, Strategic Guidance
2. **LetsEatAligned_technical.md** (this document) - Parts 5-6: Technical Implementation Context, Cross-Discipline Workflow

**Purpose**: This document provides the technical mapping between Let'sEat! (the restaurant recommendation system with smart dining card) and the underlying Recommendation Engine Platform built by CTS programming students.

---

# PART 5: TECHNICAL IMPLEMENTATION CONTEXT

## Overview: Bridging Design to Development

Let'sEat! is one of several white-label configurations of the **Recommendation Engine Platform™**. Your design work will be implemented through configuration, theming, and feature toggles—not custom code.

**Key insight:** Let'sEat! uses the same database, recommendation logic, and core features as Bookmark™, SkillOptimizer™, and other applications. What differentiates Let'sEat! is its dining/restaurant focus, automatic POS card tracking, spending analytics, and decision-fatigue-solving positioning.

---

## 5.1 Engine Capability Mapping

### Items → Restaurants

**Platform capability:** CRUD operations for items with attributes, categories, user ratings, and recommendation generation.

**Let'sEat! mapping:**
- Item = **Restaurant**
- Standard item fields:
  - `title` → Restaurant name
  - `creator` → Restaurant owner/chef (optional)
  - `item_type` → Restaurant category (Fast casual, Fine dining, Cafe, Food truck, etc.)
  - `description` → Restaurant description, specialties
  - `image_url` → Restaurant photo or logo
  - `external_id` → Yelp ID, Google Maps place ID, or POS system ID
- Additional metadata fields:
  - `cuisine_type` (Mexican, Thai, Italian, American, Fusion, etc.)
  - `price_range` ($ = under $10, $$ = $10-20, $$$ = $20-35, $$$$ = $35+)
  - `service_speed` (Fast <15min, Medium 15-30min, Slow 30min+)
  - `address` (full address for mapping/directions)
  - `phone` (for reservations)
  - `hours` (JSON: operating hours by day)
  - `average_wait_time` (calculated from user data)
  - `accepted_at_count` (how many users have visited—popularity signal)

**Design implications:**
- Restaurant cards prominently display name, cuisine type, price range
- Service speed indicator (fast/medium/slow) for decision-making
- Address/directions integration prominent
- User visit frequency shown: "You've been here 6 times"

### Ratings → Dining Experiences

**Platform capability:** User ratings with numerical scale, written reviews, timestamps, and recommendation engine learning.

**Let'sEat! mapping:**
- Rating = **Dining Experience** (what you ate, how you felt about it)
- Quick rating (5-star or thumbs up/down) labeled as "Would you go back?"
- **What you ordered** (text field): Itemized order captured from POS card swipe (automatic)
- **How was it?** (optional text field): "Carnitas were incredible" | "Service was slow"
- **Occasion** (dropdown): Solo lunch | Date night | Family dinner | Business meal | Quick bite
- **Spending amount** (captured automatically from card): Total including tip
- **Visit date** (captured automatically from card)
- **Would avoid?** (boolean): Mark restaurants you don't want suggested again
- **Favorite dishes** (multi-select from order): Which items would you reorder?

**Design implications:**
- Order details auto-populated (no manual entry needed)
- "How was it?" prompt feels conversational, not homework
- Occasion tagging for filtering: "Show me date night restaurants"
- Spending shown but not judgmental: "You spent $45" (neutral tone)
- Visual hierarchy: what you ordered (auto-filled) > how was it > occasion
- Quick "mark as avoid" for bad experiences (never suggest again)

### Attributes → Cuisine & Dining Tags

**Platform capability:** Multi-valued attributes that categorize items, enable filtering, and power recommendation similarity matching.

**Let'sEat! mapping:**
- Attributes = **Cuisine Types, Price Ranges, Service Speeds, Dietary Tags, Occasion Tags**
- **Cuisine tags:** Mexican, Thai, Italian, Chinese, Japanese, Indian, American, Mediterranean, Vietnamese, Ethiopian, etc.
- **Price tags:** $ (under $10pp), $$ ($10-20), $$$ ($20-35), $$$$ ($35+)
- **Service speed tags:** Fast (<15min), Medium (15-30min), Slow (30min+)
- **Dietary tags:** Vegetarian options, Vegan friendly, Gluten-free available, Spicy available, Halal, Kosher
- **Occasion tags:** Date night appropriate, Family-friendly, Kid menu, Business lunch suitable, Quick solo lunch
- Each attribute has:
  - `attribute_name` (specific tag)
  - `attribute_category` (cuisine, price, speed, dietary, occasion)
  - `color_code` (for visual consistency)
  - `icon` (visual indicator—cuisine icons, dollar signs, speed indicators)

**Design implications:**
- Cuisine tags use food-related colors (warm earth tones, not finance blue)
- Price tags use $ symbols (clear at-a-glance budgeting)
- Service speed tags use clock/timer icons
- Tag selection multi-select (restaurants can have multiple tags)
- Visual differentiation: cuisine warm colors, price neutral, dietary green
- Tags searchable/filterable: "Show me fast, cheap Mexican restaurants"

### Recommendations → "What Should I Eat?" Suggestions

**Platform capability:** Algorithm generates personalized suggestions based on user ratings, attribute preferences, and similarity patterns.

**Let'sEat! mapping:**
- Recommendation = **"What Should I Eat?" Suggestion** with context-aware reasoning
- Recommendation reasoning displayed: "Based on your pattern: loves spicy + quick service + under $15"
- **Decision-making flow:** User answers 3 questions → App suggests 3 restaurants
  - Question 1: Solo or with others? (filters to solo-friendly vs. group-appropriate)
  - Question 2: How much time? (filters by service speed)
  - Question 3: What mood? (Quick bite, Casual meal, Nice dinner)
- **Pattern-based suggestions:**
  - "You get tacos every Tuesday—here are your favorite 3 taco spots"
  - "You love spicy food and haven't had Thai in 2 weeks—try this"
  - "You always order vegetarian at Indian restaurants—this place has great options"
- **Discovery Mode:** Suggests restaurants OUTSIDE usual patterns but matching deeper preferences (price + speed + flavor profile)
- Recommendations include:
  - Restaurant details (name, cuisine, price, service speed)
  - **Why this recommendation** (specific reason: "You've been here 6 times" or "Similar to your favorites")
  - **What you usually order** (if returning): "You always get the pad thai here"
  - **Distance/travel time** (based on current location)
  - **Estimated spending** (based on your average order at this restaurant or similar restaurants)

**Design implications:**
- "What Should I Eat?" button LARGE and prominent on home screen (primary action)
- 3-question flow visual not text-heavy (quick decision, not form-filling)
- Reasoning explanation given visual emphasis (this is the intelligence)
- "You've been here X times" social proof from YOUR history, not strangers
- Easy actions: "Let's go!" | "Pick for me" | "Show me something else"
- Discovery Mode toggle easy to access ("Surprise me with something new")

### Sources → Recommendation Sources (Friends, Influencers)

**Platform capability:** Track where items come from, analyze source reliability, filter by source.

**Let'sEat! mapping:**
- Source = **Friend or Influencer who recommended restaurant**
- Source types:
  - **Friends** (individual people)
  - **Food Influencers** (Instagram accounts, food bloggers, TikTok)
  - **Publications** (Food magazines, local food blogs)
  - **"I discovered it"** (self-discovery through app or driving by)
- Source tracking data:
  - `source_name` (friend name, influencer handle)
  - `source_type` (friend, influencer, publication, self)
  - `recommendation_count` (how many restaurants from this source tried)
  - `hit_rate` (% of their recommendations you loved)
  - `last_hit` (most recent restaurant from this source you loved)

**Design implications:**
- Friend recommendations can be sent in-app: "Try this place!"
- Source hit rate displayed: "Sarah's recommendations: 80% hit rate (4 of 5 loved)"
- Filter by high-performing sources: "Show me restaurants Sarah recommended"
- Easy source tagging when trying new place: "Who recommended this?"

### User Profiles → Dining Profiles

**Platform capability:** User accounts with preferences, history, and personalization data.

**Let'sEat! mapping:**
- User Profile = **Dining Profile** (your complete dining identity)
- Profile contains:
  - **Dining history** (all meals tracked via card, complete with orders and spending)
  - **Favorite restaurants** (based on repeat visits)
  - **Avoid list** (restaurants marked as "don't suggest")
  - **Dietary patterns** (vegetarian, loves spicy, avoids seafood—learned from orders)
  - **Price comfort zone** (average spending per meal, calculated)
  - **Cuisine distribution** (pie chart: 40% Mexican, 30% Thai, 20% American, 10% other)
  - **Day-of-week patterns** (Taco Tuesday, date night Friday—detected automatically)
  - **Spending totals** (monthly/yearly dining spending)
  - **Dining goals** (budget limits, try-new-cuisines challenges)
  - **Couple/family sharing** (linked accounts for shared history)
  - **Card sync status** (connected dining card, last sync time)
- Connected accounts:
  - NFC dining card pairing
  - Optional: DoorDash/Uber Eats integration (if API available)
  - Optional: Yelp import (one-time to seed history)

**Design implications:**
- Dashboard shows dining profile at-a-glance: recent meals, spending this month, favorite cuisines
- "Your Dining Patterns" visualizations: cuisine distribution, price comfort zone, day patterns
- Card connection status visible: "Card synced 10 minutes ago"
- Budget tracking: "You've spent $680 of $800 budget this month"
- Cuisine diversity tracking: "You've tried 7 different cuisines this month!"
- Couple mode toggle: "Switch to couple view" vs. "Your view"

---

## 5.2 Database Entity Alignment

### Restaurants (Items Table)

```sql
CREATE TABLE items (
    id SERIAL PRIMARY KEY,
    title VARCHAR(500) NOT NULL,  -- Restaurant name
    creator VARCHAR(300),  -- Owner/chef (optional)
    description TEXT,
    image_url VARCHAR(500),  -- Restaurant photo
    external_id VARCHAR(100),  -- Yelp/Google Maps ID
    item_type VARCHAR(50),  -- 'fast_casual', 'fine_dining', etc.
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);
```

**Let'sEat!-specific fields** (JSON metadata or separate columns):
- `cuisine_type` (Mexican, Thai, Italian, etc.)
- `price_range` ($, $$, $$$, $$$$)
- `service_speed` (Fast, Medium, Slow)
- `address` (full address for mapping)
- `phone` (for reservations)
- `hours` (JSON: {monday: "11am-9pm", tuesday: "11am-9pm", ...})
- `average_wait_time` (calculated from user data)
- `dietary_tags` (Array: ['Vegetarian options', 'Gluten-free', 'Spicy available'])

### Dining Experiences (Ratings Table)

```sql
CREATE TABLE ratings (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    item_id INT REFERENCES items(id),  -- Restaurant
    rating_value DECIMAL(2,1),  -- 1.0 to 5.0 stars
    review_text TEXT,  -- "How was it?" notes
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);
```

**Let'sEat!-specific extensions**:
- `order_items` JSONB  -- Array of dishes ordered (from POS card data)
- `occasion` VARCHAR(50)  -- 'solo_lunch', 'date_night', 'family_dinner', 'business_meal'
- `spending_amount` DECIMAL(8,2)  -- Total including tip (from card)
- `visit_date` DATE  -- When dined (from card)
- `would_avoid` BOOLEAN  -- Don't suggest this restaurant again
- `favorite_dishes` JSONB  -- Array of dishes user would reorder
- `synced_from_card` BOOLEAN  -- True if captured via POS card
- `card_transaction_id` VARCHAR(100)  -- Reference to card swipe data

### Dining Card Tracking (New Table)

```sql
CREATE TABLE dining_cards (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    card_number VARCHAR(20) UNIQUE,  -- Physical card identifier
    card_type VARCHAR(50),  -- 'standard', 'premium_metal', etc.
    is_active BOOLEAN DEFAULT true,
    last_sync TIMESTAMP,
    created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE card_transactions (
    id SERIAL PRIMARY KEY,
    card_id INT REFERENCES dining_cards(id),
    user_id INT REFERENCES users(id),
    restaurant_name VARCHAR(500),
    restaurant_location VARCHAR(500),  -- Address from POS
    order_items JSONB,  -- Itemized order from POS
    total_amount DECIMAL(8,2),
    transaction_date TIMESTAMP,
    pos_system VARCHAR(50),  -- 'Square', 'Toast', 'Clover', etc.
    is_processed BOOLEAN DEFAULT false,  -- Has user confirmed/edited this?
    created_at TIMESTAMP DEFAULT NOW()
);
```

**Card transaction flow**:
1. User swipes card at restaurant
2. POS system sends data to Let'sEat! (restaurant name, order, amount, date)
3. Data stored in `card_transactions` table
4. User taps card on phone (NFC sync) or app auto-syncs via Bluetooth
5. App shows transaction: "You ate at [Restaurant]. Confirm details?"
6. User confirms → creates entry in `ratings` table linked to restaurant
7. Transaction marked `is_processed = true`

---

## 5.3 Configuration Layer (YAML for White-Label Theming)

```yaml
# config/letseat.yml
application:
  name: "Let'sEat!"
  tagline: "Never wonder 'What should I eat?' again"
  logo_url: "/assets/letseat-logo.svg"
  primary_color: "#D64E12"  # Burnt orange (food warmth + energy)
  accent_color: "#4A7C59"   # Deep green (fresh, appetite)
  font_primary: "Poppins, system-ui, sans-serif"  # Friendly but modern
  font_secondary: "Inter, system-ui, sans-serif"  # Body text

item_config:
  item_name_singular: "restaurant"
  item_name_plural: "restaurants"
  creator_label: "owner/chef"
  default_image: "/assets/default-restaurant.png"
  required_fields: ['title', 'cuisine_type', 'price_range', 'address']
  optional_fields: ['phone', 'hours', 'service_speed']

rating_config:
  rating_scale: "stars"  # 1-5 stars
  rating_label: "Would you go back?"
  review_prompt: "How was it?"
  secondary_prompts:
    - label: "What did you order?"
      field: "order_items"
      auto_filled: true  # Captured from card
    - label: "Occasion"
      field: "occasion"
      options: ['Solo lunch', 'Date night', 'Family dinner', 'Business meal', 'Quick bite']
  enable_spending_tracking: true
  enable_avoid_list: true

card_integration:
  enable_physical_card: true
  card_types:
    - type: "standard_plastic"
      name: "Standard Card"
      price: 49.99
    - type: "premium_metal"
      name: "Premium Metal Card"
      price: 99.99
  pos_systems_supported:
    - "Square"
    - "Toast"
    - "Clover"
    - "Lightspeed"
    - "TouchBistro"
  auto_sync_method: "nfc_tap"  # or 'bluetooth_auto'
  require_user_confirmation: true  # Show transaction for approval before saving

recommendation_config:
  algorithm_mode: "pattern_matching_with_decision_flow"
  decision_questions:
    - question: "Solo or with others?"
      options: ['Solo', 'With partner/friend', 'Family/group']
    - question: "How much time do you have?"
      options: ['Quick (<15min)', 'Normal (30min)', 'Leisurely (1hr+)']
    - question: "What mood?"
      options: ['Quick bite', 'Casual meal', 'Nice dinner']
  enable_discovery_mode: true
  recommendation_reasons: true
  spending_insights: true
  couple_mode: true

privacy_config:
  default_privacy: "private"
  social_features: "opt-in"
  spending_data_visibility: "user_only"
  export_formats: ['CSV', 'PDF', 'IRS_business_meal_format']

ui_customizations:
  home_screen_widgets:
    - "what_should_i_eat_button"  # PRIMARY ACTION
    - "recent_meals"
    - "spending_this_month"
    - "favorite_restaurants"
  navigation_items:
    - label: "Decide"
      route: "/decision"
    - label: "History"
      route: "/dining-history"
    - label: "Spending"
      route: "/spending"
    - label: "Card"
      route: "/card-sync"
  button_labels:
    add_item: "Add Restaurant (Manual)"  # Rare—card does this
    rate_item: "How Was It?"
    view_recommendations: "What Should I Eat?"
    sync_card: "Sync Card"
```

---

## 5.4 Asset Delivery Specifications

### Brand Identity Assets

**Logo Files**:
- `letseat-logo-full.svg` (wordmark + logomark if applicable)
- `letseat-logo-icon.svg` (icon only, for app)
- All as SVG and PNG (1x, 2x, 3x)

**Color Palette** (`colors.json`):
```json
{
  "primary": "#D64E12",
  "accent": "#4A7C59",
  "success": "#27AE60",
  "warning": "#F39C12",
  "error": "#E74C3C",
  "neutral_dark": "#2C3E50",
  "neutral_light": "#ECF0F1",
  "background": "#FFFFFF",
  "text_primary": "#2C3E50",
  "text_secondary": "#7F8C8D",
  "price_low": "#27AE60",
  "price_medium": "#F39C12",
  "price_high": "#E74C3C"
}
```

**Typography** (`typography.css`):
```css
h1, h2, h3 { font-family: 'Poppins', system-ui, sans-serif; }
body, p { font-family: 'Inter', system-ui, sans-serif; }
.restaurant-name { font-family: 'Poppins', sans-serif; font-weight: 600; }
.order-items { font-family: 'Inter', sans-serif; font-style: italic; }
```

### Dining Card Design Assets

**Physical Card Mockup**:
- Front design (3.375" × 2.125"): Logo placement, card number, NFC indicator
- Back design: Magnetic stripe, instructions ("Swipe before payment"), customer service QR code
- Material specs: PVC plastic (standard) or stainless steel (premium metal)
- Finish: Matte soft-touch coating (plastic) or brushed finish (metal)
- Color: Burnt orange (#D64E12) base with white/cream text

**Card Packaging**:
- Sliding drawer box or magnetic closure
- Window showing card
- Quick-start guide included
- NFC pairing instructions

**Icon Set**:
- `icon-card.svg` (dining card)
- `icon-sync.svg` (NFC tap)
- `icon-restaurant.svg`
- `icon-spending.svg` (budget tracking)
- `icon-fast.svg`, `icon-medium.svg`, `icon-slow.svg` (service speed)
- `icon-price-$.svg` through `icon-price-$$$$.svg`
- Cuisine icons: `icon-mexican.svg`, `icon-thai.svg`, etc.

---

## 5.5 API Integration Points

### Dining Card (NFC/Bluetooth)

**Connection Method**: NFC tap-to-sync or Bluetooth Low Energy

**Data Flow**:
1. User swipes card at restaurant POS
2. POS system sends transaction data to Let'sEat! servers (via card chip)
3. Data queued for next sync
4. User taps card on phone (NFC) or app auto-syncs (Bluetooth)
5. App retrieves transaction data, shows confirmation screen
6. User confirms/edits → saved to dining history

**Technical Requirements for Designers**:
- Design NFC pairing flow: "Tap card on back of phone"
- Design sync confirmation: "You ate at [Restaurant]. Order: [Items]. Confirm?"
- Design edit flow: "Restaurant name wrong? Edit here"
- Design sync status: "Last synced 5 minutes ago"

### Restaurant POS Integration (Fictitious/Aspirational)

**Connection Method**: POS system API (Square, Toast, Clover)

**Data Retrieved**:
- Restaurant name and location
- Itemized order (line items: "Carnitas Tacos x2", "Chips & Guac", "Horchata")
- Total amount (including tip)
- Transaction timestamp

**Reality Check**: This level of POS integration is aspirational. Design as if it works perfectly.

### Google Maps / Yelp APIs (For Restaurant Data)

**Connection Method**: REST APIs

**Use Case**: When user manually adds restaurant (didn't use card), app fetches:
- Restaurant name
- Address
- Phone
- Hours
- Photos
- Cuisine type
- Price range

### DoorDash / Uber Eats Integration (Stretch Goal)

**Connection Method**: Account linking (if APIs available)

**Data Retrieved**:
- Delivery order history
- Restaurants ordered from
- Items ordered
- Spending

**Design Requirement**: "Connect Delivery Apps" settings page

---

# PART 6: CROSS-DISCIPLINE WORKFLOW

## 6.1 Sprint Touchpoints & Collaboration Ceremonies

(Follows same structure as Bookmark—omitted for brevity)

**Key Difference for Let'sEat!**: More emphasis on card-app sync flow design and POS integration discussions.

---

## 6.2 Design Handoff Process

(Follows same structure as Bookmark—omitted for brevity)

**Let'sEat!-Specific Assets**:
- Physical card design mockup (front/back, materials specified)
- Card packaging design
- NFC sync flow (screen-by-screen interaction design)
- Decision-making flow (3 questions → 3 suggestions)

---

## 6.3 Communication Protocols

**Questions for Programming Students**:
- "Can POS systems actually provide itemized order data via card swipe?"
- "How accurate is automatic restaurant name capture from POS?"
- "What happens if user forgets to swipe card—can they manually log?"
- "How does couple mode handle two cards syncing to one account simultaneously?"

---

## 6.4 Technical Constraints That Affect Design

**POS Integration Constraints**:
- "Not all POS systems support data capture—some restaurants won't work"
  - **Design impact**: Need manual entry fallback, "Add restaurant manually" always available
- "Itemized orders might not always capture dish names accurately"
  - **Design impact**: Edit flow must be simple: "Carnitas Tacoz" → "Carnitas Tacos"
- "Card might need to be swiped at specific point in transaction (before payment processed)"
  - **Design impact**: Instructions need to be crystal clear: "Swipe BEFORE you pay"

**NFC/Bluetooth Constraints**:
- "NFC tap requires phone in specific position relative to card"
  - **Design impact**: Animated instructions showing tap location
- "Bluetooth auto-sync drains battery faster"
  - **Design impact**: Option to disable auto-sync, use manual tap instead

---

## 6.5 Success Metrics

**Design Quality**:
- ✅ Card design feels premium (justifies $50-100 price point)
- ✅ "What Should I Eat?" decision flow takes <30 seconds to complete
- ✅ NFC sync flow takes <10 seconds from tap to confirmation

**Functional Success** (Collaborative):
- ✅ Card captures restaurant data correctly >80% of time
- ✅ Recommendation suggestions match user's actual preferences (validated through testing)
- ✅ Spending tracking accurate (matches credit card statements)

---

## 6.6 Final Deliverables Checklist

**Brand Identity Package**:
- ✅ Logo files (SVG, PNG)
- ✅ Color palette JSON
- ✅ Typography CSS
- ✅ Brand Guidelines (2-3 pages)

**Physical Product Design**:
- ✅ Dining card design (front/back mockup, materials specified)
- ✅ Card packaging design

**UI Design Files**:
- ✅ High-fidelity mockups (decision flow, history, spending, card sync)
- ✅ All screen states (empty, loading, error, success)
- ✅ Responsive layouts

**Exported Assets**:
- ✅ Icon set (cuisine, price, speed, spending, card)
- ✅ App icon

---

**END OF TECHNICAL IMPLEMENTATION GUIDE**

For creative brief content, see **LetsEatAligned_core.md** (Parts 1-4).
