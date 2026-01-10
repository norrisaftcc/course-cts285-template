# PayComply™ Technical Specification
## Fiscal Compliance Platform - Development Guide

**Project Context:** PayComply™ is a satirical expense tracking platform created as a collaborative design-development learning project. While the product concept is intentionally dystopian parody, your technical implementation should be production-quality.

---

## SYSTEM OVERVIEW

### What You're Building

A full-stack expense tracking application with:
- Real-time transaction processing and approval/denial workflow
- Algorithmic categorization of transactions (Need vs. Want)
- User behavioral tracking and "compliance scoring"
- Multi-platform presence (web app, mobile app, physical card integration)
- Administrative dashboard for monitoring user behavior

### Core Functionality

1. **Transaction Management**
   - Capture transaction attempts via card swipe/app entry
   - Categorize transactions algorithmically
   - Approve or deny based on user budget, history, and "compliance" patterns
   - Generate notifications and required justifications

2. **User Account System**
   - User authentication and profile management
   - Multiple income source tracking
   - Budget configuration and modification
   - Compliance history and scoring

3. **Behavioral Monitoring**
   - Track approval/denial patterns
   - Analyze justification text for "philosophy integration"
   - Generate compliance reports
   - Trigger escalating restrictions based on non-compliant behavior

4. **Reporting & Analytics**
   - User-facing dashboards (spending patterns, compliance scores)
   - Administrative analytics (system-wide denial rates, philosophy adoption)
   - Tax estimation based on multiple income streams

---

## TECHNICAL ARCHITECTURE

### Recommended Stack

**Backend:**
- REST API (Node.js/Express, Python/Flask, or Ruby/Rails)
- Database: PostgreSQL or MongoDB
- Authentication: JWT tokens
- Real-time notifications: WebSockets or Server-Sent Events

**Frontend:**
- Web: React, Vue, or Angular
- Mobile: React Native, Flutter, or native (iOS/Android)
- State management: Redux, Vuex, or Context API
- UI framework: Material UI, Ant Design, or custom component library

**Infrastructure:**
- Cloud hosting: AWS, Google Cloud, or Azure
- CI/CD: GitHub Actions, GitLab CI, or similar
- Monitoring: Application logs, error tracking

### System Architecture Diagram

```
┌─────────────────┐
│  PayComply Card │──┐
│   (Simulated)   │  │
└─────────────────┘  │
                     │
┌─────────────────┐  │    ┌──────────────────┐
│   Mobile App    │──┼────│   API Gateway    │
└─────────────────┘  │    └────────┬─────────┘
                     │             │
┌─────────────────┐  │    ┌────────▼─────────┐
│    Web App      │──┘    │  Application     │
└─────────────────┘       │  Server          │
                          │  (Business Logic)│
                          └────────┬─────────┘
                                   │
                    ┌──────────────┼──────────────┐
                    │              │              │
           ┌────────▼───────┐ ┌───▼────────┐ ┌──▼──────────┐
           │   PostgreSQL   │ │  Redis     │ │  S3/Cloud   │
           │   (User Data)  │ │  (Cache)   │ │  (Assets)   │
           └────────────────┘ └────────────┘ └─────────────┘
```

---

## DATA MODELS

### User

```javascript
{
  id: UUID,
  email: string,
  passwordHash: string,
  name: string,
  enrollmentDate: timestamp,
  phoneNumber: string,
  complianceScore: float (0.0 - 1.0),
  philosophyAdoptionLevel: enum ['resistant', 'adapting', 'accepting', 'integrated'],
  accountStatus: enum ['active', 'restricted', 'probation', 'suspended'],
  cancelRequestDate: timestamp | null,
  createdAt: timestamp,
  updatedAt: timestamp
}
```

### Income Source

```javascript
{
  id: UUID,
  userId: UUID (foreign key),
  sourceName: string,
  sourceType: enum ['employment', 'freelance', 'gig', 'investment', 'other'],
  estimatedMonthlyAmount: decimal,
  frequency: enum ['weekly', 'biweekly', 'monthly', 'quarterly', 'irregular'],
  taxWithheld: boolean,
  isActive: boolean,
  createdAt: timestamp
}
```

### Transaction

