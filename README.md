# E-Commerce Customer Intelligence

Customer analytics on roughly 100k real orders from a Brazilian online marketplace: data quality checks, customer spending, and purchase-frequency analysis in Python.

> 🚧 Work in progress. This repo covers **step 1: data understanding**. Segmentation and further analysis come next.

## Problem

An e-commerce business needs to know **who its customers are, how much they spend, and how often they come back** before it can plan retention or marketing. This project builds that foundation from raw order data.

## Data

[Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) (Sep 2016 – Oct 2018):

| File | Rows | Content |
|---|---|---|
| `olist_orders_dataset.csv` | 99,441 | order status and purchase/delivery timestamps |
| `olist_customers_dataset.csv` | 99,441 | customer IDs and location |
| `olist_order_items_dataset.csv` | 112,650 | products, sellers, price, freight |

## Approach

1. **Data quality:** checked structure, missing values (for example 2,965 orders with no delivery date, mostly undelivered or canceled), duplicates (none) and order-status distribution.
2. **Datetime handling:** converted 5 timestamp columns and validated the date range.
3. **Relationship validation:** confirmed referential integrity between orders, customers and items. All keys match.
4. **Merging:** joined the three tables into one order-item dataset (113,425 × 18).
5. **Customer spending:** total product spend per unique customer (delivered orders only, freight excluded).
6. **Purchase frequency:** compared one-time vs. repeat customers.

## Key findings

- **93,358 customers** analyzed, with **R$13.2M** in total product sales.
- **Only 3.0% of customers come back** (2,801 repeat customers vs. 90,557 one-time buyers).
- Repeat customers spend almost **twice as much** on average (**R$260** vs. **R$138**).
- **Big spenders aren't necessarily loyal:** 9 of the top 10 spenders placed a single order.

Low retention combined with the much higher value of returning customers points to a clear business opportunity in retention.

## Tech stack

Python · Pandas · Matplotlib · Jupyter

## How to run

```bash
git clone https://github.com/abdallahmede/Ecommerce-Customer-Intelligence.git
cd Ecommerce-Customer-Intelligence
pip install -r requirements.txt
jupyter notebook notebooks/01_data_understanding.ipynb
```

Put the Olist CSV files in the `data/` folder (download them from Kaggle).

## Next steps

- RFM segmentation (Recency, Frequency, Monetary)
- Delivery-time analysis and its impact on customer behaviour
- Regional analysis by customer state
