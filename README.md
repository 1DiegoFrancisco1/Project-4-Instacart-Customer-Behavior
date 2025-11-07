# 🛒 Instacart Customer Behavior — Cleaning & EDA (Sprint 4)

**Goal:** Clean and analyze Instacart order data to understand customer shopping habits (time of day, day of week, reorder behavior, basket size) and communicate insights with clear visuals.

---

## 📦 Dataset (5 Tables)

- `instacart_orders.csv` — orders (one row per order)  
- `products.csv` — product catalog  
- `order_products.csv` — line items (products within each order)  
- `aisles.csv` — aisle dictionary  
- `departments.csv` — department dictionary  

### Key Fields
- `order_id`, `user_id`, `order_number`, `order_dow (0–6)`, `order_hour_of_day (0–23)`, `days_since_prior_order`
- `product_id`, `product_name`, `aisle_id`, `department_id`
- `add_to_cart_order`, `reordered (0/1)`

> 💡 This dataset is a curated version of the 2017 Instacart Kaggle dataset. It includes intentional **missing values** and **duplicates** to practice data cleaning.

---

## 🧭 Project Tasks

### 1️⃣ Load & Inspect
- Read all CSVs carefully (check delimiters and encoding if necessary).  
- Explore dataset shapes, dtypes, and missing values.  
- Use `info(show_counts=True)` for large DataFrames.  

```python
import pandas as pd

orders       = pd.read_csv('/datasets/instacart_orders.csv')
products     = pd.read_csv('/datasets/products.csv')
aisles       = pd.read_csv('/datasets/aisles.csv')
departments  = pd.read_csv('/datasets/departments.csv')
order_items  = pd.read_csv('/datasets/order_products.csv')

orders.info(show_counts=True)
order_items.info(show_counts=True)
