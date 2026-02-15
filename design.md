# Design Document - Crop Residue Utilization Analyzer

## 1. System Architecture

### 1.1 Architecture Overview
```
┌─────────────────────────────────────────────────────────────┐
│                     User Interface Layer                     │
│  ┌──────────────────────┐  ┌──────────────────────────┐    │
│  │   Web Interface      │  │   Python CLI             │    │
│  │   (HTML/CSS/JS)      │  │   (Command Line)         │    │
│  └──────────────────────┘  └──────────────────────────┘    │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                    Business Logic Layer                      │
│  ┌──────────────────────────────────────────────────────┐  │
│  │  Analysis Engine                                      │  │
│  │  - Input Validation                                   │  │
│  │  - Method Evaluation                                  │  │
│  │  - Feasibility Scoring                                │  │
│  │  - Financial Calculation                              │  │
│  │  - Carbon Impact Analysis                             │  │
│  └──────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                       Data Layer                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │
│  │  Subsidies   │  │  Contacts    │  │  Methods     │     │
│  │  Database    │  │  Database    │  │  Database    │     │
│  └──────────────┘  └──────────────┘  └──────────────┘     │
└─────────────────────────────────────────────────────────────┘
```

### 1.2 Component Architecture
- **Frontend**: Pure HTML5, CSS3, JavaScript (ES6+)
- **Backend**: Python 3.6+ (optional, for CLI)
- **Data Storage**: JSON objects (in-memory)
- **Charts**: Custom CSS-based visualizations
- **No External Dependencies**: Self-contained system

---

## 2. User Interface Design

### 2.1 Design Principles
1. **Simplicity First**: Minimal cognitive load
2. **Visual Hierarchy**: Important info stands out
3. **Progressive Disclosure**: Show details on demand
4. **Farmer-Friendly**: Simple language, clear icons
5. **Mobile-First**: Responsive from smallest screen up

### 2.2 Color Palette


```css
/* Primary Colors */
--primary-gradient: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
--primary-purple: #667eea;
--primary-dark: #764ba2;

/* Semantic Colors */
--success-green: #48bb78;
--success-light: #c6f6d5;
--warning-orange: #f59e0b;
--warning-light: #feebc8;
--danger-red: #f56565;
--info-blue: #0284c7;
--info-light: #bee3f8;

/* Neutral Colors */
--text-primary: #2d3748;
--text-secondary: #718096;
--background-white: #ffffff;
--background-light: #f7fafc;
--border-gray: #e2e8f0;
```

### 2.3 Typography
```css
/* Font Family */
font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;

/* Font Sizes */
--font-xl: 28px;    /* Main heading */
--font-lg: 22px;    /* Section headings */
--font-md: 18px;    /* Subsection headings */
--font-base: 14px;  /* Body text */
--font-sm: 12px;    /* Labels, badges */

/* Font Weights */
--weight-normal: 400;
--weight-semibold: 600;
--weight-bold: 700;
```

### 2.4 Layout Structure
```
┌─────────────────────────────────────────────────────────┐
│                      Header                              │
│  🌾 Crop Residue Analyzer                               │
│  Smart solution for sustainable farming                 │
├─────────────────────────────────────────────────────────┤
│                                                          │
│  ┌────────────────────────────────────────────────┐    │
│  │           Input Form Section                    │    │
│  │  - Crop Type                                    │    │
│  │  - Land Size & Residue Quantity                │    │
│  │  - Location                                     │    │
│  │  - Budget & Resources                           │    │
│  │  [Analyze Button]                               │    │
│  └────────────────────────────────────────────────┘    │
│                                                          │
│  ┌────────────────────────────────────────────────┐    │
│  │           Results Section                       │    │
│  │  A. Best Recommendation Card                    │    │
│  │  B. Feasibility Chart                           │    │
│  │  C. Financial Chart                             │    │
│  │  D. Environmental Impact                        │    │
│  │  E. Government Subsidies                        │    │
│  │  F. Contact Information                         │    │
│  │  G. Action Plan                                 │    │
│  │  H. Important Tips                              │    │
│  └────────────────────────────────────────────────┘    │
│                                                          │
└─────────────────────────────────────────────────────────┘
```

---

## 3. Data Model Design

