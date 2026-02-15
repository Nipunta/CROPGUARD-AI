# Requirements Document - Crop Residue Utilization Analyzer

## 1. Project Overview

### 1.1 Purpose
Develop an AI-powered decision support system to help farmers make optimal choices for crop residue management, promoting sustainable agriculture and reducing crop burning incidents in India.

### 1.2 Target Users
- **Primary**: Small to medium-scale farmers (2-20 acres)
- **Secondary**: Agricultural extension workers, KVK staff, NGOs
- **Tertiary**: Government agriculture departments, policy makers

### 1.3 Problem Statement
- Crop burning causes severe air pollution (especially in Punjab, Haryana, UP)
- Farmers lack awareness of profitable alternatives
- Complex government subsidy schemes are not easily accessible
- No centralized tool for residue management decision-making
- Financial constraints prevent adoption of sustainable methods

### 1.4 Solution
A comprehensive web-based and Python tool that:
- Analyzes farmer's specific situation
- Recommends optimal residue utilization methods
- Provides government subsidy information
- Shows environmental and financial impact
- Offers step-by-step implementation guidance

---

## 2. Functional Requirements

### 2.1 Input Requirements

#### 2.1.1 Mandatory Inputs
| Field | Type | Validation | Example |
|-------|------|------------|---------|
| Crop Type | Dropdown | Must select from list | Rice, Wheat, Cotton, Sugarcane, Maize |
| Land Size | Number | Min: 0.5, Max: 1000 acres | 5 acres |
| Residue Quantity | Number | Min: 1, Max: 10000 tons | 15 tons |
| Location | Text | State/District format | Ludhiana, Punjab |
| Distance to Plant | Number | Min: 0, Max: 500 km | 25 km |
| Budget | Number | Min: 0, Max: 10000000 INR | 50000 |
| Labor Availability | Dropdown | Low/Medium/High | Medium |
| Transport Access | Dropdown | Poor/Good/Excellent | Good |

#### 2.1.2 Optional Inputs
- Available machinery (multi-select)
- Previous experience with methods
- Soil type
- Water availability
- Cooperative membership

### 2.2 Analysis Requirements

#### 2.2.1 Method Evaluation
System must evaluate at least 5 methods:
1. **Composting** - Convert to organic fertilizer
2. **Biogas Production** - Generate cooking fuel + fertilizer
3. **Biomass Resale** - Sell to power plants/pellet units
4. **Biochar Production** - Create soil amendment
5. **Mulching/Incorporation** - Direct soil enrichment

#### 2.2.2 Scoring Criteria
Each method must be scored on:
- **Feasibility** (0-100%): Based on resources, budget, location
- **Setup Cost** (INR): Initial investment required
- **Expected Revenue/Savings** (INR): Financial returns
- **Payback Period** (months): Time to break even
- **Effort Level** (Low/Medium/High): Labor and management
- **Risk Assessment**: Potential challenges and limitations

#### 2.2.3 Ranking Algorithm
```
Feasibility Score = Base Score + Adjustments

Adjustments based on:
- Budget availability (+/- 30%)
- Distance to facilities (+/- 25%)
- Labor availability (+/- 20%)
- Transport access (+/- 20%)
- Machinery ownership (+/- 15%)
```

### 2.3 Output Requirements

#### 2.3.1 Visual Analytics
Must include:
1. **Feasibility Comparison Chart**
   - Bar chart showing top 3 methods
   - Percentage scores (0-100%)
   - Color-coded (gradient)
   - Animated on load

2. **Financial Comparison Chart**
   - Bar chart showing revenue potential
   - Scaled to highest value
   - Display in thousands (K)
   - Sortable by returns

3. **Environmental Impact Chart**
   - Pie chart showing CO2 comparison
   - Green: CO2 saved
   - Red: CO2 if burned
   - Tree planting equivalent

