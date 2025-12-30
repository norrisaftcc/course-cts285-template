# ENGINE BRIEF: Recommendation Engine
## *"You rated this. You might like that."*

---

## What This Engine Does

A **preference-matching system** that handles:

| Capability | Description |
|------------|-------------|
| **Item Catalog** | Store items with rich metadata |
| **Rating System** | Capture user preferences (stars, thumbs, etc.) |
| **Similarity Matching** | Find items/users that are alike |
| **Recommendation Generation** | Suggest new items based on preferences |
| **Explainability** | "Because you liked X" reasoning |

**The insight:** Book recommendations, restaurant suggestions, movie picks, recipe ideas - they're all the same pattern. Rate things → Find patterns → Suggest new things.

---

## Engine Capabilities (What Devs Build)

```
┌─────────────────────────────────────────────┐
│           RECOMMENDATION ENGINE             │
├─────────────────────────────────────────────┤
│  Items              Attributes              │
│  ├─ Title           ├─ Item ID              │
│  ├─ Description     ├─ Key (genre, cuisine) │
│  ├─ Category        └─ Value                │
│  ├─ Image URL                               │
│  └─ Metadata{}                              │
├─────────────────────────────────────────────┤
│  Ratings            Users                   │
│  ├─ User ID         ├─ Preferences{}        │
│  ├─ Item ID         └─ Taste Profile        │
│  ├─ Score                                   │
│  ├─ Timestamp                               │
│  └─ Review (opt)                            │
├─────────────────────────────────────────────┤
│  Recommendations: Similar Items, "For You", │
│  "People Like You Also Liked", Trending     │
└─────────────────────────────────────────────┘
```

---

## Skin Possibilities (Designers Propose)

| Skin Idea | What's Recommended | Target User |
|-----------|-------------------|-------------|
| **NextRead** | Books by genre, author, similar readers | Book lovers |
| **TableFor** | Restaurants by cuisine, vibe, location | Foodies |
| **StreamPick** | Movies/shows by genre, mood, actors | Entertainment seekers |
| **FlavorFind** | Recipes by ingredients, difficulty, cuisine | Home cooks |
| **WheelMatch** | Cars by features, budget, lifestyle | Car shoppers |
| **VinylVault** | Albums by genre, era, similar artists | Music collectors |
| **TrailFinder** | Hiking trails by difficulty, scenery, length | Outdoor enthusiasts |
| **BoardGameBuddy** | Games by player count, complexity, theme | Tabletop gamers |
| **PreferenceOptimizer™** | "Lifestyle choices" with coercive suggestions | 😈 *Satirical* |

**YOUR IDEA HERE:** If it involves rating things and getting personalized suggestions - it probably fits.

---

## What Designers Decide

| Engine Provides | Designer Chooses |
|-----------------|------------------|
| Generic "item" | What items are (books? restaurants? movies?) |
| Rating mechanism | How users rate (5 stars? thumbs? 1-10?) |
| Attribute system | What metadata matters (genre? cuisine? difficulty?) |
| Recommendation UI | How suggestions are presented |
| Discovery flow | Browse vs. search vs. "surprise me" |

---

## Terminology Map Template

| Engine Term | Your Skin Calls It... |
|-------------|----------------------|
| Item | |
| Category | |
| Rating | |
| Attribute | |
| Recommendation | |
| "You might like" | |
| "Because you liked X" | |
| Favorites | |
| Wishlist | |

---

## Database Challenge (For DB Specialist)

**Key problems:**
- Similarity calculations (expensive at scale)
- Sparse matrix storage (most users rate few items)
- Cold start problem (new user with no ratings)
- Efficient "top N recommendations" queries

**Sample query:**
> "Find 10 items highly rated by users whose rating patterns are most similar to User X, excluding items X has already rated"

---

## Algorithm Options (MVP = pick one)

| Approach | How It Works | Complexity |
|----------|--------------|------------|
| **Content-based** | "Items similar to what you liked" | Medium |
| **Collaborative filtering** | "Users like you also liked..." | Higher |
| **Popularity-based** | "Top rated in your categories" | Simple |
| **Hybrid** | Combine approaches | Highest |

**Recommendation:** Start with content-based or popularity, add collaborative as stretch goal.

---

## Stretch Goals (Not MVP)

- [ ] Collaborative filtering algorithm
- [ ] "Not interested" / negative signals
- [ ] Social features (friends' ratings)
- [ ] Import from Goodreads/Letterboxd/etc.
- [ ] Machine learning recommendations

---

## For This Skin, I Want to Build...

**Skin name:** _______________________

**Target user:** _______________________

**What they're discovering:** _______________________

**How they rate things:** _______________________

---

*"The Algorithm knows your preferences. The Algorithm suggests improvements. Resistance degrades your recommendation quality."* 🤖