### 3.1 Input Data Structure
```javascript
{
  cropType: String,           // "Rice", "Wheat", etc.
  landSize: Number,           // In acres
  residueQty: Number,         // In tons
  location: String,           // "City, State"
  distance: Number,           // To nearest plant (km)
  budget: Number,             // In INR
  labor: String,              // "Low", "Medium", "High"
  transport: String,          // "Poor", "Good", "Excellent"
  machinery: Array<String>    // Optional: ["tractor", "rotavator"]
}
```

### 3.2 Method Evaluation Structure
```javascript
{
  method: String,             // "Mulching/Incorporation"
  feasibility: Number,        // 0-100
  setupCost: Number,          // In INR
  revenue: Number,            // In INR
  payback: Number,            // In months
  effort: String,             // "Low", "Medium", "High"
  risks: String               // Description of risks
}
```

### 3.3 Subsidy Data Structure
```javascript
{
  name: String,               // Scheme name
  type: String,               // "Central" or "State"
  subsidy: String,            // "50% (up to ₹1 lakh)"
  applicableFor: String,      // Equipment/methods
  eligibility: String,        // Who can apply
  howToApply: String,         // Application process
  documents: String,          // Required documents
  website: String,            // Official URL
  contact: String             // Phone/email
}
```

### 3.4 Contact Data Structure
```javascript
{
  name: String,               // Organization name
  phone: String,              // Contact number
  email: String,              // Email address (optional)
  address: String,            // Physical address (optional)
  timings: String,            // Office hours (optional)
  services: String            // Services offered (optional)
}
```

---

## 4. Algorithm Design

### 4.1 Feasibility Scoring Algorithm
```python
def calculate_feasibility(method, farmer_data):
    base_score = METHOD_BASE_SCORES[method]
    
    # Budget adjustment
    if farmer_data.budget < method.min_budget:
        base_score -= 30
    elif farmer_data.budget > method.optimal_budget:
        base_score += 10
    
    # Distance adjustment
    if method.requires_plant_access:
        if farmer_data.distance > 50:
            base_score -= 25
        elif farmer_data.distance < 10:
            base_score += 15
    
    # Labor adjustment
    if method.labor_intensive and farmer_data.labor == "Low":
        base_score -= 20
    
    # Transport adjustment
    if method.requires_transport:
        if farmer_data.transport == "Poor":
            base_score -= 20
        elif farmer_data.transport == "Excellent":
            base_score += 10
    
    # Machinery adjustment
    if method.required_machinery in farmer_data.machinery:
        base_score += 15
    
    return max(0, min(100, base_score))
```

### 4.2 Financial Calculation Algorithm
```python
def calculate_financials(method, farmer_data):
    # Setup cost calculation
    setup_cost = method.base_cost
    setup_cost += farmer_data.residue_qty * method.cost_per_ton
    
    if farmer_data.distance > 25:
        setup_cost += (farmer_data.distance - 25) * method.transport_cost_per_km
    
    # Revenue calculation
    if method.type == "sale":
        revenue = farmer_data.residue_qty * method.market_price_per_ton
    elif method.type == "savings":
        revenue = farmer_data.land_size * method.savings_per_acre
    elif method.type == "production":
        revenue = farmer_data.residue_qty * method.output_value_per_ton
    
    # Payback calculation
    net_benefit = revenue - setup_cost
    if net_benefit > 0:
        payback_months = (setup_cost / revenue) * 12
    else:
        payback_months = float('inf')
    
    return {
        'setup_cost': setup_cost,
        'revenue': revenue,
        'payback_months': payback_months
    }
```

### 4.3 Carbon Impact Calculation
```python
def calculate_carbon_impact(residue_qty):
    # Constants (kg CO2 per ton of residue)
    BURNING_EMISSION = 1500
    CONVERSION_SAVING = 1200
    CO2_PER_TREE_YEAR = 20
    
    burning_emission = residue_qty * BURNING_EMISSION
    conversion_saving = residue_qty * CONVERSION_SAVING
    net_reduction = conversion_saving
    trees_equivalent = int(net_reduction / CO2_PER_TREE_YEAR)
    
    return {
        'burning_emission_kg': burning_emission,
        'conversion_saving_kg': conversion_saving,
        'net_reduction_kg': net_reduction,
        'trees_equivalent': trees_equivalent
    }
```