#### 2.3.2 Government Subsidies Section
Must display:
- Scheme name (official)
- Type (Central/State)
- Subsidy percentage and limits
- Applicable equipment/methods
- Eligibility criteria
- Application process
- Required documents
- Official website links
- Contact information

**Minimum Coverage:**
- 3 Central Government schemes
- State-specific schemes for 5+ major states
- Auto-detection based on location

#### 2.3.3 Contact Information
Must provide:
- National helplines (toll-free)
- State agriculture department contacts
- District office information
- KVK (Krishi Vigyan Kendra) details
- Email addresses
- Physical addresses
- Office timings
- Services offered

**Auto-population:**
- Detect state from location input
- Show relevant state contacts
- Prioritize local resources

#### 2.3.4 Action Plan
Must include:
- Minimum 5-7 detailed steps
- Specific costs (equipment rental, materials)
- Timeline for each step
- Where to get help (KVK, Agriculture Office)
- Technical specifications (measurements, ratios)
- Safety precautions
- Quality checkpoints

#### 2.3.5 Additional Information
- Important tips and best practices
- Legal requirements and compliance
- Common mistakes to avoid
- Success metrics to track
- Follow-up recommendations

### 2.4 Report Generation

#### 2.4.1 Print Functionality
- Print-friendly CSS
- Remove form and buttons
- Keep all analysis and charts
- Professional formatting
- Page break optimization

#### 2.4.2 PDF Export
- Download as PDF option
- Preserve formatting
- Include all charts
- Maintain readability

#### 2.4.3 Share Options
- Email report
- WhatsApp share
- Copy link
- Social media share

---

## 3. Non-Functional Requirements

### 3.1 Performance Requirements
- **Page Load Time**: < 2 seconds
- **Analysis Time**: < 1 second
- **Chart Rendering**: < 500ms
- **Mobile Load Time**: < 3 seconds

### 3.2 Usability Requirements
- **Language**: Simple, farmer-friendly Hindi/English
- **Reading Level**: 8th grade or below
- **Form Completion Time**: < 3 minutes
- **Learning Curve**: < 5 minutes for first-time users
- **Error Messages**: Clear and actionable

### 3.3 Accessibility Requirements
- **Screen Reader**: Compatible
- **Keyboard Navigation**: Full support
- **Color Contrast**: WCAG AA compliant
- **Font Size**: Minimum 14px
- **Touch Targets**: Minimum 44x44px

### 3.4 Compatibility Requirements

#### 3.4.1 Browser Support
- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+
- Opera 76+
- Mobile browsers (iOS Safari, Chrome Mobile)

#### 3.4.2 Device Support
- Desktop (1920x1080 to 1366x768)
- Tablet (1024x768 to 768x1024)
- Mobile (375x667 to 414x896)
- Responsive breakpoints at 768px and 1024px

#### 3.4.3 Operating Systems
- Windows 10/11
- macOS 10.15+
- Linux (Ubuntu, Fedora)
- Android 8+
- iOS 13+

### 3.5 Security Requirements
- **Data Privacy**: No personal data stored
- **Input Validation**: Sanitize all inputs
- **XSS Prevention**: Escape user inputs
- **HTTPS**: Required for production
- **No External Dependencies**: Minimize attack surface

### 3.6 Reliability Requirements
- **Uptime**: 99.5% (if hosted)
- **Error Handling**: Graceful degradation
- **Offline Mode**: Full functionality without internet
- **Data Persistence**: Local storage for form data
- **Backup**: Regular backups if hosted

### 3.7 Maintainability Requirements
- **Code Documentation**: Inline comments
- **Modular Design**: Separate functions
- **Version Control**: Git-based
- **Update Frequency**: Quarterly for subsidies
- **Bug Fixes**: Within 48 hours

---

## 4. Data Requirements

### 4.1 Crop Database
Must include data for:
- Rice (Paddy)
- Wheat
- Sugarcane
- Cotton
- Maize
- Bajra
- Jowar
- Pulses

