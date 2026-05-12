# depaul-admissions-analytics

# DePaul University International Admissions Analytics


---

## 📊 What This Project Does

This project analyzes 5,000 international student applications to DePaul University from 97 countries (2023-2025) to answer one critical question:

**"Why are hundreds of qualified applicants not getting admitted?"**

The answer: **They're not being rejected. They're stuck in the process.**

---

## 🎯 The Problem We Solved

### Before This Analysis

- 7,543 messy application records with duplicate entries
- 33.7% of data was duplicated (inflating applicant counts)
- 47.5% of the database structure was completely empty
- No visibility into why admission rates varied dramatically by country:
  - India: 77.5% admitted
  - Ghana: 26.5% admitted  
  - Nigeria: 31.0% admitted

### Business Impact of the Problem

- Hundreds of qualified students blocked from admission
- Counselor team of 4 overwhelmed with unclear priorities
- One counselor handling 68.9% of all outreach work
- No system to identify which students needed help vs which were rejected

---

## ✅ What We Built

### Week 1: Found the Problems
- Analyzed 7,543 application records across 80 data fields
- Identified 2,543 duplicate entries skewing all metrics
- Documented data quality issues blocking accurate analysis
- Created comprehensive data dictionary (80 fields defined)

📄 [View Week 1 Full Report](reports/Week1_DataExplorationReport.pdf)

### Week 2: Cleaned the Data
- Removed 2,543 duplicate records
- Eliminated 38 completely empty columns
- Fixed phone numbers stored incorrectly (9.20E+11 → readable format)
- Standardized 95 country names ("united states" vs "United States")
- Converted timestamps from computer code to readable dates
- **Result: 7,543 messy rows → 5,000 clean, reliable records**

📄 [View Week 2 Full Report](reports/Week2_DataCleaningReport.pdf)

### Week 3: Built the Dashboard
- Created interactive dashboard with 9 visualizations
- Added 4 filters: Country, Term, Application Source, Counselor
- Enabled one-click analysis: select Ghana → see full recruitment picture instantly
- Color-coded conversion rates (red = needs attention, green = performing well)

📄 [View Week 3 Full Report](reports/Week3_DashboardReport.pdf)

