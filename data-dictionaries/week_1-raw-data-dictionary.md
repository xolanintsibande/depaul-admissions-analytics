# Week 1: Raw Data Dictionary

## Dataset Overview
- **Source:** DePaul University International Student Applications
- **Time Period:** 2023-2025 intake cycles
- **Total Records (Raw):** 7,543 rows
- **Total Fields (Raw):** 80 columns

---

## Core Identity Fields

| Field Name | Data Type | Description | Quality Notes |
|------------|-----------|-------------|---------------|
| Reference_id | Integer | Unique applicant identifier (primary key) | Range: 291,925 to 999,518,802 |
| Given_Name | String | Applicant first or given name | Some null values |
| Email_id | Text | Applicant email address | Primary contact method |
| Phone_number | String | Primary contact phone | **Issue:** Inconsistent formats, some stored as scientific notation (9.20E+11) |

---

## Academic Background

| Field Name | Data Type | Description | Quality Notes |
|------------|-----------|-------------|---------------|
| College | String | Composite field: country + university + degree | **Issue:** Multi-line text format, difficult to parse |
| Major | String | Undergraduate major field | Empty in raw dataset |
| University | Text | Target institution for application | Populated |
| Degree_type | Text | Applicant qualification level | High percentage of null values |

---

## Application Tracking

| Field Name | Data Type | Description | Quality Notes |
|------------|-----------|-------------|---------------|
| Recieved_At | Timestamp | Record receipt timestamp (Unix milliseconds) | **Issue:** Spelling error, stored as milliseconds |
| Birth_Date | Date | Applicant date of birth | Some null values |
| Admit_Date | Date | Admission decision date | Null = not yet admitted |
| Intake | Text | Application intake period | Format: "Program - Term" (combined field) |

---

## Geographic Data

| Field Name | Data Type | Description | Quality Notes |
|------------|-----------|-------------|---------------|
| Country | String | Applicant's country of origin | **Issue:** Inconsistent casing ("united states" vs "United States") |
| Region | String | Geographic region classification | High percentage of null values |

---

## Counselor Engagement

| Field Name | Data Type | Description | Quality Notes |
|------------|-----------|-------------|---------------|
| Counselor | String | Assigned counselor name | High percentage of null values |
| Caller_name | Text | Name of counselor who contacted applicant | Values: Jagdeep, Swarna, Ayesha, Lavnaya |
| Outcome_1 | Text | Result of outreach contact | Free-text, inconsistent formatting |
| Comment | Text | Additional application notes | Free-text, no standardization |

---

## Known Data Quality Issues

### Critical Issues
1. **2,543 duplicate records** (33.7% of dataset)
   - Example: Reference_id 209623088 appears 5 times
   - Duplicates identified by matching Reference_id + Intake

2. **38 completely empty columns** (47.5% of structure)
   - Examples: Citizenship, Status, Major, housing_contracts
   - Add no analytical value

3. **Phone number formatting**
   - Scientific notation: 9.20E+11 instead of 920000000000
   - Lost leading zeros for some regions

4. **Country naming inconsistencies**
   - Same country appears multiple times: "india", "India", "United states", "United States"
   - Causes segmentation errors in analysis

### Moderate Issues
5. **Multi-line College field**
   - Stores country + institution + degree in one cell
   - Violates first normal form
   - Difficult to parse programmatically

6. **Column naming spelling error**
   - RECIEVED_AT should be RECEIVED_AT

7. **Missing values in key fields**
   - Counselor: high null rate
   - Degree_type: high null rate
   - Admit_date: null = pending/not admitted
   - Region: high null rate

### Documentation Gaps
8. **Undocumented free-text fields**
   - Outcome_1: no standard categories defined
   - Comment: no structure or format guidelines
   - Caller_name: no role or ID definitions

---

## Field Relationships

**Applicant Identity**  
Reference_id (unique) → Given_Name, Email_id, Phone_number, Country

**Application Process**  
Reference_id → Intake, University, College, Major, Degree_type → Admit_Date

**Counselor Outreach**  
Reference_id → Caller_name → Outcome_1, Comment  
(Note: Not all applicants have counselor contact records)

---

## Usage Notes

This data dictionary represents the **raw, uncleaned state** of the dataset as received in Week 1.

For the cleaned version after Week 2 transformations, see:  
📂 [Week 2 Cleaned Data Dictionary](week2-cleaned-data-dictionary.md)
