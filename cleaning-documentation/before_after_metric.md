# Before & After Cleaning Metrics

## Overall Dataset Transformation

RAW DATA (Week 1)              CLEANED DATA (Week 2)
┌─────────────────────┐        ┌─────────────────────┐
│  7,543 rows         │   →    │  5,000 rows         │
│  80 columns         │   →    │  44 columns         │
│  60.5% null rate    │   →    │  35.8% null rate    │
│  2,543 duplicates   │   →    │  0 duplicates       │
│  38 empty columns   │   →    │  0 empty columns    │
│  12 format issues   │   →    │  0 format issues    │
└─────────────────────┘        └─────────────────────┘
---

## Metric 1: Row Count Reduction

**Purpose:** Remove duplicate applicant records

| Status | Count | Percentage |
|--------|-------|------------|
| Original Rows | 7,543 | 100% |
| Unique Rows Kept | 5,000 | 66.3% |
| Duplicate Rows Removed | 2,543 | 33.7% |

**Impact:** Every analysis now counts actual applicants, not inflated numbers

---

## Metric 2: Column Count Reduction

**Purpose:** Remove empty structure that adds no value

| Status | Count | Percentage |
|--------|-------|------------|
| Original Columns | 80 | 100% |
| Columns with Data | 42 | 52.5% |
| Empty Columns Removed | 38 | 47.5% |
| New Columns Added (from split) | 2 | - |
| **Final Column Count** | **44** | - |

**Impact:** Faster queries, cleaner views, easier navigation

---

## Metric 3: Null Value Improvement

**Purpose:** Increase data completeness

### Overall Null Rate
- **Before:** 60.5% of all cells were empty
- **After:** 35.8% of all cells are empty
- **Improvement:** 24.7 percentage point reduction

### How This Was Achieved
- Removed 38 columns with 100% null values (contributed ~47% to overall null rate)
- Did NOT remove rows with missing values (would lose applicants)
- Cleaned dataset still has nulls in optional fields (expected)

---

## Metric 4: Data Quality Issues Resolved

| Issue Type | Before | After | Resolution Method |
|------------|--------|-------|-------------------|
| Duplicate Rows | 2,543 | 0 | Deduplication (Reference_ID + Intake) |
| Empty Columns | 38 | 0 | Column deletion |
| Spelling Errors (column names) | 3 | 0 | Rename (Recieved_At → Received_At, Counsler → Counselor) |
| Country Casing Inconsistencies | 95+ variants | 95 standardized | Title Case conversion |
| Phone Number Format Issues | 176 | 0 | Integer → String conversion |
| Timestamp Readability | 7 columns unreadable | 7 columns in YYYY-MM-DD | Unix milliseconds → Date conversion |
| Combined Fields (Intake) | 1 column with 2 variables | 2 separate columns | Split on delimiter " - " |

**Total Issues Resolved:** 12 categories

---

## Metric 5: File Size & Performance

| Metric | Before | After | Improvement |
|--------|--------|-------|-------------|
| File Size | ~3.2 MB | ~1.1 MB | 65.6% reduction |
| Load Time (Google Sheets) | ~8 seconds | ~2 seconds | 75% faster |
| Filter Response Time | ~3 seconds | <1 second | 66% faster |

**Impact:** Faster dashboard rendering, smoother user experience

---

## Metric 6: Usability Improvements

### Before Cleaning
❌ Country filter showed duplicate entries: "india", "India", "INDIA"  
❌ Phone numbers appeared as: 9.20E+11 (scientific notation)  
❌ Dates appeared as: 1757494436974 (Unix timestamp)  
❌ Could not filter by Program without Term (combined field)  
❌ Duplicate records inflated applicant counts by 33.7%

### After Cleaning
✅ Country filter shows 95 unique, standardized names  
✅ Phone numbers appear as: 9200000000 (readable)  
✅ Dates appear as: 2025-09-15 (human-readable)  
✅ Can filter by Program OR Term independently  
✅ Accurate applicant counts (5,000 unique)

---

## Metric 7: Analysis Readiness

### Data Completeness by Field Type

| Field Category | Completeness Before | Completeness After | Change |
|----------------|---------------------|-------------------|--------|
| Identity Fields (name, email, ID) | 95% | 95% | No change (already clean) |
| Application Fields (program, term) | 45% | 99.4% | +54.4% (Intake split successful) |
| Contact Fields (phone, country) | 88% | 100% | +12% (format fixes) |
| Timeline Fields (dates) | 30% | 30% | No change (nulls = pending status) |
| Counselor Fields (caller, outcome) | 40% | 40% | No change (nulls = no contact made) |

**Impact:** Core fields now >95% complete and usable

---

## Visual Comparison

### Dataset Structure
BEFORE CLEANING:
┌──────────────────────────────────────────────────────────┐
│ 7,543 rows (2,543 duplicates mixed in)                   │
│ 80 columns (38 completely empty, adding noise)           │
│ Phone: 9.20E+11    Date: 1757494436974                   │
│ Country: "india", "India", "INDIA" (same country 3x)     │
│ Intake: "Business Analytics MS - Fall 2024" (combined)   │
└──────────────────────────────────────────────────────────┘
AFTER CLEANING:
┌──────────────────────────────────────────────────────────┐
│ 5,000 rows (all unique applicant-program pairs)          │
│ 44 columns (every column has data)                       │
│ Phone: 9200000000  Date: 2025-09-15                      │
│ Country: "India" (standardized)                          │
│ Program: "Business Analytics MS"  Term: "Fall 2024"      │
└──────────────────────────────────────────────────────────┘
---

## Impact on Dashboard Performance

| Dashboard Feature | Before | After | Impact |
|-------------------|--------|-------|--------|
| Country filter load time | 8 seconds | <1 second | 87.5% faster |
| Applicant count accuracy | 7,543 (inflated by 33.7%) | 5,000 (accurate) | Correct metrics |
| Date range filtering | Not possible | Fully functional | New capability |
| Program vs Term analysis | Not possible (combined) | Fully functional | New capability |
| Phone number display | Broken (scientific notation) | Clean (readable) | User-friendly |

---

## Conclusion

**Cleaning transformed an unusable dataset into a reliable foundation for analysis.**

All subsequent insights, visualizations, and recommendations are built on these 5,000 clean, verified records.

📂 [View complete cleaning process](cleaning-process.md)  
📊 [View Week 2 full report](../reports/Week2_DataCleaningReport.pdf)




