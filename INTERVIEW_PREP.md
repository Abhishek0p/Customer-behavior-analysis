# 🛍️ Customer Shopping Behavior Analysis — Interview Prep

---

## 1. The Elevator Pitch (30 seconds)

> *"I analyzed a dataset of 3,900+ customer shopping records to uncover purchasing patterns. I used Python for EDA, wrote 10 SQL queries covering CTEs and window functions to segment customers into New, Returning, and Loyal cohorts, and built a Power BI dashboard to present insights on revenue by gender, age group, and subscription behavior."*

---

## 2. What We Did (The Project Overview)

| Component | Details |
|---|---|
| **Dataset** | `customer_shopping_behavior.csv` — 3,900+ rows, ~18 columns |
| **Columns** | Customer ID, Age, Gender, Item Purchased, Category, Purchase Amount, Location, Review Rating, Subscription Status, Payment Method, Shipping Type, Discount Applied, Previous Purchases |
| **Tools** | Python (Pandas, Seaborn), PostgreSQL / SQL, Jupyter Notebook, Power BI |
| **Output** | EDA notebook, 10 SQL queries, Power BI dashboard, PDF/PPTX report |

---

## 3. Why We Did It (Business Problem)

**The business question:** *"Who are our customers, what do they buy, and what drives them to spend more?"*

Retail businesses generate massive transaction data but rarely extract structured insights from it. The goal was to:
- Understand which **customer segments** generate the most revenue
- Identify which **products** are top-rated vs. most discounted
- Find out if **subscriptions** or **shipping preferences** affect spend
- Communicate findings to non-technical stakeholders via a dashboard

---

## 4. How We Did It (Technical Walkthrough)

### Step 1 — Exploratory Data Analysis (EDA) with Python
- Loaded `customer_shopping_behavior.csv` using **Pandas**
- Checked data types, nulls, and distributions
- Created visualizations using **Seaborn & Matplotlib**:
  - Revenue distribution by gender and age group
  - Product category breakdown
  - Subscription vs. non-subscription spend comparison
  - Review rating distributions

### Step 2 — SQL Analysis (10 Queries)
Wrote analytical SQL queries that cover the business questions:

| Query | Technique Used |
|---|---|
| Q1. Revenue by gender | `GROUP BY`, `SUM()` |
| Q2. Discount users spending above average | Correlated subquery with `AVG()` |
| Q3. Top 5 products by review rating | `GROUP BY`, `AVG()`, `ORDER BY`, `LIMIT` |
| Q4. Standard vs. Express shipping spend | `WHERE IN`, `AVG()` |
| Q5. Subscribers vs. non-subscribers | `COUNT`, `AVG`, `SUM`, `GROUP BY` |
| Q6. Top 5 products by discount rate | `CASE WHEN`, `SUM`, `GROUP BY` |
| Q7. Customer segmentation (New/Returning/Loyal) | **CTE** + `CASE WHEN` on `previous_purchases` |
| Q8. Top 3 products per category | **CTE** + `ROW_NUMBER() OVER (PARTITION BY category)` |
| Q9. Repeat buyers and subscription likelihood | `WHERE`, `GROUP BY` |
| Q10. Revenue by age group | `GROUP BY`, `SUM`, `ORDER BY` |

**Key SQL Concepts Demonstrated:**
- **CTEs** (`WITH` clause) for readable multi-step queries
- **Window Functions** — `ROW_NUMBER() OVER (PARTITION BY ...)`
- **CASE WHEN** for conditional bucketing/segmentation
- **Correlated Subqueries** for per-row comparisons

### Step 3 — Power BI Dashboard
- Built an interactive dashboard with slicers for Category, Gender, Subscription Status
- Visuals: Revenue by age group (bar), discount impact (pie), review ratings (heatmap)

---

## 5. Key Business Insights Found

1. **Female customers generate slightly higher revenue** than male on average per transaction
2. **Loyal customers (10+ purchases)** account for the majority of total revenue despite being fewer in number
3. **Subscribed customers spend ~15% more** than non-subscribers on average
4. **Blouse, Jewelry, and Pants** are top-rated items consistently across categories
5. **Discounted products** have higher purchase volume but lower average ticket size — a trade-off for the business

---

## 6. Interview Q&A

**Q: "Why did you use CTEs instead of just nested subqueries?"**
> *"CTEs make complex queries readable and maintainable. For the customer segmentation query (Q7 and Q8), the logic had multiple steps — first calculate attributes, then apply filters. A CTE lets you name each step clearly, which is also easier to debug."*

**Q: "How did you define New, Returning, and Loyal?"**
> *"Based on the `previous_purchases` column: 1 purchase = New, 2–10 = Returning, 11+ = Loyal. This is a business assumption — in a real setting, I'd validate these thresholds with stakeholders before hardcoding them."*

**Q: "What was the hardest SQL query to write?"**
> *"Q8 — Top 3 products per category. I needed `ROW_NUMBER() OVER (PARTITION BY category ORDER BY COUNT(customer_id) DESC)` inside a CTE, then filter where `item_rank <= 3`. The tricky part is you can't use a window function in a `WHERE` clause directly, so the CTE wrapping is essential."*

**Q: "What would you do if you had more time?"**
> *"I'd add a time dimension to do cohort analysis — track whether returning customers are growing or declining month over month. I'd also connect the SQL data to Power BI dynamically instead of importing static CSVs."*

---

## 7. Tech Stack Summary

```
Python → Pandas (EDA) → Seaborn/Matplotlib (charts)
SQL    → PostgreSQL (10 queries: CTEs, Window Functions, CASE WHEN)
Power BI → Interactive Dashboard
```