### 4.4 Location-Based Subsidy Matching
```python
def match_subsidies(location):
    subsidies = []
    
    # Add central schemes (always)
    subsidies.extend(CENTRAL_SCHEMES)
    
    # Detect state from location
    state = extract_state(location)
    
    # Add state-specific schemes
    if state in STATE_SCHEMES:
        subsidies.extend(STATE_SCHEMES[state])
    
    return subsidies

def extract_state(location):
    # Parse location string
    parts = location.split(',')
    if len(parts) >= 2:
        state = parts[-1].strip()
        return state
    return None
```

---

## 5. Chart Design

### 5.1 Feasibility Bar Chart
```html
<div class="bar-chart">
  <div class="bar-item">
    <div class="bar-label">Method Name</div>
    <div class="bar-wrapper">
      <div class="bar-fill" style="width: 85%">85%</div>
    </div>
  </div>
</div>
```

**Design Specifications:**
- Bar height: 30px
- Label width: 150px
- Bar color: Purple gradient
- Animation: 1s ease transition
- Max width: 100% = 100% feasibility

### 5.2 Financial Bar Chart
```html
<div class="bar-chart">
  <div class="bar-item">
    <div class="bar-label">Method Name</div>
    <div class="bar-wrapper">
      <div class="bar-fill" style="width: 75%">₹45K</div>
    </div>
  </div>
</div>
```

**Design Specifications:**
- Scaled to highest value
- Display in thousands (K)
- Same styling as feasibility chart
- Sortable by revenue

### 5.3 Environmental Pie Chart
```css
.pie-chart {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  background: conic-gradient(
    #48bb78 0deg 180deg,    /* CO2 saved */
    #f56565 180deg 360deg   /* CO2 burned */
  );
}
```

**Design Specifications:**
- Diameter: 200px
- Green: CO2 saved (50%)
- Red: CO2 if burned (50%)
- Legend below chart
- Tree icon with equivalent

---

## 6. Responsive Design

### 6.1 Breakpoints
```css
/* Mobile First */
@media (min-width: 768px) {
  /* Tablet */
  .row { grid-template-columns: 1fr 1fr; }
  .container { max-width: 800px; }
}

@media (min-width: 1024px) {
  /* Desktop */
  .container { max-width: 1000px; }
  .contact-grid { grid-template-columns: repeat(2, 1fr); }
}
```

### 6.2 Mobile Optimizations
- Single column layout
- Larger touch targets (44x44px)
- Simplified navigation
- Collapsible sections
- Optimized images
- Reduced animations

### 6.3 Tablet Optimizations
- Two-column grid for form
- Side-by-side charts
- Expanded contact cards
- Full-width action plan

### 6.4 Desktop Optimizations
- Maximum width: 1000px
- Multi-column layouts
- Hover effects
- Expanded visualizations
- Print-optimized layout

---

## 7. Interaction Design

### 7.1 Form Interactions


**Input Validation:**
- Real-time validation on blur
- Error messages below fields
- Red border for invalid inputs
- Green checkmark for valid inputs

**Submit Button:**
- Disabled until form valid
- Loading state during analysis
- Success animation on completion

**Auto-save:**
- Save form data to localStorage
- Restore on page reload
- Clear on successful submission

### 7.2 Results Interactions

**Smooth Scrolling:**
- Auto-scroll to results on analysis
- Smooth animation (500ms)
- Highlight new content

**Chart Animations:**
- Bars fill from left to right
- 1 second duration
- Ease-out timing function
- Stagger effect (100ms delay between bars)

**Expandable Sections:**
- Click to expand/collapse
- Smooth height transition
- Arrow icon rotation
- Remember state in localStorage

### 7.3 Print Interactions

**Print Button:**
- Opens browser print dialog
- Hides form and buttons
- Optimizes layout for paper
- Preserves charts and colors

**PDF Download:**
- Triggers browser print
- User saves as PDF
- Maintains formatting
- Includes all content

---

## 8. State Management

### 8.1 Application States
```javascript
const AppState = {
  INITIAL: 'initial',           // Form visible, no results
  ANALYZING: 'analyzing',       // Processing input
  RESULTS: 'results',           // Showing analysis
  ERROR: 'error'                // Error occurred
}
```

### 8.2 State Transitions
```
INITIAL → [Submit Form] → ANALYZING
ANALYZING → [Analysis Complete] → RESULTS
ANALYZING → [Error] → ERROR
RESULTS → [New Analysis] → ANALYZING
ERROR → [Retry] → INITIAL
```

