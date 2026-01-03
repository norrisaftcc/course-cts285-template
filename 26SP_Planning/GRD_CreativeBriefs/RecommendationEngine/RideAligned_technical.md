# RIDE - Technical Implementation (Parts 5-6)

**Platform:** Recommendation Engine (Preference-Learning System)
**White-Label Application:** Vehicle Comparison Shopping + Smart Scanner Key Fob
**Technical Purpose:** Platform Integration & Cross-Discipline Collaboration Guide
**Target Market:** Car shoppers navigating dealer pressure and feature overload
**Project Classification:** ORANGE Clearance
**Last Updated:** January 2026

---

## ABOUT THIS DOCUMENT

This document is **Part 2 of 2** of the RideAligned brief:

1. **RideAligned_core.md** - Parts 1-4: Creative Brief, Product Deep Dive, User Research, Strategic Guidance
2. **RideAligned_technical.md** (this document) - Parts 5-6: Technical Implementation Context, Cross-Discipline Workflow

**Purpose**: This document provides the technical mapping between Ride (the vehicle comparison system with smart scanner key fob + browser extension) and the underlying Recommendation Engine Platform built by CTS programming students.

---

# PART 5: TECHNICAL IMPLEMENTATION CONTEXT

## Overview: Bridging Design to Development

Ride is one of several white-label configurations of the **Recommendation Engine Platform™**. What differentiates Ride is its **three-component ecosystem** (IoT scanner + browser tool + mobile app), **adversarial positioning** (protecting buyers FROM dealer manipulation), and **multi-phase workflow** (research → dealership → decision).

---

## 5.1 Engine Capability Mapping

### Items → Vehicles

**Platform capability:** CRUD operations for items with attributes, categories, user ratings, and recommendation generation.

**Ride mapping:**
- Item = **Vehicle** (specific car at specific dealer, OR online listing)
- Standard item fields:
  - `title` → Make + Model + Year + Trim (e.g., "2024 Honda CR-V EX-L")
  - `creator` → Dealer name or online listing source
  - `item_type` → Vehicle category (SUV, Sedan, Truck, Electric, etc.)
  - `description` → Dealer notes or listing description
  - `image_url` → Vehicle photo (from listing or user upload)
  - `external_id` → VIN (most critical for matching online to dealer)