```javascript
{
  id: UUID,
  userId: UUID (foreign key),
  amount: decimal,
  merchant: string,
  category: string,
  needWantClassification: enum ['need', 'want', 'uncertain'],
  algorithmicScore: float (0.0 - 1.0),
  approvalStatus: enum ['pending', 'approved', 'denied'],
  decisionTimestamp: timestamp,
  decisionRationale: text,
  attemptedAt: timestamp,
  location: geolocation | null,
  paymentMethod: enum ['card', 'manual_entry'],
  requiresJustification: boolean,
  justificationSubmitted: boolean,
  justificationText: text | null,
  justificationSubmittedAt: timestamp | null,
  createdAt: timestamp
}
```

### Budget

```javascript
{
  id: UUID,
  userId: UUID (foreign key),
  category: string,
  monthlyLimit: decimal,
  currentSpend: decimal,
  lastResetDate: timestamp,
  alertThreshold: float (0.0 - 1.0),
  isActive: boolean,
  createdAt: timestamp,
  updatedAt: timestamp
}
```

### Compliance Event

```javascript
{
  id: UUID,
  userId: UUID (foreign key),
  eventType: enum ['denial', 'justification_required', 'justification_late', 
                   'external_payment_detected', 'philosophy_mention', 
                   'system_defense', 'gratitude_expressed'],
  severity: enum ['minor', 'moderate', 'major'],
  description: text,
  impactOnScore: float,
  timestamp: timestamp
}
```

### Notification

```javascript
{
  id: UUID,
  userId: UUID (foreign key),
  type: enum ['approval', 'denial', 'justification_request', 'compliance_alert', 
              'philosophy_milestone', 'weekly_report'],
  title: string,
  message: text,
  isRead: boolean,
  sentAt: timestamp,
  readAt: timestamp | null
}
```

---

## API ENDPOINTS

### Authentication

```
POST   /api/auth/register
POST   /api/auth/login
POST   /api/auth/logout
POST   /api/auth/refresh-token
GET    /api/auth/verify
```

### Users

```
GET    /api/users/profile
PUT    /api/users/profile
POST   /api/users/cancel-request
GET    /api/users/compliance-score
GET    /api/users/philosophy-level
```

### Transactions

```
POST   /api/transactions/attempt          # Submit transaction for approval
GET    /api/transactions                  # List user transactions
GET    /api/transactions/:id             
PUT    /api/transactions/:id/justification  # Submit justification
GET    /api/transactions/pending         # Pending approvals
GET    /api/transactions/denied          # Denial history
```

### Budgets

```
GET    /api/budgets
POST   /api/budgets
PUT    /api/budgets/:id
DELETE /api/budgets/:id
GET    /api/budgets/summary              # Current month overview
```

### Income Sources

```
GET    /api/income-sources
POST   /api/income-sources
PUT    /api/income-sources/:id
DELETE /api/income-sources/:id
GET    /api/income-sources/tax-estimate  # Quarterly tax calculation
```

### Compliance & Analytics

```
GET    /api/compliance/score-history
GET    /api/compliance/events
GET    /api/compliance/weekly-report
GET    /api/analytics/spending-patterns
GET    /api/analytics/need-vs-want
```

### Notifications

```
GET    /api/notifications
PUT    /api/notifications/:id/read
DELETE /api/notifications/:id
```

---

## ALGORITHMS & BUSINESS LOGIC

### Transaction Approval Algorithm

The "Algorithm" that approves/denies transactions should consider:

```javascript
function evaluateTransaction(transaction, user, budgets) {
  let score = 0.5; // Start neutral
  
  // Factor 1: Budget availability (40% weight)
  const budgetStatus = checkBudgetAvailability(transaction.category, budgets);
  score += budgetStatus.withinBudget ? 0.4 : -0.4;
  
  // Factor 2: Need vs. Want classification (30% weight)
  const classification = classifyNeedVsWant(transaction);
  score += classification === 'need' ? 0.3 : -0.3;
  
  // Factor 3: User compliance history (20% weight)
  score += user.complianceScore * 0.2;
  
  // Factor 4: Recent denial pattern (10% weight)
  const recentDenials = getRecentDenials(user.id, 7); // Last 7 days
  score -= (recentDenials.length / 10) * 0.1;
  
  // Decision threshold
  const approved = score >= 0.6;
  const requiresJustification = score < 0.6 && score >= 0.4;
  
  return {
    approved,
    requiresJustification,
    score,
    rationale: generateRationale(score, classification, budgetStatus)
  };
}
```

