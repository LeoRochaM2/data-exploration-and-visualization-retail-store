# Data Exploration and Visualization – Retail Store Sales

## ▸ Project Overview
- **Exploratory data analysis:** structured investigation of a retail transaction dataset
- **Feature understanding:** distributions, relationships, and data quality checks
- **Insight-driven focus:** analysis aimed at uncovering meaningful patterns in sales behavior

## ▸ Tech Stack
- **Language:** Python
- **Data analysis:** Pandas, NumPy
- **Visualization:** Matplotlib, Seaborn
- **Workflow:** Jupyter Notebook (VS Code)

## ▸ Project Context
- **Academic origin:** university project (data cleaning portion reused/extended from a prior data-wrangling course assignment)
- **Design goal:** applied EDA workflow reflecting standard data science practice

---

## 1. Dataset Overview

**Source**: `retail_store_sales.csv` — retail store transaction data

**Main Columns**:
- `price_per_unit`, `quantity`, `total_spent`: transaction-level numeric values
- `category`, `item`: product classification
- `payment_method`: Cash, Credit Card, Digital Wallet
- `location`: Online or In-store
- `transaction_date`: date of purchase
- Enriched fields: `day_of_week`, `is_weekend`, `month`, `year`, `spend_category` (Low/Mid/High, via quantile binning)

---

## 2. Project Objectives

- Clean and prepare the raw dataset for analysis
- Describe location, variance, and distribution of key numeric variables
- Explore relationships between categorical variables (payment method, location, category)
- Visualize revenue and sales patterns over time
- Critically assess whether observed patterns reflect authentic retail behavior

---

## 3. Data Processing and Transformation

### 3.1 Data Cleaning
- Fixed data types (dates parsed to datetime, quantity to nullable integer, discount flag to boolean)
- Standardized column names (lowercase, underscores, no spaces)
- Recovered missing values in `total_spent`, `item`, and `quantity` where recoverable via cross-referencing other columns
- Checked for exact and partial duplicates
- Verified semantic consistency (e.g., `price_per_unit × quantity == total_spent`)
- Identified that `discount_applied` carried no usable information (flagged discounts never actually reduced `total_spent`) and dropped the column
- Applied Z-score outlier detection (threshold = 3 std deviations) on numeric columns

### 3.2 Enrichment
- Extracted `day_of_week`, `is_weekend`, `month`, `year` from `transaction_date`
- Created `spend_category` (Low/Mid/High) via quantile binning of `total_spent`

---

## 4. Exploratory Data Analysis & Visualization

### 4.1 Distributions of Numeric Variables
- Boxplots and histograms (with KDE) for `price_per_unit`, `quantity`, and `total_spent`
- `total_spent` is right-skewed, consistent with it being derived from price × quantity
- `quantity` shows a near-uniform distribution with a sharp spike at 10, suggesting the variable may be capped at that value

### 4.2 Price Distribution by Category
- Faceted histograms comparing `price_per_unit` distribution across all product categories
- Distributions are similar in shape and range across categories, showing little category-specific pricing variation

### 4.3 Revenue Over Time
- Monthly revenue trends across the full dataset timeline
- Year-over-year comparison of revenue by month (grouped bar chart)

### 4.4 Weekday vs. Weekend Spending
- Compared average revenue per day between weekdays and weekends (normalized by actual day counts, not raw totals)

### 4.5 Categorical Relationships
- Cross-tabulations (visualized as heatmaps) exploring:
  - Payment method distribution by category
  - Payment method distribution by location (Online vs. In-store)
  - Spend category (Low/Mid/High) distribution by product category
- Across all these comparisons, distributions were nearly uniform, with no meaningful association between variables

### 4.6 Top-Selling Items
- Ranked top 10 items by units sold and by total revenue generated

---

## 5. Conclusion and Insights

- Numeric variables show expected patterns (right-skewed spend, capped quantity), but categorical relationships (payment method, location, spend tier) show almost no variation across groups.
- This near-uniformity across nearly every relationship tested is atypical of real-world retail data, where payment preferences, category pricing, and spend behavior usually show at least some skew or clustering.
- This pattern suggests the dataset may be synthetically generated rather than reflecting authentic customer behavior, which limits the depth of actionable business insight that can be drawn from it — while still providing a solid basis for demonstrating EDA and visualization technique.

---

## Data & Attribution

This analysis is based on a publicly available retail sales dataset, used here for academic and analytical purposes.