- Additional metadata fields:
  - `vin` (17-character Vehicle Identification Number—unique identifier)
  - `msrp` (manufacturer's suggested retail price)
  - `dealer_price` (actual asking price at dealer)
  - `online_listing_price` (price shown in original online listing—for comparison)
  - `features` (JSON array: safety features, tech features, comfort features)
  - `mpg_city` / `mpg_highway`
  - `engine_specs`
  - `trim_level`
  - `source_type` ('online_listing', 'dealer_scanned', 'manual_entry')
  - `source_url` (link to original listing if from browser extension)
  - `scan_timestamp` (when key fob captured data)
  - `price_discrepancy` (calculated: dealer_price - online_listing_price)
  - `missing_features` (features shown online but not on dealer car)

**Design implications:**
- Vehicle cards show make/model/year prominently
- Price comparison highlighted: "$27,500 online → $29,800 dealer (+$2,300)"
- Feature checklist with visual indicators: ✅ Has feature, ❌ Missing, ⚠️ Discrepancy
- VIN displayed for verification
- Source badge: "Scanned at AutoNation" or "Saved from Cars.com"

### Ratings → Test Drive Experiences

**Platform capability:** User ratings with numerical scale, written reviews, timestamps, and recommendation engine learning.

**Ride mapping:**
- Rating = **Test Drive Experience** (your impression of specific vehicle)
- Quick rating (5-star or thumbs) labeled as "Would you buy this?"
- **Driving impressions** (text field): "Good visibility," "Tight steering," "Noisy at highway speed"
- **Feature verification** (checkboxes): Which promised features did you actually see/test?
- **Dealer experience** (dropdown): Helpful, Neutral, Pushy, Deceptive
- **Pressure tactics used** (multi-select): "Price expires today," "Another buyer interested," "Manager special," None
- **Visit date** (captured automatically if using scanner, manual if not)
- **Would revisit?** (boolean)

**Design implications:**
- Test drive notes quick and casual ("Good visibility" not essay)
- Feature verification checklist auto-populated from scan
- Dealer experience tracking helps other Ride users
- Pressure tactic tagging builds database of dealer behavior
- Visual hierarchy: driving impressions > feature verification > dealer experience

### Attributes → Vehicle Features & Shopping Priorities

**Platform capability:** Multi-valued attributes that categorize items, enable filtering, and power recommendation similarity matching.

**Ride mapping:**
- Attributes = **Vehicle Features, Safety Tech, Price Ranges, Priorities**
- **Feature tags:** Blind-spot monitoring, Adaptive cruise control, Lane keeping assist, 360 camera, Heated seats, Sunroof, etc.
- **Safety tags:** Forward collision warning, Automatic emergency braking, Pedestrian detection, etc.
- **Price ranges:** Under $25K, $25-35K, $35-45K, $45K+
- **Vehicle categories:** Compact SUV, Mid-size SUV, Sedan, Truck, Electric, Hybrid
- **Priority tags** (user-defined): Safety first, Family hauling, Budget max, Fuel economy, Tech features, Reliability
- Each attribute has:
  - `attribute_name` (specific feature/tag)
  - `attribute_category` (feature, safety, price, vehicle_type, priority)
  - `is_priority` (boolean: did user rank this in top priorities?)
  - `priority_rank` (1-10 if user prioritized)

**Design implications:**
- Priority tags use distinctive styling (user's top 3 priorities highlighted in gold)
- Feature tags show availability: ✅ Standard, 💰 Upgrade package, ❌ Not available
- Safety tags grouped separately (critical decision factor)
- Price tags use color coding (green = budget-friendly, red = over budget)
- Visual differentiation: priorities bold, features neutral, safety distinct

### Recommendations → "Best Match" Suggestions

**Platform capability:** Algorithm generates personalized suggestions based on user ratings, attribute preferences, and similarity patterns.

**Ride mapping:**
- Recommendation = **Best Match Vehicle** based on ranked priorities
- Recommendation reasoning displayed: "Matches 8 of 10 top priorities, $2K under budget, strong safety ratings"
- **Priority scoring:** How many of user's ranked priorities does each vehicle match?
- **Compromise alerts:** "Honda matches 9/10 priorities but missing heated seats (priority #7)"
- **Budget fit:** Within budget? How much under/over?
- **Deal quality:** Fair market value comparison (is dealer overcharging?)
- **Reliability data:** Consumer Reports scores, recall history
- Recommendations include:
  - Vehicle details (make/model/year, price, dealer)
  - **Why recommended** (priority match score, specific features that align)
  - **Trade-offs** (what you're giving up vs. alternatives)
  - **Negotiation leverage** (online vs. dealer price discrepancy, competitor pricing)

**Design implications:**
- "Best Match" badge on top-scoring vehicle
- Priority match visualization: "8 of 10 ✅"
- Trade-off comparison: "Honda vs. Mazda: Honda wins on safety, Mazda wins on price"
- Deal quality alert: ⚠️ "$2,200 over fair market value"
- Easy actions: "Go back to dealer," "Make offer," "Need more test drives"

### Sources → Online Listings & Dealerships

**Platform capability:** Track where items come from, analyze source reliability, filter by source.

**Ride mapping:**
- Source = **Online Listing Site or Dealership**
- Source types:
  - **Online Listing Sites** (Autotrader, Cars.com, dealer websites)
  - **Dealerships** (specific dealer locations—AutoNation Springfield, CarMax Downtown)
  - **Private Sellers** (Craigslist, Facebook Marketplace—if supported)
- Source tracking data:
  - `source_name` (website or dealer name)
  - `source_type` (online_listing, dealership, private_seller)
  - `reliability_score` (calculated from user experiences—honest pricing? Bait-and-switch incidents?)
  - `pressure_tactic_frequency` (how often users report pressure at this dealer)
  - `price_honesty` (how often online price matches dealer reality)

**Design implications:**
- Dealer reputation badges: "✅ Honest pricing" or "⚠️ Frequent bait-and-switch"
- Source filter: "Show only honest dealers"
- Cross-reference prominence: "Online listing (Cars.com) vs. Dealer reality"

### User Profiles → Car Shopping Profiles

**Platform capability:** User accounts with preferences, history, and personalization data.

**Ride mapping:**
- User Profile = **Car Shopping Profile** (your priorities, budget, timeline)
- Profile contains:
  - **Shopping timeline** (when did you start? How urgent?)
  - **Budget** (max price, financing pre-approval status)
  - **Ranked priorities** (1-10: safety, space, tech, fuel economy, etc.)
  - **Must-haves** (deal-breaker features: third row, AWD, etc.)
  - **Test drive history** (vehicles tested, impressions, dealer experiences)
  - **Shortlist** (vehicles under consideration from browser extension)
  - **Scanner fob pairing** (connected device, last sync time)
  - **Browser extension status** (installed, active listings tracked)
  - **Credit union rates** (optional: pre-approval info for financing comparison)

**Design implications:**
- Dashboard shows shopping status: "Day 45 of shopping, 6 vehicles tested, 2 strong contenders"
- Priority visualization: Top 3 priorities always visible
- Budget tracker: "3 vehicles within budget, 2 over"
- Timeline reminder: "You tested Honda 3 weeks ago—time to revisit?"

---

## 5.2 Database Entity Alignment

### Vehicles (Items Table)

```sql
CREATE TABLE items (
    id SERIAL PRIMARY KEY,
    title VARCHAR(500) NOT NULL,  -- Make/Model/Year/Trim
    creator VARCHAR(300),  -- Dealer name or listing source
    description TEXT,
    image_url VARCHAR(500),
    external_id VARCHAR(100),  -- VIN (critical)
    item_type VARCHAR(50),  -- 'suv', 'sedan', 'truck', 'electric'
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);
```

**Ride-specific fields**:
- `vin` VARCHAR(17) UNIQUE
- `msrp` DECIMAL(10,2)
- `dealer_price` DECIMAL(10,2)
- `online_listing_price` DECIMAL(10,2)
- `price_discrepancy` DECIMAL(10,2)  -- Calculated field
- `features` JSONB  -- Array of feature objects
- `mpg_city` INT
- `mpg_highway` INT
- `source_type` VARCHAR(50)  -- 'online_listing', 'dealer_scanned', 'manual'
- `source_url` VARCHAR(500)
- `scan_timestamp` TIMESTAMP

### Scanner Device Tracking (New Table)

```sql
CREATE TABLE scanner_devices (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    device_serial VARCHAR(50) UNIQUE,
    device_type VARCHAR(50),  -- 'standard', 'premium'
    is_paired BOOLEAN DEFAULT false,
    last_sync TIMESTAMP,
    battery_level INT,  -- 0-100
    created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE scan_transactions (
    id SERIAL PRIMARY KEY,
    device_id INT REFERENCES scanner_devices(id),
    user_id INT REFERENCES users(id),
    scan_type VARCHAR(50),  -- 'window_sticker', 'spec_sheet', 'qr_code'
    raw_scan_data TEXT,  -- OCR output before processing
    extracted_vin VARCHAR(17),
    extracted_price DECIMAL(10,2),
    extracted_features JSONB,
    scan_quality_score INT,  -- 0-100 (OCR confidence)
    requires_user_confirmation BOOLEAN DEFAULT true,
    is_processed BOOLEAN DEFAULT false,
    scan_location VARCHAR(200),  -- GPS coordinates (optional)
    created_at TIMESTAMP DEFAULT NOW()
);
```

**Scanner flow**:
1. User presses button on key fob scanner
2. Camera captures document (window sticker)
3. OCR processing extracts data (VIN, price, features)
4. Data stored in `scan_transactions` with quality score
5. User opens app, sees: "New scan from AutoNation. Confirm details?"
6. User confirms/edits → creates vehicle entry in `items` table
7. Transaction marked `is_processed = true`

### Browser Extension Captures (New Table)

```sql
CREATE TABLE browser_captures (
    id SERIAL PRIMARY KEY,
    user_id INT REFERENCES users(id),
    source_url VARCHAR(500),
    capture_timestamp TIMESTAMP DEFAULT NOW(),
    extracted_data JSONB,  -- All listing data
    vin VARCHAR(17),  -- If available in listing
    is_added_to_shortlist BOOLEAN DEFAULT false,
    created_at TIMESTAMP DEFAULT NOW()
);
```

---

## 5.3 Configuration Layer (YAML)

```yaml
# config/ride.yml
application:
  name: "Ride"
  tagline: "Your priorities, your decision, your control"
  logo_url: "/assets/ride-logo.svg"
  primary_color: "#2C5F8D"  -- Confident blue (trust, protection)
  accent_color: "#E85D75"   -- Alert red (warnings, discrepancies)
  font_primary: "Inter, system-ui, sans-serif"  -- Professional clarity

item_config:
  item_name_singular: "vehicle"
  item_name_plural: "vehicles"
  creator_label: "dealer/source"
  required_fields: ['title', 'vin', 'dealer_price']

scanner_integration:
  enable_physical_scanner: true
  scanner_types:
    - type: "standard"
      price: 59.99
    - type: "premium"
      price: 79.99
  ocr_confidence_threshold: 75  -- Require user confirmation if below
  auto_cross_reference: true  -- Match scans to online listings automatically

browser_extension:
  supported_browsers: ['Chrome', 'Firefox', 'Safari', 'Edge']
  supported_sites:
    - 'autotrader.com'
    - 'cars.com'
    - 'cargurus.com'
    - '*.dealerwebsites.com'
  capture_interval: 500ms  -- Delay before scraping page

cross_reference_config:
  enable_price_alerts: true
  price_alert_threshold: 1000  -- Alert if dealer price > $1000 over online
  enable_feature_alerts: true
  enable_bait_switch_detection: true
  vin_matching_priority: true  -- VIN match > fuzzy match

financing_calculator:
  enable_financing_comparison: true
  default_credit_score_range: 700-750
  rate_sources:
    - 'user_credit_union' (manual entry)
    - 'national_average' (fallback)

privacy_config:
  dealer_blind_mode: true  -- Scanner looks like normal key fob
  data_never_sold_to_dealers: true
  anonymous_aggregation_opt_in: true
```

---

## 5.4 Asset Delivery Specifications

### Scanner Key Fob Design

**Physical Mockup Requirements**:
- Dimensions: ~2" × 1" × 0.5" (pocket/keychain sized)
- Camera lens position (optimal for document capture)
- Single button (large enough for gloved hands, tactile feedback)
- LED indicators (3 states: scanning/success/error, visible outdoors)
- USB-C port (protected, bottom or side placement)
- Keychain attachment (split ring or carabiner loop)
- Materials: Durable ABS plastic, rubber grip areas
- Finish: Matte (reduces glare, premium feel)
- Logo: Subtle engraving or print

**Packaging Design**:
- Window showing device
- Includes USB-C cable
- Quick-start guide
- "Protect yourself from dealer manipulation" messaging

### Browser Extension UI

**Icon Design**: Toolbar icon (16×16px, 32×32px, 48×48px)
**Popup Interface**: One-click capture confirmation
**Badge**: Shows number of listings captured

### App Icon

- iOS: 1024×1024px
- Android: 512×512px adaptive icon
- Symbol: Scanner + shield (protection) or checkmark (verification)

---

## 5.5 API Integration Points

### OCR Service (Cloud)

**Connection**: Scanner fob captures image → uploads to cloud OCR → returns extracted text

**Design Requirements**:
- Confirmation screen: "Did scanner capture correctly?"
- Error state: "Scan failed—try again in better lighting"

### Browser Extension Web Scraping

**Connection**: Extension scrapes listing page HTML → parses data → sends to app

**Technical Reality**: Sites block scrapers, requires ongoing maintenance

### Cross-Reference Matching

**Connection**: Match scanned VIN to online listing VIN (exact) OR fuzzy match (make/model/year/trim)

### Financing Rate APIs

**Connection**: Credit union APIs (if available) or manual user entry

---

# PART 6: CROSS-DISCIPLINE WORKFLOW

(Follows same sprint structure as Bookmark/LetsEat)

**Ride-Specific Collaboration Points**:

**Design needs from programming**:
- OCR accuracy expectations (80%? 90%? 100%?)
- Browser extension site compatibility (which listing sites work?)
- Scanner battery life with typical use
- Cross-reference matching confidence scores

**Programming needs from design**:
- Scanner fob industrial design (camera angle, button placement, LED visibility)
- Browser extension UI (popup size, capture confirmation)
- Cross-reference alert styling (how prominent? Color coding?)
- Financing calculator interface (savings visualization)

---

## Success Metrics

**Design Quality**:
- ✅ Scanner fob feels professional (car buyers comfortable using at dealers)
- ✅ Cross-reference alerts immediately obvious (price discrepancies highlighted)
- ✅ Financing calculator savings shown in total dollars (not just APR difference)

**Functional Success**:
- ✅ Scanner captures window sticker data with >80% accuracy
- ✅ Browser extension captures listings from major sites
- ✅ Cross-reference matching identifies VIN matches 100%, fuzzy matches 70%+

---

**END OF TECHNICAL IMPLEMENTATION GUIDE**

For creative brief content, see **RideAligned_core.md** (Parts 1-4).
