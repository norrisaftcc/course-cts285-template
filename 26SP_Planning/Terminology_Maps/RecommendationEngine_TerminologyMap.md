# Recommendation Engine Terminology Configuration

## White-Label Architecture - Spring 2026

**Status:** ACTIVE - GRD Creative Briefs Received (Issue #7 Partially Resolved)

---

## Overview

The Recommendation Engine provides personalized suggestions based on user preferences, behavior patterns, and contextual data. Three white-label skins are now defined:

| Skin | Target Market | Voice | Status |
|------|--------------|-------|--------|
| **Bookmark** | Book readers | Sophisticated, literary | GRD Brief Complete |
| **Let'sEat!** | Decision-fatigued diners | Enthusiastic, friendly | GRD Brief Complete |
| **PreferenceOptimizer** | AlgoCratic satire | Corporate dystopia | In Development |

---

## Core Entity Terminology

### Items (What's Being Recommended)

| Generic Term | Bookmark | Let'sEat! | PreferenceOptimizer |
|-------------|----------|-----------|---------------------|
| Item | Book | Restaurant | Approved Resource |
| Item Collection | Library / Shelf | Dining History | Skill Repository |
| Item Details | Book Profile | Restaurant Profile | Resource Dossier |
| Featured Items | Staff Picks | Popular Spots | Algorithm-Approved Content |

### User Preferences

| Generic Term | Bookmark | Let'sEat! | PreferenceOptimizer |
|-------------|----------|-----------|---------------------|
| Rating | Reading Experience | Dining Experience | Compliance Assessment |
| Positive Rating | Loved It | Would Eat Again | Skill Acquired |
| Negative Rating | Not For Me | Skip It | Remediation Required |
| Neutral Rating | Mixed Feelings | It Was Fine | Partial Compliance |
| Rating Scale | Feeling-First (1-5 hearts) | Satisfaction (thumbs/stars) | Alignment Index (0-100%) |

### Wishlists & Queues

| Generic Term | Bookmark | Let'sEat! | PreferenceOptimizer |
|-------------|----------|-----------|---------------------|
| Wishlist | TBR List (To Be Read) | Want to Try | Mandatory Learning Queue |
| Favorites | Loved Books | Go-To Spots | Mastered Skills |
| Currently Active | Currently Reading | - | In Progress Modules |
| Completed | Finished | Tried | Compliance Achieved |

### Recommendations

| Generic Term | Bookmark | Let'sEat! | PreferenceOptimizer |
|-------------|----------|-----------|---------------------|
| Recommendation | Your Next Read | What Should I Eat? | Skill Directive |
| "You might like" | "You might love" | "Try this place" | "The Algorithm recommends" |
| "Because you liked X" | "Because you loved X" | "Based on your dining patterns" | "Due to competency gaps in..." |
| Discovery Mode | Break the Bubble | Try Something New | Mandatory Skill Expansion |
| Trending | Popular This Month | Hot Right Now | Organization Priority Skills |

### Attributes & Metadata

| Generic Term | Bookmark | Let'sEat! | PreferenceOptimizer |
|-------------|----------|-----------|---------------------|
| Category | Genre | Cuisine Type | Skill Domain |
| Subcategory | Subgenre | Cuisine Style | Competency Area |
| Mood/Feeling | Reading Mood | Dining Mood | Learning Context |
| Difficulty | - | Price Range | Complexity Level |
| Duration | Page Count | Time Available | Estimated Learning Hours |
| Source | Who Recommended | How You Found It | Assignment Source |

### Sources & Attribution

| Generic Term | Bookmark | Let'sEat! | PreferenceOptimizer |
|-------------|----------|-----------|---------------------|
| Source | Recommendation Source | Discovery Source | Directive Origin |
| Source Types | Friend, Podcast, Book Club, Instagram | Friend, Instagram, Drove Past | Manager, Team Lead, Algorithm |
| Source Hit Rate | Taste Alignment | Recommendation Success | Directive Compliance Rate |
| Trusted Sources | Your Reading Guides | Your Food Friends | Approved Authorities |

---

## Feature-Specific Terminology

### Bookmark-Specific Terms

| Feature | Term | Description |
|---------|------|-------------|
| Physical Product | Reading Journal | Hardcover 6"x8" journal with reading sections |
| Journal Sync | Photo Capture | OCR sync from handwritten journal to app |
| Memory Feature | Reading Memory | Remember why you wanted to read / how it felt |
| Filter Bubble Escape | Discovery Mode | Intentional genre expansion |
| Source Tracking | Hit Rate Analysis | Which recommenders match your taste |

### Let'sEat!-Specific Terms

| Feature | Term | Description |
|---------|------|-------------|
| Physical Product | Dining Passport | Pocket 4"x6" booklet with stamps |
| Quick Decision | "What Should I Eat?" | One-button decision flow |
| Pattern Recognition | Dining Patterns | "Friday = date night," "Tired = comfort food" |
| Location Feature | Near Me Now | Geofenced suggestions |
| Occasion Tagging | Dining Occasion | Quick lunch, Date night, Family dinner, Solo treat |

### PreferenceOptimizer-Specific Terms

| Feature | Term | Description |
|---------|------|-------------|
| Physical Product | Learning Compliance Card | Satirical skill tracking card |
| Skill Assessment | Competency Gap Analysis | What skills you need for a task |
| Learning Paths | Approved Learning Pathways | Curated resource recommendations |
| Progress Metric | Skill Alignment Score | Gamified progress (0-100%) |
| Directive | Skill Directive | Algorithmic learning recommendation |

---

## Voice & Tone Guidelines

### Bookmark Voice
- **Tone:** Sophisticated, warm, literary
- **Personality:** Thoughtful companion who respects your reading life
- **Avoid:** Casual slang, corporate speak, algorithm emphasis
- **Example:** "You loved books that made you think about time differently. This novel explores similar themes through the lens of memory."

### Let'sEat! Voice
- **Tone:** Enthusiastic, friendly, decisive
- **Personality:** Confident friend who always has an answer
- **Avoid:** Pretentiousness, indecision language, overwhelming options
- **Example:** "You loved that Thai place last Tuesday! Based on your craving for bold flavors, try this Vietnamese spot - 0.3 miles away."

### PreferenceOptimizer Voice
- **Tone:** Corporate dystopia, faux-helpful surveillance
- **Personality:** Algorithmic authority with "voluntary" compliance requirements
- **Avoid:** Actually being threatening, losing the satirical wink
- **Example:** "Your Skill Compliance Report indicates a 23% deficiency in database concepts. The Algorithm recommends immediate remediation via these resources (compliance is voluntary but monitored)."

---

## Configuration Color Palettes

### Bookmark Colors
```yaml
primary: "#8B7355"        # Warm Taupe (leather-bound books)
secondary: "#D4A574"      # Golden Ochre (aged paper)
accent: "#C4A77D"         # Antique Gold (gilded edges)
background: "#FAF8F5"     # Cream (book pages)
text_primary: "#3D3D3D"   # Charcoal (readable ink)
```

### Let'sEat! Colors
```yaml
primary: "#FF6B35"        # Appetizing Orange (energetic, hungry)
secondary: "#F7C59F"      # Warm Peach (friendly, inviting)
accent: "#2EC4B6"         # Fresh Teal (cleansing, confident)
background: "#FFFCF9"     # Warm White (clean plate)
text_primary: "#2D3436"   # Soft Black (readable menus)
```

### PreferenceOptimizer Colors
```yaml
primary: "#1E3A5F"        # Corporate Navy (institutional authority)
secondary: "#4A90A4"      # Compliance Teal (monitoring calm)
accent: "#E8B800"         # Warning Gold (attention required)
background: "#F5F7FA"     # Clinical Gray (sterile efficiency)
text_primary: "#2C3E50"   # Authority Gray (official communications)
```

---

## API Terminology Mapping

### Endpoint Naming

| Generic Endpoint | Bookmark | Let'sEat! | PreferenceOptimizer |
|-----------------|----------|-----------|---------------------|
| `GET /items` | `GET /books` | `GET /restaurants` | `GET /resources` |
| `POST /ratings` | `POST /reading-experience` | `POST /dining-experience` | `POST /skill-assessment` |
| `GET /recommendations` | `GET /next-reads` | `GET /suggestions` | `GET /skill-directives` |
| `GET /wishlist` | `GET /tbr-list` | `GET /want-to-try` | `GET /learning-queue` |
| `GET /history` | `GET /reading-history` | `GET /dining-history` | `GET /compliance-log` |

---

## Physical Product Terminology

| Component | Bookmark | Let'sEat! | PreferenceOptimizer |
|-----------|----------|-----------|---------------------|
| Format | Hardcover Journal 6"x8" | Pocket Passport 4"x6" | Compliance Card (credit card size) |
| Sections | Want to Read / Currently Reading / Completed | Tried & Loved / Want to Try / City Pages | Skills Acquired / In Progress / Mandated |
| Tracking Mechanism | Ribbon Bookmark | Stamps/Stickers | QR Code Scans |
| Achievement | Reading Memory Archive | Dining Explorer Stamps | Skill Clearance Badges |

---

## Database Entity Summary

### Core Tables (All Skins)

```
users                    # User profiles with preferences
items                    # Books / Restaurants / Resources
ratings                  # User ratings with context
attributes               # Item metadata (genre/cuisine/skill)
recommendations          # Generated suggestions
wishlists                # TBR / Want-to-Try / Learning Queue
sources                  # Where recommendations came from
```

### Skin-Specific Extensions

**Bookmark:** `reading_sessions`, `journal_entries`, `source_hit_rates`, `reading_goals`

**Let'sEat!:** `dining_patterns`, `occasions`, `location_history`, `passport_stamps`

**PreferenceOptimizer:** `skill_assessments`, `competency_gaps`, `learning_paths`, `compliance_scores`

---

## Cross-Reference: Engine Capabilities to Skin Features

| Engine Capability | Bookmark Feature | Let'sEat! Feature | PreferenceOptimizer Feature |
|-------------------|-----------------|-------------------|------------------------------|
| Item Catalog | Book Library | Restaurant Database | Resource Repository |
| Rating System | Reading Experience (feeling-first) | Dining Experience (satisfaction) | Skill Assessment (compliance) |
| Similarity Matching | "Readers who loved this" | "Based on your patterns" | "Citizens with similar gaps" |
| Recommendation Generation | Your Next Read | What Should I Eat? | Skill Directives |
| Explainability | "Because you loved X" | "You usually order Y on Z days" | "Due to competency deficit in..." |
| Discovery Mode | Break the Bubble | Try Something New | Mandatory Skill Expansion |
| Source Tracking | Recommendation Hit Rate | Discovery Source Success | Directive Authority Rating |

---

## Document Version

**Version:** 1.0
**Updated:** 2026-01-02
**Status:** Active - GRD Briefs Received
**Spring 2026 Great Alignment**

**Related Issues:**
- Issue #7: Rec Engine now unblocked (Data Tracking still blocked)
- Issue #10: Recommendation GRD Aligned Briefs

---

*"The Algorithm knows what you want. The Algorithm knows what you need. The Algorithm knows the difference."*