**Data per crop:**
- Average residue per acre
- Typical residue-to-crop ratio
- Seasonal variations
- Regional differences

### 4.2 Government Schemes Database

#### 4.2.1 Central Schemes
1. **Crop Residue Management (CRM) Scheme**
   - Subsidy: 50% (individual), 80% (cooperative)
   - Limit: ₹1L (individual), ₹10L (cooperative)
   - Contact: 1800-180-1551
   - Website: agricoop.nic.in

2. **PM-KUSUM Scheme**
   - Subsidy: 60%
   - For: Solar/biogas equipment
   - Contact: 011-2436-0707
   - Website: pmkusum.mnre.gov.in

3. **National Biofuel Policy**
   - MSP: ₹2000-3000/ton
   - For: Biomass resale
   - Website: petroleum.nic.in

#### 4.2.2 State Schemes
Must cover:
- Punjab
- Haryana
- Uttar Pradesh
- Madhya Pradesh
- Rajasthan
- Bihar
- West Bengal
- Maharashtra
- Karnataka
- Tamil Nadu

**Data per state:**
- Scheme name
- Subsidy percentage
- Maximum amount
- Eligibility
- Contact details
- Application process

### 4.3 Contact Database

#### 4.3.1 National Contacts
- Kisan Call Centre: 1800-180-1551
- Ministry of Agriculture: 011-2338-2651
- MNRE: 011-2436-0707
- ICAR: 011-2584-2806

#### 4.3.2 State Contacts
For each major state:
- Agriculture department phone
- Agriculture department email
- Department address
- Office timings
- Key officials

#### 4.3.3 District Resources
- District Agriculture Office (generic info)
- KVK locator information
- Biomass plant directory
- Equipment rental services

### 4.4 Cost Database
Must maintain current prices for:
- Equipment rental (per acre)
- Machinery purchase
- Labor costs (per day)
- Transport costs (per km)
- Material costs (decomposer, etc.)
- Market prices (compost, biochar, biomass)

**Update Frequency:** Quarterly

---

## 5. Integration Requirements

### 5.1 External APIs (Optional)
- Weather API for timing recommendations
- Location API for auto-detection
- SMS API for sending reports
- Email API for sharing reports

### 5.2 Backend Integration (Future)
- Database for storing farmer data
- Analytics for usage tracking
- Admin panel for content updates
- Feedback collection system

### 5.3 Mobile App Integration (Future)
- React Native wrapper
- Offline-first architecture
- Push notifications
- Camera for document upload

---

## 6. Localization Requirements

### 6.1 Language Support
**Phase 1 (Current):**
- English (primary)
- Hindi labels (secondary)

**Phase 2 (Future):**
- Full Hindi translation
- Punjabi
- Marathi
- Tamil
- Telugu
- Bengali

### 6.2 Regional Customization
- State-specific schemes
- Local crop varieties
- Regional terminology
- Local contact information
- Currency format (INR)

---

## 7. Compliance Requirements

### 7.1 Legal Compliance
- Comply with IT Act 2000
- Follow agricultural guidelines
- Accurate subsidy information
- Disclaimer for recommendations
- Terms of use

### 7.2 Data Protection
- No personal data collection (current version)
- GDPR-ready architecture (future)
- Data retention policy
- User consent mechanism

### 7.3 Agricultural Standards
- Follow ICAR guidelines
- Align with government policies
- Accurate technical information
- Safety recommendations

---

## 8. Testing Requirements

### 8.1 Functional Testing
- Input validation testing
- Calculation accuracy testing
- Chart rendering testing
- Print functionality testing
- Cross-browser testing

### 8.2 Usability Testing
- Farmer user testing (5+ farmers)
- Extension worker testing (3+ workers)
- Time-to-complete testing
- Error recovery testing
- Accessibility testing

### 8.3 Performance Testing
- Load time testing
- Stress testing (multiple users)
- Mobile performance testing
- Offline functionality testing

