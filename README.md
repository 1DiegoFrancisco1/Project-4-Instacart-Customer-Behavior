# 🛒 Project 4 — Instacart Customer Behavior Analysis

Analyze Instacart orders to understand **when** customers shop, **what** they buy, and **how often** they reorder.  
This project focuses on **data cleaning**, **EDA**, and clear **visual storytelling**.

## 🎯 Objectives
1) Preprocess 5 related tables (fix dtypes, handle missing values/duplicates).  
2) Validate time fields and visualize shopping patterns.  
3) Explore order sizes, reorders, and “first-in-cart” behavior.  
4) Deliver business-ready insights supported by charts.

---

## 📂 Data
This project uses five tables derived from Instacart’s public Kaggle dataset (trimmed and with synthetic NA/dupes):

- `orders` — order-level info (`order_id`, `user_id`, `order_dow`, `order_hour_of_day`, `days_since_prior_order`, …)
- `order_products__prior` — products per **prior** order (`order_id`, `product_id`, `add_to_cart_order`, `reordered`)
- `order_products__train` — products per **train** order (same schema as prior)
- `products` — `product_id`, `product_name`, `aisle_id`, `department_id`
- `aisles` / `departments` — lookup tables

> All results/plots are produced in the Jupyter notebook: **`Project 4.ipynb`**.

---

## 🧹 Step 2 — Preprocessing Summary
- **Dtypes**: Casted IDs to `int`, time fields to `int`, ensured booleans where appropriate (`reordered` → `int`/`bool`).
- **Missing values**:
  - `days_since_prior_order`: imputed (e.g., with median or left NA for first orders — decision documented in notebook).
  - Lookups (`product_name`, `aisle`, `department`): dropped rows only if key info missing and non-recoverable.
- **Duplicates**:
  - Removed exact duplicates in order-product tables.
  - Verified uniqueness constraints (`order_id` + `product_id`).
- **Integrity checks**:
  - `order_hour_of_day` within **0–23** ✅
  - `order_dow` within **0–6** ✅

> Rationale: preserve realistic distributions, avoid target leakage, document each decision (see notebook cells).

---

## 📊 Step 3A — Core Time Patterns
- **Orders by hour**: Line/area chart of `order_hour_of_day` → peak shopping times.  
- **Orders by weekday**: Bar chart of `order_dow` → which days are busiest.  
- **Time to next order**: Histogram of `days_since_prior_order` → min/max and mode(s).

**Key observations (fill with your findings):**
- Peak hour(s): **…**  
- Busiest day(s): **…**  
- Typical reorder interval: **…** days; min: **…**, max: **…**

---

## 📊 Step 3B — User & Product Distributions
- **Hour distribution: Wed vs Sat**: overlapped histograms; note shifts in usage patterns.  
- **Orders per customer**: distribution of total order count by `user_id`.  
- **Top-20 most ordered products**: join `order_products*` → `products`; list `product_id` + `product_name`.

**Highlights (fill):**
- Wednesday vs Saturday: **…**  
- Heavy/Light shoppers: **…**  
- Top products: **…** (IDs + names shown in notebook table)

---

## 📊 Step 3C — Basket Size & Reorder Dynamics
- **Items per order**: distribution of `count(product_id)` per `order_id`.  
- **Top-20 most re-ordered items**: rank by times `reordered==1`.  
- **Product-level reorder ratio**:  
  `reorder_rate = (# times product reordered) / (# times product ordered)`  
  Output table: `product_id`, `product_name`, `reorder_rate`.
- **Customer-level reorder ratio**: share of a user’s items that are reorders.  
- **First-in-cart Top-20**: rank by `add_to_cart_order == 1` counts.

**Insights (fill):**
- Median basket size: **…** items.  
- Products with highest reorder rates: **…**  
- First-in-cart favorites: **…** (IDs + names)

---

## 🧠 Business Takeaways
Our initial goal was to identify purchasing patterns in Instacart’s customer base.
We began by loading and cleaning the data to enable reliable exploratory analysis.

We worked with five interconnected tables (orders, products, aisles, departments, and order_products), normalizing data types, filling or removing missing values, and eliminating duplicates to ensure data integrity.

From our analysis, we uncovered key patterns such as peak activity occurring mid-morning and Sundays and Mondays being the most active shopping days.
The interval between orders ranged from 1 day (first order) up to 30 days.

Customer behavior was highly skewed, with most customers placing few orders and a small segment making many.
On average, nearly 50% of items ordered were reorders.

We also identified the top 20 most popular items, the most frequently reordered products, those added first to the cart, and the most common items in large baskets.

These insights can guide data-driven business strategies, such as:

Smart reorder notifications.

Promotions during off-peak hours.

UX improvements tailored to habitual purchase patterns.

Overall, this analysis helps Instacart improve retention, leverage customer loyalty, and optimize marketing campaigns based on real user behavior.
## ▶️ How to Run
```bash
# 1) Create env and install basics
pip install pandas numpy matplotlib seaborn jupyter

# 2) Launch notebook
jupyter notebook "Project 4.ipynb"
