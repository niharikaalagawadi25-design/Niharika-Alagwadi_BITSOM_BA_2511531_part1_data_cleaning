# Task 5: Apply Business Rules

# Business Rules Applied

## 1. Missing Region

**Rule:** Fill missing Region values with **"Unknown"** and report them in the Data Quality Report.

**Action Performed:**

* Blank Region values were replaced with **"Unknown"**.
* These records were counted in the Missing Value Summary of the Data Quality Report.
* The original dataset was not modified.

---

## 2. Missing Ship Mode

**Rule:** Fill missing Ship Mode values with **"Unknown"** and report them in the Data Quality Report.

**Action Performed:**

* Blank Ship Mode values were replaced with **"Unknown"**.
* These records were documented in the Missing Value Summary.

---

## 3. Missing Discount

**Rule:** Treat missing Discount values as **0** only when Quantity, Unit Price, Sales, and Cost contained valid values.

**Action Performed:**

* Blank Discount values were replaced with **0**.
* A new **cleaned_discount** column was created to store the standardized values.
* Original Discount values were retained for reference.

---

## 4. Negative Discount

**Rule:** Negative Discount values must be flagged as invalid.

**Action Performed:**

* Negative Discount values were **not modified**.
* They were identified using the **discount_status** helper column and marked as **"Invalid Discount"**.
* These records were included in the Invalid Discount Summary.

---

## 5. Discount Above Allowed Range

**Rule:** Discount values greater than **1 (100%)** must be flagged as invalid.

**Action Performed:**

* Discounts above the allowed range were retained in the dataset.
* These records were flagged as **"Invalid Discount"** using the **discount_status** column.
* Invalid records were excluded from calculations where appropriate.

---

## 6. Cancelled Orders

**Rule:** Cancelled orders should not contribute to the final completed sales summary.

**Action Performed:**

* Cancelled orders were retained in the cleaned dataset.
* An **order_inclusion** helper column was created.
* Orders with **Order Status = Cancelled** were marked as **Exclude**.
* These records were excluded from completed sales Pivot Tables but remained available for audit purposes.

---

## 7. Failed Payments

**Rule:** Failed payment records should not contribute to the final completed sales summary.

**Action Performed:**

* Failed payment records were retained.
* A **payment_inclusion** helper column was created.
* Records with **Payment Status = Failed** were marked as **Exclude**.
* These records were excluded from completed sales analysis.

---

## 8. Refunded Orders

**Rule:** Refunded orders must be summarized separately.

**Action Performed:**

* Refunded records were retained in the cleaned dataset.
* A **refund_status** helper column was created.
* These records were summarized separately in the Pivot Summary Report.
---

## 9. Ship Date Before Order Date

**Rule:** Ship Date earlier than Order Date must be flagged as an invalid shipping record.

**Action Performed:**

* Shipping dates were compared with Order Dates.
* Records where **Ship Date < Order Date** were flagged as **"Invalid Shipping Record"**.
* These records were marked as **Invalid** in the **data_quality_flag** column and reported in the Date Issue Summary.

---


# Task 9: Write Cleaning Log

## Project
Business Data Cleaning, Validation & Excel Reporting
---

# 1. List of Issues Found

The following data quality issues were identified in the raw dataset:

- Leading and trailing spaces in text fields.
- Inconsistent capitalization (uppercase, lowercase, mixed case).
- Inconsistent spellings and naming conventions.
- Unwanted special characters in some text values.
- Mixed date formats in Order Date and Ship Date columns.
- Missing values in Region.
- Missing values in Ship Mode.
- Missing values in Discount.
- Exact duplicate records.
- Invalid discount values (negative discounts and discounts above the allowed range).
- Ship Date earlier than Order Date.
- Cancelled orders.
- Failed payment records.
- Refunded payment records.

---

# 2. Cleaning Actions Performed

The following cleaning steps were carried out:

- Preserved the original dataset as **raw_orders.xlsx**.
- Created a separate cleaned dataset named **cleaned_orders.xlsx**.
- Removed leading and trailing spaces using the TRIM function.
- Standardized text capitalization using PROPER and UPPER functions where appropriate.
- Corrected inconsistent spellings using Find & Replace.
- Standardized all dates into **dd-mm-yyyy** format.
- Filled missing Region values with **Unknown**.
- Filled missing Ship Mode values with **Unknown**.
- Replaced missing Discount values with **0** where other sales-related fields were valid.
- Converted percentage discount values into decimal format where required.
- Removed exact duplicate records.
- Retained conflicting duplicate Order IDs for review.
- Added calculated columns:
  - cleaned_discount
  - calculated_sales
  - calculated_profit
  - profit_margin
  - shipping_delay_days
  - order_month
  - order_year
  - data_quality_flag
- Created helper columns for:
  - shipping_status
  - discount_status
  - payment_inclusion
  - order_inclusion
  - refund_status

---

# 3. Business Rules Applied

### Missing Region
Blank Region values were replaced with **Unknown** and documented in the Data Quality Report.

### Missing Ship Mode
Blank Ship Mode values were replaced with **Unknown**.

### Missing Discount
Blank Discount values were replaced with **0** only when the remaining sales-related fields were valid.

### Negative Discount
Negative discount values were retained and flagged as **Invalid Discount**.

### Discount Above Allowed Range
Discount values greater than **1 (100%)** were retained and flagged as **Invalid Discount**.

### Cancelled Orders
Cancelled orders were retained in the cleaned dataset but excluded from completed sales summaries and Pivot Tables.

### Failed Payments
Orders with Failed payment status were retained but excluded from completed sales summaries.

### Refunded Orders
Refunded payment records were retained and summarized separately in the Pivot Summary Report.

### Ship Date Before Order Date
Records where Ship Date was earlier than Order Date were flagged as **Invalid Shipping Record**.

---

# 4. Assumptions Made

- Missing Region values represent unavailable information and were replaced with **Unknown**.
- Missing Ship Mode values were replaced with **Unknown**.
- Blank Discount values were assumed to be **0** only when Quantity, Unit Price, Sales, and Cost were available.
- Discount values are expected to remain between **0 and 1**.
- Cancelled and Failed payment orders should not contribute to completed sales analysis.
- Refunded transactions should be reported separately rather than included in completed sales.

---

# 5. Records Removed

- Exact duplicate records were removed from the cleaned dataset.
- Original raw data was preserved without modification.
- Conflicting duplicate Order IDs were not removed automatically.

---

# 6. Records Flagged

The following records were flagged during validation:

- Invalid Discount
- Invalid Shipping Record
- Missing Region (filled as Unknown)
- Missing Ship Mode (filled as Unknown)
- Cancelled Orders
- Failed Payments
- Refunded Payments

Records were classified using the **data_quality_flag** column as:

- Clean
- Warning
- Invalid

---

# 7. Limitations of the Cleaning Process

- Spellings were standardized based on visible inconsistencies only.
- Business validation was limited to the rules provided in the assignment.
- Some business-specific exceptions cannot be verified without additional company information.
- Calculation validation assumes Quantity, Unit Price, Sales, and Cost values are correct in the source dataset.
- Data cleaning was performed using Microsoft Excel without external validation tools.

---

# Summary

The dataset was successfully cleaned, validated, standardized, and prepared for business analysis. Data Quality Reports and Pivot Summary Reports were generated to support management reporting and decision-making.


