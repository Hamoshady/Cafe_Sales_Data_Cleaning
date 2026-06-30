# ☕ Cafe Sales Data Cleaning

## Project Overview

This project demonstrates a complete data cleaning workflow using Python and Pandas on a messy cafe sales dataset containing **10,000 transactions**. The dataset included missing values, inconsistent column names, invalid entries (`ERROR`, `UNKNOWN`), and incorrect data types. The goal was to clean the data while preserving as many records as possible by using logical imputation instead of unnecessary row deletion.

---

## Dataset Issues

The original dataset contained several data quality problems:

* Inconsistent column names (uppercase letters and extra spaces)
* Invalid values such as `ERROR` and `UNKNOWN`
* Missing values in both numerical and categorical columns
* Incorrect data types
* Incomplete transaction records

---

## Data Cleaning Process

### 1. Data Standardization

* Standardized column names by converting them to lowercase and replacing spaces with underscores.
* Replaced invalid values (`ERROR`, `UNKNOWN`) with `NaN`.
* Converted columns to the appropriate data types (`numeric` and `datetime`).

### 2. Missing Value Imputation

Instead of removing records, missing values were reconstructed whenever possible.

* Restored missing **price_per_unit** values using a predefined item-price mapping.
* Restored safe **item** values only when the price uniquely identified a single product.
* Calculated missing numerical values using the relationship:

```text
total_spent = quantity × price_per_unit
```

* Filled missing **total_spent** and **quantity** whenever the other values were available.
* Filled missing categorical values (`payment_method`, `location`) with `"Unknown"`.
* Removed only the small number of rows that could not be recovered.

---

## Results

| Column           | Missing Before | Missing After |
| ---------------- | -------------: | ------------: |
| transaction_id   |              0 |             0 |
| item             |            969 |             0 |
| quantity         |            479 |             0 |
| price_per_unit   |            533 |             0 |
| total_spent      |            502 |             0 |
| payment_method   |           3178 |             0 |
| location         |           3961 |             0 |
| transaction_date |            460 |             0 |

**Dataset Size**

* Before Cleaning: **10,000 rows**
* After Cleaning: **9,514 rows**

Less than **4.8%** of the data was removed because those records could not be recovered reliably.

---

## Technologies Used

* Python
* Pandas
* NumPy
* Jupyter Notebook

---

## Project Structure

```text
├── dirty_cafe_sales.csv
├── cafe_sales_data_cleaning.ipynb
├── cleaned_cafe_sales.csv
└── README.md
```

---

## How to Run

```bash
git clone https://github.com/your-username/cafe-sales-data-cleaning.git

cd cafe-sales-data-cleaning

pip install pandas numpy jupyter

jupyter notebook
```

---

## Key Learning Outcomes

* Data cleaning with Pandas
* Handling missing values using logical imputation
* Data type conversion
* Dictionary mapping
* Feature validation using mathematical relationships
* Working with real-world messy datasets