### Need vs. Want Classification

Implement a rules-based or machine learning classifier:

```javascript
function classifyNeedVsWant(transaction) {
  // Simple rule-based approach
  const needCategories = [
    'groceries', 'utilities', 'rent', 'healthcare', 
    'transportation', 'insurance'
  ];
  
  const wantKeywords = [
    'entertainment', 'luxury', 'hobby', 'coffee shop',
    'restaurant', 'clothing' // Unless essential
  ];
  
  // Check merchant category
  if (needCategories.includes(transaction.category)) {
    return 'need';
  }
  
  // Check for want indicators
  const merchantLower = transaction.merchant.toLowerCase();
  for (const keyword of wantKeywords) {
    if (merchantLower.includes(keyword)) {
      return 'want';
    }
  }
  
  // Amount-based heuristics
  if (transaction.amount > 100 && !needCategories.includes(transaction.category)) {
    return 'want'; // Large discretionary purchases
  }
  
  return 'uncertain';
}
```

### Compliance Score Calculation

```javascript
function calculateComplianceScore(userId, timeframe = 30) {
  const events = getComplianceEvents(userId, timeframe);
  
  let score = 1.0; // Start at perfect compliance
  
  events.forEach(event => {
    score += event.impactOnScore; // Can be positive or negative
  });
  
  // Recent justifications quality
  const justifications = getRecentJustifications(userId);
  const philosophyMentions = countPhilosophyMentions(justifications);
  score += philosophyMentions * 0.05; // Bonus for philosophy integration
  
  // Clamp between 0 and 1
  return Math.max(0, Math.min(1, score));
}
```

### Philosophy Integration Detection

```javascript
function analyzePhilosophyIntegration(justificationText) {
  const corePhrase = "the algorithm provides everything you need";
  const needVsWantLanguage = ["need", "want", "necessary", "unnecessary"];
  const gratitudeLanguage = ["grateful", "thank", "appreciate", "helps"];
  
  let integrationScore = 0;
  
  // Check for direct phrase usage
  if (justificationText.toLowerCase().includes(corePhrase)) {
    integrationScore += 0.5;
  }
  
  // Check for need/want framing
  const usesNeedWant = needVsWantLanguage.some(word => 
    justificationText.toLowerCase().includes(word)
  );
  if (usesNeedWant) integrationScore += 0.25;
  
  // Check for gratitude language
  const showsGratitude = gratitudeLanguage.some(word =>
    justificationText.toLowerCase().includes(word)
  );
  if (showsGratitude) integrationScore += 0.25;
  
  return {
    score: integrationScore,
    hasPhilosophy: integrationScore >= 0.5,
    sentiment: analyzeTextSentiment(justificationText) // Use sentiment API
  };
}
```

### Tax Estimation

```javascript
function calculateQuarterlyTaxEstimate(userId) {
  const incomeSources = getIncomeSources(userId);
  const currentQuarter = getCurrentQuarter();
  
  let totalIncome = 0;
  let taxWithheld = 0;
  
  incomeSources.forEach(source => {
    const quarterlyIncome = source.estimatedMonthlyAmount * 3;
    totalIncome += quarterlyIncome;
    
    if (source.taxWithheld) {
      taxWithheld += quarterlyIncome * 0.15; // Rough estimate
    }
  });
  
  const estimatedTax = calculateTaxBracket(totalIncome);
  const owedTax = estimatedTax - taxWithheld;
  
  return {
    quarter: currentQuarter,
    totalIncome,
    estimatedTax,
    taxWithheld,
    owedTax,
    dueDate: getQuarterlyDueDate(currentQuarter)
  };
}
```

---

## UI/UX REQUIREMENTS

### What Designers Will Provide

From the design team, you'll receive (see PayComply_Aligned_base.md for their perspective):

1. **Complete Design System**
   - Brand colors, typography, spacing scales
   - Logo files (SVG, PNG in multiple sizes)
   - Icon set for all UI elements
   - Component designs with all states (buttons, forms, cards, etc.)

