# 🛍️ Retail Sales Analysis — SQL Project

A structured SQL project that explores **1,997 retail transactions** spanning 2 years (2022–2023) across 3 product categories. The project covers database setup, data cleaning, and business insight generation through analytical queries.

---

## 📁 Table of Contents

- [Database Schema](#-database-schema)
- [Data Exploration](#-data-exploration)
- [Data Cleaning](#-data-cleaning)
- [Analysis Queries](#-analysis-queries)
- [Key Findings](#-key-findings)
- [Data Source](#-data-source)

---

## 🗄️ Database Schema

The project uses a single table — **`retail_sales`**:

| Column | Type | Description |
|---|---|---|
| `transactions_id` | `INT PRIMARY KEY` | Unique transaction identifier |
| `sale_date` | `DATE` | Date of sale |
| `sale_time` | `TIME` | Time of sale |
| `customer_id` | `INT` | Customer identifier |
| `gender` | `VARCHAR(15)` | Customer gender |
| `age` | `INT` | Customer age |
| `category` | `VARCHAR(15)` | Product category |
| `quantity` | `INT` | Units sold |
| `price_per_unit` | `FLOAT` | Price per unit |
| `cogs` | `FLOAT` | Cost of goods sold |
| `total_sale` | `FLOAT` | Total sale amount |

---

## 🔍 Data Exploration

| Metric | Value |
|---|---|
| Total Transactions | 1,997 |
| Unique Customers | 155 |
| Product Categories | 3 (Electronics, Clothing, Beauty) |
| Date Range | Jan 2022 – Dec 2023 |
| Total Revenue | ₹9,11,720 |
| Average Sale Value | ₹456.54 |

---

## 🧹 Data Cleaning

Removed records with NULL values across critical columns:
```sql
DELETE FROM retail_sales
WHERE transactions_id IS NULL
   OR sale_date IS NULL
   OR sale_time IS NULL
   OR gender IS NULL
   OR category IS NULL
   OR quantity IS NULL
   OR cogs IS NULL
   OR total_sale IS NULL;
```

---

## 📊 Analysis Queries

### Q1. Sales on a Specific Date
Retrieved all transactions on `2022-11-05`.

### Q2. Clothing Sales in Nov-2022 (Qty ≥ 4)
Filtered category, month, and quantity together using `TO_CHAR`.

### Q3. Total Sales by Category
| Category | Total Sales |
|---|---|
| Electronics | ₹3,13,810 |
| Clothing | ₹3,11,070 |
| Beauty | ₹2,86,840 |

### Q4. Average Customer Age — Beauty Category
Average age of Beauty buyers: **40.42 years**

### Q5. High-Value Transactions (> ₹1,000)
**306 transactions** exceeded ₹1,000 in total sale value.

### Q6. Transactions by Gender & Category
| Category | Female | Male |
|---|---|---|
| Clothing | 347 | 354 |
| Electronics | 340 | 344 |
| Beauty | 330 | 282 |

### Q7. Best-Selling Month Each Year
Used `RANK()` window function partitioned by year to find peak months by average sales.

### Q8. Top 5 Customers by Total Sales
| Customer ID | Total Sales |
|---|---|
| 3 | ₹38,440 |
| 1 | ₹30,750 |
| 5 | ₹30,405 |
| 2 | ₹25,295 |
| 4 | ₹23,580 |

### Q9. Unique Customers per Category
| Category | Unique Customers |
|---|---|
| Clothing | 149 |
| Electronics | 144 |
| Beauty | 141 |

### Q10. Orders by Time Shift
| Shift | Orders |
|---|---|
| Evening (after 5PM) | 1,062 |
| Morning (before 12PM) | 558 |
| Afternoon (12–5PM) | 377 |

---

## 💡 Key Findings

- **Electronics** leads revenue at ₹3.13L — narrowly ahead of Clothing (₹3.11L)
- **Evening shift drives 53% of all orders** — peak operational hours are post-5PM
- **306 high-value transactions (>₹1,000)** represent premium buying behaviour
- **Beauty category** skews older with an average buyer age of **40 years**
- Gender split is nearly equal across all 3 categories — no strong gender skew

---

## 🛠️ Tools Used

- **PostgreSQL** — querying and analysis
- **Window Functions** — `RANK()`, `PARTITION BY`
- **CTEs** — for shift-based order analysis
- **Aggregate Functions** — `SUM`, `AVG`, `COUNT`, `DISTINCT`

---

## 🗃️ Data Source

📂 Dataset: [Retail Sales Dataset — Kaggle](https://www.kaggle.com/)