### 8.3 Data Persistence
```javascript
// Save form data
localStorage.setItem('formData', JSON.stringify(formData));

// Restore form data
const savedData = JSON.parse(localStorage.getItem('formData'));

// Clear on submit
localStorage.removeItem('formData');
```

---

## 9. Error Handling Design

### 9.1 Input Validation Errors
```javascript
const ValidationErrors = {
  REQUIRED: 'This field is required',
  MIN_VALUE: 'Value must be at least {min}',
  MAX_VALUE: 'Value cannot exceed {max}',
  INVAr performance
- Easier maintenance

### 20.4 Why Mobile-First?
**Decision:** Design for mobile, enhance for desktop

**Rationale:**
- Most farmers use smartphones
- Better progressive enhancement
- Forced simplicity
- Better performance on low-end devices
- Future-proof design

---

**Document Version:** 1.0  
**Last Updated:** February 14, 2026  
**Status:** Approved  
**Next Review:** May 14, 2026
)
- Better offline support
- Simpler deployment
- Lower learning curve

### 20.2 Why Client-Side Only?
**Decision:** No backend server

**Rationale:**
- Lower hosting costs (free static hosting)
- Better privacy (no data sent to server)
- Faster response (no network latency)
- Easier scaling (CDN handles traffic)
- Offline capability

### 20.3 Why Custom Charts?
**Decision:** CSS-based charts instead of library

**Rationale:**
- Smaller file size
- No external dependencies
- Full customization control
- BetteteMethod(type, data) {
    switch(type) {
      case 'Mulching':
        return new MulchingMethod(data);
      case 'Biogas':
        return new BiogasMethod(data);
      case 'Composting':
        return new CompostingMethod(data);
      default:
        throw new Error('Unknown method type');
    }
  }
}
```

---

## 20. Design Decisions and Rationale

### 20.1 Why No Framework?
**Decision:** Pure HTML/CSS/JavaScript

