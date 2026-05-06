# Data Cleaning Process: 7 Steps

## Process Overview

**Input:** 7,543 rows × 80 columns (raw DePaul application data)  
**Output:** 5,000 rows × 44 columns (analysis-ready dataset)  
**Tool:** Google Sheets  
**Documentation:** [View transformation log](https://docs.google.com/spreadsheets/d/16a9t0CX49NpcWSXF_cpmZnsEO_Z8ccT/edit)

---

## Step 1: Remove Empty Columns

### Problem
38 columns (47.5% of structure) contained no data across all 7,543 rows

### Examples of Empty Columns
- Citizenship
- Status
- Major
- housing_contracts
- Most_Recent_Decisions
- (33 additional columns)

### Action
Deleted all 38 columns with 100% null values

### Result
- **Before:** 80 columns
- **After:** 42 columns
- **Impact:** Reduced file size, improved query performance, eliminated visual noise

---

## Step 2: Fix Column Name Errors

### Problem
Three column names contained spelling mistakes

### Corrections Made
| Before | After | Issue |
|--------|-------|-------|
| Recieved_At | Received_At | Spelling error ("i before e") |
| Recieved_At-2 | Received_At_2 | Spelling error + hyphen instead of underscore |
| Counsler | Counselor | Spelling error (missing "o") |

### Result
- Consistent naming convention (underscore_separated)
- Proper English spelling for documentation and code
- No hyphenated field names (breaks some SQL queries)

---

## Step 3: Remove Duplicates

### Problem
2,543 records (33.7% of dataset) were duplicated

### Detection Method
Matched rows on two fields:
1. Reference_ID (applicant identifier)
2. Intake (program + term)

### Example Duplicate
**Reference_ID:** 209623088  
**Student:** Rohan Rameshbhai Kevadiya  
**Occurrences:** 5 rows (4 duplicates)  
**Matching fields:** Same intake, address, email, all data identical

### Action
- Kept first occurrence of each Reference_ID + Intake combination
- Deleted subsequent duplicate rows

### Result
- **Before:** 7,543 rows
- **After:** 5,000 rows
- **Removed:** 2,543 duplicate records
- **Impact:** Accurate applicant counts, no inflated metrics

---

## Step 4: Standardize Country Casing

### Problem
Same country appeared multiple times due to inconsistent casing:
- "united states" vs "United States"
- "india" vs "India"
- "PAKISTAN" vs "Pakistan"

This caused the same country to appear as 2-3 separate entries in analysis.

### Action
Converted all 95 country names to Title Case format

### Examples
| Before | After |
|--------|-------|
| united states | United States |
| INDIA | India |
| pakistan | Pakistan |
| CHINA | China |

### Result
- **Before:** 95+ country variants (duplicates due to casing)
- **After:** 95 unique countries (standardized)
- **Impact:** Accurate country-level aggregation and filtering

---

## Step 5: Convert Timestamps

### Problem
Seven columns stored dates as 13-digit Unix milliseconds (unreadable by humans)

**Example:** 1757494436974 instead of "2025-09-15"

### Columns Affected
- Received_At
- Received_At_2
- Created_At
- Modified_At
- Updated_At
- (2 additional timestamp fields)

### Action
Converted all 7 columns from Unix milliseconds to YYYY-MM-DD format

### Formula Used (Google Sheets)
=TEXT((A2/1000 + 25569), "YYYY-MM-DD")

### Result
- **Before:** 1757494436974 (computer-readable only)
- **After:** 2025-09-15 (human-readable)
- **Impact:** Enabled date filtering, trend analysis, timeline visualization

---

## Step 6: Split Intake Column

### Problem
The Intake field combined two separate data points in one cell:
- Program name (e.g., "Business Analytics MS")
- Term (e.g., "Fall 2024")

**Example value:** "Business Analytics MS - Fall 2024"

This violated tidy data principles (one variable per column).

### Action
Split Intake into two new columns using delimiter " - "

1. **Program:** Everything before " - "
2. **Term:** Everything after " - "

### Formula Used (Google Sheets)
=SPLIT(A2, " - ")

### Result
- **Before:** 1 combined column (5,000 values)
- **After:** 2 separate columns (4,997 successfully split)
- **Failed:** 3 rows with non-standard format (manually reviewed)
- **Impact:** Enabled filtering by program OR term independently

### Example
| Before (Intake) | After (Program) | After (Term) |
|-----------------|-----------------|--------------|
| Business Analytics MS - Fall 2024 | Business Analytics MS | Fall 2024 |
| Data Science MS - Winter 2025 | Data Science MS | Winter 2025 |

---

## Step 7: Fix Phone Number Types

### Problem
176 phone numbers were stored as integers instead of strings

**Issues caused:**
1. Leading zeros were lost (important for some countries)
2. Numbers appeared in scientific notation: 9.20E+11
3. Trailing ".0" appeared on some numbers: 1234567890.0

### Action
1. Converted all phone number cells from Number format to Plain Text format
2. Removed trailing ".0" artifacts using find-and-replace

### Formula Used (Google Sheets)
REGEXREPLACE(A2, ".0$", "")

### Result
- **Before:** 9200000000.0 or 9.20E+11 (integer format)
- **After:** 9200000000 (string format, preserves leading zeros)
- **Records affected:** 176 phone numbers
- **Impact:** Accurate international phone number storage

---

## Validation & Quality Control

### Post-Cleaning Checks Performed

✅ **Duplicate Check**  
Re-ran duplicate detection → 0 duplicates found

✅ **Null Value Audit**  
Overall null rate reduced from 60.5% → 35.8%

✅ **Column Count Verification**  
Confirmed 44 columns remaining, all contain data

✅ **Data Type Validation**  
- All timestamps in YYYY-MM-DD format
- All phone numbers stored as text
- All countries in Title Case

✅ **Row Count Verification**  
5,000 unique applicant-program combinations (Reference_ID + Term)

---

## Before vs After Summary

| Metric | Before Cleaning | After Cleaning | Change |
|--------|----------------|----------------|--------|
| Total Rows | 7,543 | 5,000 | -2,543 (duplicates) |
| Total Columns | 80 | 44 | -36 (empty columns removed, +2 new from split) |
| Null Rate | 60.5% | 35.8% | -24.7 percentage points |
| Empty Columns | 38 | 0 | -38 |
| Duplicate Records | 2,543 | 0 | -2,543 |
| Format Issues | 12 | 0 | All resolved |
| Spelling Errors | 3 column names | 0 | All corrected |

---

## Files & Resources

📄 **Transformation Log:** [Google Sheets with step-by-step edits](https://docs.google.com/spreadsheets/d/16a9t0CX49NpcWSXF_cpmZnsEO_Z8ccT/edit)

📊 **Before/After Metrics:** [View comparison charts](before-after-metrics.md)

📋 **Data Dictionary:** [Cleaned field definitions](../data-dictionaries/week2-cleaned-data-dictionary.md)

