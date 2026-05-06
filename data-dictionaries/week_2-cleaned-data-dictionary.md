# Week 2: Cleaned Data Dictionary

## Dataset Overview
- **Source:** DePaul University International Student Applications (cleaned)
- **Time Period:** 2023-2025 intake cycles
- **Total Records (Cleaned):** 5,000 rows (2,543 duplicates removed)
- **Total Fields (Cleaned):** 44 columns (38 empty columns removed)

---

## Cleaning Transformations Applied

| Transformation | Before | After | Records Affected |
|----------------|--------|-------|------------------|
| Remove duplicates | 7,543 rows | 5,000 rows | 2,543 removed |
| Remove empty columns | 80 columns | 44 columns | 38 removed |
| Fix column names | 3 spelling errors | 0 errors | 3 renamed |
| Standardize country casing | 95 variants | 95 standardized | All country values |
| Convert timestamps | Unix milliseconds | YYYY-MM-DD | 7 columns |
| Split Intake field | Combined | Separated | 4,997 of 5,000 |
| Fix phone numbers | Integer/scientific | String | 176 values |

---

## Core Identity Fields (Cleaned)

| Field Name | Data Type | Description | Cleaning Applied |
|------------|-----------|-------------|------------------|
| Reference_ID | String | Unique applicant identifier | None (already clean) |
| Given_Name | String | Applicant first or given name | None |
| Email_id | String | Applicant email address | None |
| Phone_number | String | Primary contact phone | **Converted from integer to string**, removed trailing ".0" |
| Country | String | Applicant's country of origin | **Standardized to Title Case** (e.g., "united states" → "United States") |

---

## Application Tracking (Cleaned)

| Field Name | Data Type | Description | Cleaning Applied |
|------------|-----------|-------------|------------------|
| Received_At | Date | Record receipt timestamp | **Renamed from Recieved_At**, converted from Unix milliseconds to YYYY-MM-DD |
| Received_At_2 | Date | Secondary timestamp | **Renamed from Recieved_At-2**, converted to YYYY-MM-DD |
| Admit_Date | Date | Admission decision date | Converted to YYYY-MM-DD (null = not yet admitted) |
| Program | String | Degree program (separated from Intake) | **NEW: Split from combined Intake field** |
| Term | String | Intake period (separated from Intake) | **NEW: Split from combined Intake field** |

---

## Counselor Engagement (Cleaned)

| Field Name | Data Type | Description | Cleaning Applied |
|------------|-----------|-------------|------------------|
| Counselor | String | Assigned counselor name | **Renamed from Counsler** |
| Caller_Name | String | Counselor who contacted applicant | None (values: Jagdeep, Swarna, Ayesha, Lavnaya) |
| Outcome_1 | String | Result of outreach contact | None (still free-text) |
| Attempts | Integer | Number of contact attempts | None |

---

## New Calculated Fields (Dashboard)

| Field Name | Formula | Purpose |
|------------|---------|---------|
| Conversion_Rate | (Admit_Date not null / Reference_ID count) × 100 | Percentage of applicants admitted per country |

---

## Removed Columns (38 total)

**Reason:** 100% empty across all 7,543 rows

Examples of removed columns:
- Citizenship
- Status
- Major
- housing_contracts
- Most_Recent_Decisions
- (33 additional columns with no data)

---

## Data Quality Metrics: Before vs After

| Metric | Raw Data (Week 1) | Cleaned Data (Week 2) | Improvement |
|--------|-------------------|----------------------|-------------|
| **Total Rows** | 7,543 | 5,000 | -33.7% (duplicates removed) |
| **Total Columns** | 80 | 44 | -45% (empty columns removed) |
| **Overall Null Rate** | 60.5% | 35.8% | -24.7 percentage points |
| **Duplicate Rows** | 2,543 (33.7%) | 0 | 100% eliminated |
| **Empty Columns** | 38 (47.5%) | 0 | 100% eliminated |
| **Format Inconsistencies** | 12 issues | 0 | Fully standardized |

---

## Field Relationships (Cleaned)

**Group 1: Applicant Identity**  
Reference_ID (unique) → Given_Name, Email_id, Phone_number, Country

**Group 2: Application Process**  
Reference_ID → Term, Program, University, College_1st_Choice → Admit_Date → Application_Source → Slate_Form_Filled

**Group 3: Counselor Outreach**  
Reference_ID → Caller_Name → Attempts → Outcome_1  
(Note: Not every applicant has a Caller_Name value = not all were contacted)

---

## Usage Notes

This data dictionary represents the **cleaned, analysis-ready state** of the dataset after Week 2 transformations.

All 5,000 rows are unique applicant-program combinations (duplicates removed).  
All 44 columns contain at least some populated data (empty columns removed).

For transformation details, see:  
📂 [Cleaning Process Documentation](../cleaning-documentation/cleaning-process.md)
