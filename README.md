# BI-Sales-Dashboard
Analyzing Revenue &amp; Profit Trends


# E-commerce Sales Analysis with SQL & Tableau Public

## ASK Phase: Business Problem and Analytical Goals

### Project Objective
This project aims to develop an **interactive Business Intelligence (BI) dashboard** using **Tableau Public** to help an e-commerce business track **sales performance, revenue trends, and customer behavior**.  

By leveraging **SQL for data extraction and transformation** and **Tableau for visualization**, the dashboard will provide **actionable insights** to optimize business strategies.

---

## Stakeholders and Use Cases
### Who Will Use This Dashboard?
| **Stakeholder**    | **Use Case** |
|------------------|-------------|
| **Marketing Team**  | Understand customer segmentation, purchase behavior, and the effectiveness of discounts & promotions. |
| **Sales Team**      | Track revenue, order volume, and top-selling products to drive sales strategies. |
| **Executives & Managers** | Assess financial & operational KPIs to identify risks and inform strategic decision-making. |

---

## Key Business Questions
To support business decisions, the dashboard will address the following questions:

### Sales Performance
- How are sales trending over time?  
- What seasonal or cyclical patterns exist?  

### Product Insights
- Which products and categories generate the **highest revenue and profitability**?  
- Which products are **underperforming**?  

### Customer Behavior
- Who are the **most valuable customers**, and how do their purchasing patterns vary?  

### Promotion Effectiveness
- What impact do **discounts and promotions** have on revenue and profit margins?  

### Regional Sales Trends
- How do different **geographical regions** compare in sales performance?  

---

## Key Performance Indicators (KPIs)
To measure **e-commerce success**, the following KPIs will be tracked:

| **KPI**                  | **Description** |
|------------------------|------------------------------------------------------------|
| **Total Sales Revenue** | Total revenue generated over time. |
| **Number of Orders**    | Total transactions completed within a given period. |
| **Average Order Value (AOV)** | Customer spending behavior (Total Sales / Number of Orders). |
| **Customer Segmentation** | Classification of customers based on purchase frequency & order size. |
| **Top Products & Categories** | Best-selling products driving revenue growth. |

---

## Success Criteria for the Dashboard
A **well-designed Tableau Public dashboard** will be assessed based on:

- **Automated Data Updates**: SQL queries structured for efficient refresh cycles.  
- **Intuitive User Experience**: Interactive filters for date, product category, region, and customer type.  
- **Actionable Insights**: Visualizations that highlight trends, anomalies, and opportunities.  
- **Performance Optimization**: Aggregations structured for smooth performance in Tableau Public.

---

## Dataset Overview
This project uses an **online sales dataset** sourced from **[Kaggle](https://www.kaggle.com/datasets/samruddhi4040/online-sales-data?select=Orders.csv)**.  
It contains **customer orders and transaction details** from **all 12 months of 2018**.

### Dataset Summary
| **Table Name**    | **Rows** | **Description** |
|------------------|---------|----------------|
| **orders**       | 500     | Customer & order metadata (who, when, where). |
| **order_details** | 1500    | Transaction details (what was sold, how much, payment type). |

**License:** CC0: Public Domain  

---

## Database Schema
The dataset follows a **one-to-many relationship** between the `orders` and `order_details` tables:
- **`Order ID`** is the **Primary Key (PK)** in both tables.
- The **`orders` table** contains order **metadata**.
- The **`order_details` table** contains **sales and transaction details**.

### Orders Table
```sql
+---------------+----------+-------------------------------+
| Column Name   | Data Type | Description                 |
+---------------+----------+-------------------------------+
| Order ID      | STRING   | Primary Key, unique order identifier. |
| Order Date    | DATE     | Date the order was placed.  |
| CustomerName  | STRING   | Name of the customer.       |
| State         | STRING   | State where the order was placed. |
| City          | STRING   | City where the order was placed. |
+---------------+----------+-------------------------------+
```
### Orders Table
```sql
+---------------+----------+---------------------------------+
| Column Name   | Data Type | Description                   |
+---------------+----------+---------------------------------+
| Order ID      | STRING   | Foreign Key, links to orders.Order ID. |
| Amount        | INT64    | Total revenue from the order.  |
| Profit        | INT64    | Profit from the order.        |
| Quantity      | INT64    | Number of items purchased.   |
| Category      | STRING   | General product category (Clothing, Electronics, Furniture). |
| Sub-Category  | STRING   | Specific product type within a category. |
| PaymentMode   | STRING   | Payment method (COD, UPI, Debit Card, Credit Card, EMI). |
+---------------+----------+---------------------------------+
```
## Data Exploration & Key Insights

### Orders Table Insights
- **25 distinct cities** across **19 states**.
- **336 unique customers**, with **107 customers appearing more than once**.
- **307 distinct order dates**—further validation required to ensure completeness.
- **500 distinct `Order ID`s**, all present in both tables.

#### Analysis Test:
- How many **distinct `Order ID`s** are associated with the **336 customers**?
- Do duplicate `Order ID`s on the same day indicate **multi-item purchases**?

### Order Details Table Insights
- **3 main product categories**: Clothing, Electronics, Furniture.
- **17 total sub-categories**, distributed as:
  - **Furniture:** 4 sub-categories.
  - **Clothing:** 9 sub-categories.
  - **Electronics:** 4 sub-categories.
- **1500 total order entries but only 500 distinct `Order ID`s**, suggesting multiple items per order.
- **5 payment methods**: COD, UPI, Debit Card, Credit Card, EMI.

#### Analysis Test:
- Validate that **all 500 `Order ID`s in `order_details` match the 500 IDs in `orders`**.

---

## Business Questions & Analytical Focus

### Product & Sales Performance
- Which **sub-categories sell the most** and generate the **highest profit**?
- Which **sub-categories have negative profits**?
- Which **sub-categories have the lowest sales & profit per month**?
- Which **sub-categories have the fewest orders but highest profit**?
- Which **sub-categories have the lowest quantities ordered but highest profit**?

### Geographical Trends
- Which **states & cities generate the most orders, highest sales, and highest profits**?
- Which **states & cities generate the lowest sales and profits**?
- Are **negative profits concentrated in certain states or cities**?
- Does a specific **state/city show a consistent pattern of unprofitability** over multiple months?

---

## Next Steps

### Data Validation & Cleaning
- Ensure all **order date values** are formatted correctly.
- Verify whether **duplicate `Order ID`s reflect multi-item purchases** or data inconsistencies.

### Sales & Profitability Analysis
- Identify **high-performing vs. low-performing products**.
- Investigate **negative profits and potential causes**.

### Geographical & Customer Insights
- Identify **profitable vs. unprofitable locations**.
- Detect **regional sales patterns and seasonal trends**.