2. **Screen Designs**
   - High-fidelity mockups for all major screens
   - Mobile and desktop layouts
   - Interactive prototypes (likely in Figma)

3. **Design Specifications**
   - Exact spacing, sizing, and layout measurements
   - Color values (hex, RGB)
   - Font weights and sizes
   - Animation/transition timing

4. **Voice & Tone Guidelines**
   - Copy for notifications, error messages, success states
   - Messaging hierarchy for different alert types
   - Philosophy integration examples

### What You Need to Implement

**Core Screens:**
1. Authentication (login, register, password reset)
2. Dashboard (compliance score, recent transactions, budget status)
3. Transaction list (with filters for approved/denied/pending)
4. Transaction detail (with approval/denial notification)
5. Justification submission form
6. Budget management (create, edit, view progress)
7. Income source management
8. User profile and settings
9. Compliance history and reports
10. Philosophy integration milestones

**Key UI Patterns:**
- Transaction approval/denial notifications (prominent, require acknowledgment)
- Justification form validation (check for philosophy keywords?)
- Real-time budget depletion indicators
- Compliance score visualization
- "Need" vs. "Want" visual differentiation

**Responsive Behavior:**
- Mobile-first approach for transaction entry
- Desktop-optimized for detailed analytics
- Tablet support for hybrid use cases

**Accessibility:**
- WCAG 2.1 AA compliance
- Keyboard navigation
- Screen reader support
- Color contrast requirements

---

## IMPLEMENTATION PRIORITIES

### MVP (Minimum Viable Product)

**Phase 1: Core Transaction System**
1. User authentication
2. Transaction entry (manual, simulated card swipe)
3. Basic approval/denial algorithm
4. Transaction history display
5. Simple budget tracking

**Phase 2: Compliance Features**
6. Justification submission workflow
7. Compliance score calculation
8. Denial notification system
9. Basic analytics dashboard

**Phase 3: Advanced Features**
10. Philosophy integration detection
11. Multiple income source tracking
12. Tax estimation
13. Behavioral escalation (increased restrictions)

### Stretch Goals

- Real payment card integration (via Stripe, Square)
- Machine learning for need/want classification
- Natural language processing for justification analysis
- Progressive Web App (PWA) for offline functionality
- Social features (share denial stories, compare philosophy adoption)
- Admin dashboard for system-wide monitoring

---

## COLLABORATION WITH DESIGN STUDENTS

### What You Need From Designers

**Week 1-2: Initial Requirements**
- Clarification on brand concept and user experience goals
- Initial style direction (colors, typography preferences)
- Screen flow diagrams (which screens needed, navigation structure)

**Week 3-5: Design Deliverables**
- Complete UI component library with specifications
- High-fidelity mockups for all screens
- Icon set and imagery
- Copy for all interface text (buttons, labels, notifications, error messages)

**Week 6-7: Handoff**
- Organized design files (Figma/Sketch with developer access)
- Exported assets (SVG icons, PNG images at multiple resolutions)
- Design system documentation (spacing, colors, typography specs)
- Edge case handling guidance (long text, empty states, errors)

### What Designers Need From You

**Technical Constraints:**
- Data limitations (how many items can a list display efficiently?)
- API response times (should we show loading states? skeleton screens?)
- Authentication requirements (social login available? password requirements?)
- Platform limitations (what mobile OS versions supported?)
- Animation/transition capabilities

**Feature Clarifications:**
- Can the system actually detect philosophy adoption in text? (NLP capabilities)
- How intrusive can notifications be? (push notifications, in-app only?)
- Real-time updates via WebSockets or polling?
- Can we track when users use external payment methods?

**Integration Specifications:**
- Screen dimensions and breakpoints for responsive design
- Component state requirements (loading, error, empty, success)
- Data structure for dynamic content (transaction lists, budget displays)
- Form validation rules

### Communication Protocol

**Regular Check-ins:**
- Weekly sprint planning meetings
- Mid-week async updates via Slack/Discord
- Friday demos of completed work

**When to Ask Questions:**
- Early and often
- Before building something that seems technically impossible
- When design mockups don't account for edge cases
- When you need clarification on user interactions