**Rationale:**
- Faster loading (no framework overhead)
- Easier maintenance (no dependenciesventEmitter {
  constructor() {
    this.events = {};
  }
  
  on(event, callback) {
    if (!this.events[event]) {
      this.events[event] = [];
    }
    this.events[event].push(callback);
  }
  
  emit(event, data) {
    if (this.events[event]) {
      this.events[event].forEach(cb => cb(data));
    }
  }
}

// Usage
const analyzer = new EventEmitter();
analyzer.on('analysisComplete', (results) => {
  displayResults(results);
});
```

### 19.3 Factory Pattern
```javascript
class MethodFactory {
  static creather integration

Computer Vision:
- Residue quantity estimation
- Crop type identification
- Equipment recognition
- Quality assessment
```

---

## 19. Design Patterns Used

### 19.1 Module Pattern
```javascript
const AnalysisEngine = (function() {
  // Private variables
  const methods = [...];
  
  // Private functions
  function calculateScore() { }
  
  // Public API
  return {
    analyze: function(data) { },
    getMethods: function() { }
  };
})();
```

### 19.2 Observer Pattern
```javascript
class Eress tracking                │
└─────────────────────────────────────┘
```

### 18.2 Phase 3: Mobile App
```
Technology Stack:
- React Native (cross-platform)
- Offline-first architecture
- Push notifications
- Camera integration
- GPS location

Features:
- All web features
- Offline mode
- Document scanning
- Voice input
- SMS sharing
```

### 18.3 Phase 4: AI Enhancements
```
Machine Learning Features:
- Predictive analytics
- Personalized recommendations
- Market price forecasting
- Crop yield estimation
- Wea 18.1 Phase 2: User Accounts
```
┌─────────────────────────────────────┐
│         Authentication              │
│  - Email/phone login                │
│  - OTP verification                 │
│  - Social login (optional)          │
└─────────────────────────────────────┘
              │
              ▼
┌─────────────────────────────────────┐
│         User Dashboard              │
│  - Analysis history                 │
│  - Saved recommendations            │
│  - Subsidy applications             │
│  - Prog What is this tool?
   - How to use it?
   - Sample walkthrough

2. User Manual (10 pages)
   - Detailed instructions
   - Understanding results
   - Subsidy information
   - Contact resources

3. FAQ (20 questions)
   - Common questions
   - Troubleshooting
   - Technical support

4. Video Tutorials (5 videos)
   - Introduction (2 min)
   - Form filling (3 min)
   - Understanding results (4 min)
   - Applying for subsidies (5 min)
   - Success stories (3 min)
```

---

## 18. Future Enhancements Design

###lable budget in INR
 * @param {number} farmerData.distance - Distance to plant in km
 * @param {string} farmerData.labor - Labor availability (Low/Medium/High)
 * @returns {number} Feasibility score (0-100)
 * 
 * @example
 * const score = calculateFeasibility('Mulching', {
 *   budget: 50000,
 *   distance: 25,
 *   labor: 'Medium'
 * });
 * // Returns: 85
 */
function calculateFeasibility(method, farmerData) {
  // Implementation
}
```

### 17.2 User Documentation Structure
```
1. Quick Start Guide (2 pages)
   -

### 16.3 Rollback Strategy
```bash
# Tag current version
git tag v2.0.0

# If issues found, rollback
git revert HEAD
netlify deploy --prod

# Or restore previous version
git checkout v1.9.0
netlify deploy --prod
```

---

## 17. Documentation Design

### 17.1 Code Documentation
```javascript
/**
 * Calculate feasibility score for a residue management method
 * 
 * @param {string} method - Method name (e.g., "Mulching")
 * @param {Object} farmerData - Farmer's input data
 * @param {number} farmerData.budget - Avai  - Verify contact information
   - Test all links

2. Monthly Content Review
   - Update market prices
   - Review action plans
   - Check for broken links
   - Update FAQs

3. Weekly Monitoring
   - Check error logs
   - Review user feedback
   - Monitor performance
   - Test critical paths
```

### 16.2 Version Control
```
Version Format: MAJOR.MINOR.PATCH

MAJOR: Breaking changes (e.g., 1.0 → 2.0)
MINOR: New features (e.g., 1.0 → 1.1)
PATCH: Bug fixes (e.g., 1.0.0 → 1.0.1)

Current: 2.0.0 (Enhanced Edition)
``` popularMethods: {},
  averageSessionTime: 0,
  errorRate: 0
};

// No personal data collected
// No IP addresses stored
// No cookies used
```

### 15.3 Error Tracking
```javascript
window.addEventListener('error', (event) => {
  console.error('Error:', event.error);
  // Log to error tracking service (optional)
  // Display user-friendly error message
});
```

---

## 16. Maintenance Design

### 16.1 Update Process
```
1. Quarterly Subsidy Review
   - Check government websites
   - Update subsidy amounts
 
window.addEventListener('load', () => {
  const loadTime = performance.timing.loadEventEnd - 
                   performance.timing.navigationStart;
  console.log('Page load time:', loadTime, 'ms');
});

// Measure analysis time
const startTime = performance.now();
analyzeData(formData);
const endTime = performance.now();
console.log('Analysis time:', endTime - startTime, 'ms');
```

### 15.2 Usage Analytics (Privacy-Friendly)
```javascript
// Track anonymized usage
const analytics = {
  analysisCount: 0,
           │
│  - CI/CD integration                │
└─────────────────────────────────────┘
```

### 14.2 Deployment Process
```bash
# 1. Build (if needed)
npm run build

# 2. Test
npm test

# 3. Deploy to staging
netlify deploy --dir=dist

# 4. Test staging
npm run test:e2e

# 5. Deploy to production
netlify deploy --prod --dir=dist

# 6. Verify production
curl https://crop-analyzer.netlify.app
```

---

## 15. Monitoring and Analytics

### 15.1 Performance Monitoring
```javascript
// Measure page load time                  │
└─────────────────────────────────────┘
              │
              ▼
┌─────────────────────────────────────┐
│    Static Hosting (Netlify)         │
│  - Automatic deployments            │
│  - Branch previews                  │
│  - Form handling                    │
└─────────────────────────────────────┘
              │
              ▼
┌─────────────────────────────────────┐
│    Git Repository (GitHub)          │
│  - Version control                  │
│  - Collaboration          ring
- Subsidy matching
- Contact information display
- Print functionality

### 13.3 User Acceptance Testing
- Farmer testing (5+ users)
- Extension worker testing (3+ users)
- Time-to-complete measurement
- Error recovery testing
- Satisfaction survey

---

## 14. Deployment Architecture

### 14.1 Static Hosting (Recommended)
```
┌─────────────────────────────────────┐
│         CDN (CloudFlare)            │
│  - Global edge locations            │
│  - SSL/TLS encryption               │
│  - DDoS protectioning
- Clear privacy policy

---

## 13. Testing Strategy

### 13.1 Unit Testing
```javascript
// Test feasibility calculation
describe('calculateFeasibility', () => {
  it('should return 95 for optimal mulching conditions', () => {
    const result = calculateFeasibility('Mulching', {
      budget: 50000,
      distance: 10,
      labor: 'High',
      transport: 'Good',
      machinery: ['rotavator']
    });
    expect(result).toBe(95);
  });
});
```

### 13.2 Integration Testing
- Form submission flow
- Chart rende // Escape special characters
  input = input.replace(/[&<>"']/g, (char) => {
    const escapeMap = {
      '&': '&amp;',
      '<': '&lt;',
      '>': '&gt;',
      '"': '&quot;',
      "'": '&#x27;'
    };
    return escapeMap[char];
  });
  
  return input.trim();
}
```

### 12.2 XSS Prevention
- Escape all user inputs
- Use textContent instead of innerHTML
- Validate data types
- Whitelist allowed values

### 12.3 Data Privacy
- No personal data collection
- No cookies (current version)
- No external trackton>

<div role="alert" aria-live="polite">
  Analysis complete
</div>

<img src="chart.png" alt="Feasibility comparison showing mulching at 95%, biomass at 80%, and composting at 70%">
```

### 11.4 Color Contrast
- Text: 4.5:1 minimum (WCAG AA)
- Large text: 3:1 minimum
- Interactive elements: 3:1 minimum
- Test with color blindness simulators

---

## 12. Security Design

### 12.1 Input Sanitization
```javascript
function sanitizeInput(input) {
  // Remove HTML tags
  input = input.replace(/<[^>]*>/g, '');
  
 us indicators visible
- Skip to content link
- Keyboard shortcuts for common actions
- Escape to close modals

### 11.3 Screen Reader Support
```html
<button aria-label="Analyze crop residue data">
  Analyze
</but where appropriate

---

## 11. Accessibility Design

### 11.1 Semantic HTML
```html
<main role="main">
  <section aria-labelledby="form-heading">
    <h1 id="form-heading">Input Form</h1>
    <form aria-label="Crop residue analysis form">
      <label for="crop-type">Crop Type</label>
      <select id="crop-type" required aria-required="true">
        <option value="">Select crop</option>
      </select>
    </form>
  </section>
</main>
```

### 11.2 Keyboard Navigation
- Tab order follows visual flow
- Foctions

### 10.2 Rendering Optimization
```javascript
// Batch DOM updates
const fragment = document.createDocumentFragment();
items.forEach(item => {
  const element = createItemElement(item);
  fragment.appendChild(element);
});
container.appendChild(fragment);

// Use requestAnimationFrame for animations
requestAnimationFrame(() => {
  element.style.width = '100%';
});
```

### 10.3 Memory Optimization
- Remove event listeners on cleanup
- Clear large data structures
- Avoid memory leaks
- Use weak references Use CSS transforms for animaink

### 9.3 System Errors
```javascript
const SystemErrors = {
  BROWSER_NOT_SUPPORTED: 'Please use a modern browser',
  JAVASCRIPT_DISABLED: 'JavaScript must be enabled',
  STORAGE_FULL: 'Unable to save data. Please clear browser storage.'
}
```

**Display:**
- Full-page overlay
- Clear instructions
- Help resources
- Alternative options

---

## 10. Performance Optimization

### 10.1 Loading Optimization
- Inline critical CSS
- Defer non-critical JavaScript
- Lazy load images
- Minimize DOM manipulation
-
- Error icon
- Retry button
- Contact support lLID_FORMAT: 'Please enter a valid {field}',
  OUT_OF_RANGE: 'Value must be between {min} and {max}'
}
```

**Display:**
- Red text below field
- Red border on input
- Icon indicator
- Clear on correction

### 9.2 Analysis Errors
```javascript
const AnalysisErrors = {
  INSUFFICIENT_DATA: 'Please provide all required information',
  INVALID_COMBINATION: 'This combination of inputs is not supported',
  CALCULATION_ERROR: 'Unable to calculate results. Please try again.'
}
```

**Display:**
- Alert banner at top