🔗 [**Open Live Dashboard**](https://drive.google.com/file/d/1w_MBMbzHTWoWMGcQhhAV2XeNB5Cmc8EW/view?usp=drivesdk)

🎥 [**Watch 2-Minute Dashboard Demo**](https://drive.google.com/file/d/11BbfQbRZgbt08TFIcLDowZL72ZKj7gCC/view?usp=drivesdk)

---

## 💡 What We Discovered

### Finding #1: Missing Paperwork, Not Missing Qualifications

**895 applicants (17.9%) are blocked by missing transcripts**

- These students submitted applications (showing serious interest)
- They're not rejected (showing they likely qualify)
- They're stuck waiting because paperwork is incomplete
- **100% of students who received follow-up calls got admitted (148 out of 148)**

**What this means:** Every follow-up call = one admitted student

---

### Finding #2: Geographic Performance Gap

| Country | Applications | Admitted | Conversion Rate |
|---------|--------------|----------|-----------------|
| India | 2,684 | 2,080 | **77.5%** ✅ |
| China | 82 | 65 | **79.3%** ✅ |
| United States | 489 | 328 | **67.1%** ✅ |
| Pakistan | 252 | 147 | 58.3% |
| **Ghana** | **412** | **109** | **26.5%** ⚠️ |
| **Nigeria** | **361** | **112** | **31.0%** ⚠️ |

**What this means:** Ghana and Nigeria submit 773 applications but only 221 get admitted. The data shows this is a documentation barrier, not a qualification barrier.

---

### Finding #3: Workload Is Not Balanced

**Counselor Distribution:**
- Jagdeep: 1,244 contacts (68.9%)
- Swarna: 311 contacts (17.2%)
- Ayesha: 166 contacts (9.2%)
- Lavnaya: 85 contacts (4.7%)

**What this means:** One person is handling nearly 70% of all student outreach. This creates a bottleneck and risk if that person is unavailable.

---

### Finding #4: Fall Intake Drives Everything

**Application Volume by Term:**
- Fall 2024: 1,459 applications
- Winter 2024: Moderate volume
- Summer 2025: 50 applications

**What this means:** Marketing budget and counselor capacity should align with Fall deadline timing, not spread evenly across the year.

---

## 🚀 Our Recommendations

### Recommendation 1: Build Automated Transcript Reminder System

**The Opportunity:**
- 895 students waiting with missing transcripts
- Ghana and Nigeria have 773 applications stuck at 28.6% conversion
- Follow-up calls produced 100% admission rate (148 out of 148)

**What To Do:**
1. Send automated email at 7, 14, and 21 days when:
   - Student has not been admitted yet
   - Reason = missing transcript
2. Assign one counselor to specialize in Ghana and Nigeria support

**Expected Impact:**  
Recovering just 50% of stuck Ghana/Nigeria applicants = **220 additional admitted students**

**Revenue Impact:**  
220 students × $16,000 average tuition = **$3.5M+ potential revenue**

---

### Recommendation 2: Rebalance Counselor Workload

**Current State:**
- Jagdeep: 68.9% of workload
- Other 3 counselors: 31.1% combined

**Target State:**
- Jagdeep: 45%
- Swarna: 25%
- Ayesha: 20%
- Lavnaya: 10%

**What To Do:**
- Assign Lavnaya and Ayesha as primary contacts for Ghana and Nigeria
- Use dashboard's Counselor filter to track rebalancing monthly

**Expected Impact:**  
Reduced bottleneck risk, improved response time for students

---

### Recommendation 3: Concentrate Marketing on Fall Intake

**The Data:**
- Fall 2024: 1,459 applications
- Summer 2025: 50 applications

**What To Do:**
- Allocate majority of marketing budget to 3 months before Fall deadline
- Use dashboard's Term filter to compare current intake pace vs last year

**Expected Impact:**  
Higher ROI on marketing spend, better counselor capacity planning

---

### Recommendation 4: Scale the Follow-Up Protocol

**The Proof:**
- Current: 148 follow-up calls → 148 admissions (100% conversion)

**What To Do:**
1. Apply follow-up workflow to ALL applicants where:
   - Not yet admitted
   - Not a hard rejection
2. Track conversion rate monthly to confirm 100% holds at higher volume

**Expected Impact:**  
Convert pending applicants into admitted students systematically

---

## 📈 How to Use This Dashboard

### For Recruitment Managers

**Question: "How is Ghana performing?"**
1. Open dashboard
2. Click Country filter → select Ghana
3. Instantly see:
   - Total applications: 412
   - Admitted: 109
   - Conversion rate: 26.5% (red = needs attention)
   - Which counselors contacted them
   - Why they're not converting (missing transcripts)

**Time from question to answer: 5 seconds**

---

### For Counselors

**Question: "Which students should I call today?"**
1. Open dashboard
2. Click your name in Counselor filter
3. See all your assigned contacts
4. Check Outcome Distribution → prioritize "Missing 0 Transcript" category

---

### For Leadership

**Question: "Where should we invest recruitment budget next year?"**
1. Applications by Term chart → shows Fall drives volume
2. Country Volume chart → shows geographic concentration
3. Conversion Rate table → shows which markets need support vs which are working

**Make budget decisions based on actual data, not guesses**

---

## 🛠️ Technical Details (For Data Teams)

### Tools Used
- **Data Cleaning:** Google Sheets (7-step transformation process)
- **Dashboard:** Looker Studio (9 visualizations, 4 live filters)
- **Analysis:** Python (data profiling and visualization)
- **Documentation:** Comprehensive data dictionaries and field mapping

### Data Quality Improvements
| Metric | Before | After | Improvement |
|--------|--------|-------|-------------|
| Total Rows | 7,543 | 5,000 | 33.7% duplicates removed |
| Total Columns | 80 | 44 | 45% reduction |
| Null Rate | 60.5% | 35.8% | 24.7% improvement |
| Empty Columns | 38 (47.5%) | 0 | 100% cleanup |
| Format Issues | 12 | 0 | Fully standardized |

### Key Transformations
1. Removed 38 completely empty columns
2. Fixed 3 column name spelling errors
3. Removed 2,543 duplicate records (Reference_ID + Intake matching)
4. Standardized 95 country names to Title Case
5. Converted 7 timestamp columns from Unix milliseconds to YYYY-MM-DD
6. Split combined Intake field into Program + Term (4,997 successful)
7. Fixed 176 phone numbers stored as integers

📂 [View Complete Cleaning Documentation](cleaning-documentation/cleaning-process.md)

---

## 📝 Project Impact Summary

✅ **220 recoverable students identified** (documentation gaps, not rejections)  
✅ **$3.5M+ tuition revenue potential** (assuming 50% recovery rate)  
✅ **100% conversion rate on follow-ups** (148 out of 148 admitted)  
✅ **5-second query-to-insight time** (vs hours of manual analysis)  
✅ **Workload rebalancing roadmap** (from 68.9% concentration to 45% target)

---