**How to Give Feedback:**
- "This design is beautiful, but rendering 1000 items will slow performance. Can we paginate?"
- "The gradient background requires custom CSS. Is this a priority or can we simplify?"
- "This animation is great! Should it trigger on every interaction or just the first time?"

*See PayComply_Aligned_base.md for the design team's collaboration perspective.*

---

## TESTING & QUALITY ASSURANCE

### Test Coverage

**Unit Tests:**
- Transaction approval algorithm
- Compliance score calculation
- Need/want classification logic
- Tax estimation calculations

**Integration Tests:**
- API endpoint functionality
- Database queries and updates
- Authentication flow
- Notification delivery

**E2E Tests:**
- User registration and login
- Complete transaction approval/denial flow
- Justification submission workflow
- Budget management CRUD operations

**Edge Cases to Test:**
- Simultaneous transactions (race conditions)
- Very large transaction amounts
- Negative balances
- Empty states (no transactions, no budgets)
- Network failures and recovery
- Concurrent user sessions

### Performance Targets

- API response time: < 200ms for most endpoints
- Page load time: < 2 seconds on 3G connection
- Transaction approval decision: < 500ms
- Support for 1000+ concurrent users
- Database queries optimized with indexes

---

## SECURITY CONSIDERATIONS

**Authentication & Authorization:**
- Secure password hashing (bcrypt, argon2)
- JWT token expiration and refresh
- HTTPS for all communications
- Rate limiting on API endpoints

**Data Protection:**
- Encrypted storage of sensitive data
- PCI compliance if handling real payment data
- Secure transmission of transaction data
- Regular security audits

**Input Validation:**
- Sanitize all user inputs
- Prevent SQL injection, XSS attacks
- Validate data types and ranges
- Handle file uploads securely (if applicable)

---

## DEPLOYMENT & OPERATIONS

**Environment Setup:**
- Development: Local machine, test database
- Staging: Cloud-hosted, mirrors production
- Production: Load-balanced, auto-scaling

**CI/CD Pipeline:**
- Automated testing on every commit
- Staging deployment on merge to main branch
- Production deployment after manual approval
- Rollback procedures for failed deployments

**Monitoring:**
- Application performance monitoring (APM)
- Error tracking and logging
- Database query performance
- User analytics (transaction approval rates, engagement metrics)

**Maintenance:**
- Database backups (daily, weekly, monthly)
- Log rotation and archival
- Dependency updates and security patches
- Performance optimization based on metrics

---

## LEARNING OBJECTIVES

Through building PayComply™, you will demonstrate:

1. **Full-stack development:** Backend APIs, frontend interfaces, database design
2. **Algorithm implementation:** Business logic, scoring systems, classification
3. **User experience:** Real-time interactions, notifications, responsive design
4. **Data modeling:** Complex relationships, efficient queries, data integrity
5. **API design:** RESTful conventions, authentication, error handling
6. **Testing:** Unit, integration, and E2E test coverage
7. **Collaboration:** Working with design students, asset integration, communication
8. **Ethics consideration:** Building a satirical product that critiques real patterns

**Reflection Questions:**

- How do algorithmic scoring systems make decisions feel "objective" even when they're rule-based?
- What are the ethical implications of tracking user behavior and "compliance"?
- How does notification design influence user psychology?
- When does helpful tracking become surveillance?
- What makes a financial app feel trustworthy vs. controlling?

---

## ADDITIONAL RESOURCES

**Recommended Tools:**
- API testing: Postman, Insomnia
- Database GUI: TablePlus, pgAdmin, MongoDB Compass
- Version control: Git, GitHub/GitLab
- Project management: Trello, Jira, Linear
- Code quality: ESLint, Prettier, SonarQube

**Learning Resources:**
- REST API design best practices
- PostgreSQL optimization techniques
- React/Vue state management patterns
- WebSocket implementation guides
- Authentication and security fundamentals

**Similar Projects to Study:**
- Mint (expense tracking)
- YNAB (budgeting philosophy)
- Qapital (automated savings with rules)
- Level Money (simplified expense view)

---

**Thank you for your participation in this collaborative learning project.**

Build thoughtfully. Question thoroughly. Code excellently.
