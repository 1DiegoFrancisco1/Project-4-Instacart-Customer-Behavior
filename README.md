# 🛒 Instacart Customer Behavior — Cleaning & Exploratory Data Analysis (Sprint 4)

## 🧭 Project Overview
This project explores **Instacart customer shopping behavior** using a real-world dataset originally released for a Kaggle competition (2017).  
As a data analyst, your goal is to **clean, explore, and visualize** Instacart order data to uncover patterns in purchase times, frequency, and reorder behavior.

---

## 🎯 Objectives
You will:
- Load and clean multiple related tables.
- Handle missing values, duplicates, and data type issues.
- Explore customer behavior patterns such as:
  - Time of day and day of week of orders.
  - Time between consecutive purchases.
  - Most popular and most frequently reordered products.
  - Items most often added first to a cart.
- Present findings visually using clear, labeled plots.

---

## 📦 Dataset Description
The dataset consists of **five CSV tables**, each representing a different layer of Instacart’s transactional data:

| File | Description |
|------|--------------|
| `instacart_orders.csv` | Each row corresponds to a unique order. |
| `products.csv` | Product catalog with category IDs. |
| `order_products.csv` | Line items (products included in each order). |
| `aisles.csv` | Mapping of `aisle_id` to aisle names. |
| `departments.csv` | Mapping of `department_id` to department names. |

### 🗂️ Key Columns

#### instacart_orders.csv
- `order_id`: Unique order identifier  
- `user_id`: Unique customer identifier  
- `order_number`: Number of orders the customer has placed  
- `order_dow`: Day of the week (0 = Sunday)  
- `order_hour_of_day`: Hour the order was placed (0–23)  
- `days_since_prior_order`: Days since the previous order  

#### products.csv
- `product_id`: Unique product identifier  
- `product_name`: Product name  
- `aisle_id`: Aisle category  
- `department_id`: Department category  

#### order_products.csv
- `order_id`: Order identifier  
- `product_id`: Product identifier  
- `add_to_cart_order`: Sequential order items were added to the cart  
- `reordered`: 0 = first time, 1 = product was reordered  

---

## ⚙️ Step-by-Step Workflow

### 🧩 Step 1 – Load & Inspect the Data
Load all five CSVs with `pandas.read_csv()` and check:
- File shapes  
- Missing values  
- Data types (`int`, `float`, `object`)  
- Non-standard delimiters if necessary  

```python
import pandas as pd

orders       = pd.read_csv('/datasets/instacart_orders.csv')
products     = pd.read_csv('/datasets/products.csv')
aisles       = pd.read_csv('/datasets/aisles.csv')
departments  = pd.read_csv('/datasets/departments.csv')
order_items  = pd.read_csv('/datasets/order_products.csv')

orders.info(show_counts=True)
order_items.info(show_counts=True)