### 8.4 Acceptance Criteria
- 90% of farmers can complete form without help
- 95% accuracy in recommendations
- 100% of subsidies are current and accurate
- Zero critical bugs
- < 3 seconds load time on 3G

---

## 9. Documentation Requirements

### 9.1 User Documentation
- Quick start guide (2 pages)
- User manual (10 pages)
- FAQ (20 questions)
- Video tutorials (5 videos)
- Troubleshooting guide

### 9.2 Technical Documentation
- System architecture
- API documentation
- Database schema
- Deployment guide
- Maintenance guide

### 9.3 Training Materials
- Farmer training presentation
- Extension worker training
- Train-the-trainer guide
- Case studies
- Success stories

---

## 10. Deployment Requirements

### 10.1 Hosting Options
**Option 1: Static Hosting**
- GitHub Pages
- Netlify
- Vercel
- AWS S3 + CloudFront

**Option 2: Server Hosting**
- Shared hosting
- VPS (DigitalOcean, Linode)
- Cloud (AWS, Azure, GCP)

### 10.2 Domain Requirements
- Memorable domain name
- .in or .org extension
- SSL certificate (HTTPS)
- CDN for faster loading

### 10.3 Backup Requirements
- Daily backups
- Version control (Git)
- Disaster recovery plan
- Rollback capability

---

## 11. Success Metrics

### 11.1 Usage Metrics
- Number of analyses performed
- Unique users per month
- Average session duration
- Form completion rate
- Return user rate

### 11.2 Impact Metrics
- Farmers helped
- Residue managed (tons)
- CO2 emissions prevented (kg)
- Subsidies claimed (₹)
- Burning incidents reduced

### 11.3 Quality Metrics
- User satisfaction (1-5 stars)
- Recommendation accuracy
- Subsidy information accuracy
- Bug reports per month
- Support requests per month

---

## 12. Future Enhancements

### 12.1 Phase 2 Features
- User accounts and history
- Equipment marketplace
- Farmer community forum
- Success story sharing
- Video tutorials

### 12.2 Phase 3 Features
- Mobile app (Android/iOS)
- SMS-based interface
- Voice input support
- AI chatbot assistance
- Satellite imagery integration

### 12.3 Phase 4 Features
- Blockchain for subsidy tracking
- IoT sensor integration
- Predictive analytics
- Market price forecasting
- Cooperative management tools

---

## 13. Constraints and Assumptions

### 13.1 Constraints
- Limited budget for hosting
- No dedicated backend initially
- Volunteer-based maintenance
- Dependency on government data accuracy
- Internet connectivity in rural areas

### 13.2 Assumptions
- Farmers have basic smartphone/computer access
- Extension workers can assist with tool usage
- Government subsidy schemes remain stable
- Market prices fluctuate within normal range
- Users have basic digital literacy

---

## 14. Risks and Mitigation

### 14.1 Technical Risks
| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| Browser incompatibility | High | Low | Extensive testing, fallbacks |
| Slow loading on 2G | High | Medium | Optimize assets, offline mode |
| Chart rendering issues | Medium | Low | Use lightweight library |
| Data accuracy | High | Medium | Regular updates, verification |

### 14.2 Operational Risks
| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|------------|
| Outdated subsidy info | High | Medium | Quarterly updates, disclaimer |
| Incorrect recommendations | High | Low | Validation, user feedback |
| Low adoption | High | Medium | Training, awareness campaigns |
| Maintenance burden | Medium | High | Documentation, community support |

---

## 15. Approval and Sign-off

### 15.1 Stakeholders
- Agricultural experts
- Farmer representatives
- Government officials
- NGO partners
- Technical team

### 15.2 Review Cycle
- Requirements review: Quarterly
- Feature updates: Monthly
- Bug fixes: As needed
- Subsidy updates: Quarterly

---

**Document Version:** 1.0  
**Last Updated:** February 14, 2026  
**Status:** Approved  
**Next Review:** May 14, 2026
