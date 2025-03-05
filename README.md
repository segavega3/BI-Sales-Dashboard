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




# Sales & Profitability Trends

## Objective
Analyze total sales, net profit, profit margin, and profitability trends across months, states, and quarters to understand overall business performance.

## Business Impact
Understanding profitability trends helps in:
- **Identifying peak and low-performing periods** to adjust sales strategies.
- **Optimizing product pricing and discounting strategies** to reduce negative profits.
- **Recognizing unprofitable regions and months** to mitigate losses and improve marketing allocation.

---

## Key Findings


### **Gross & Net Profit Overview**
| Metric               | Value ($) |
|----------------------|---------|
| **Total Gross Sales** | **$437,771** |
| **Total Gross Profit** | **$75,042** |
| **Total Negative Profit** | **-$38,079** |
| **Net Profit** | **$36,963** |
| **Overall Profit Margin** | **8.44%** |

### **Profit Margin by Category (Yearly)**
| Category   | Profit Margin (%) |
|------------|------------------|
| **Clothing**  | **9.23%** |
| **Furniture** | **8.24%** |
| **Electronics** | **7.92%** |

### **Observations**
- **Clothing has the highest profit margin (9.23%)**, which indicates a **strong revenue-to-cost efficiency ratio**.
- **Electronics, despite high sales, has the lowest profit margin (7.92%)**, possibly due to **lower markup, high returns, or warranty costs**.
- **Negative profits (-$38,079) account for a significant portion of total revenue**, highlighting the need for **better cost control and pricing strategies**.


---

## **Statistical Analysis**
- **Median Monthly Sales:** $31,613
- **Standard Deviation of Sales:** $14,396.02
---

## **Most Profitable Months**
| Month        | Sales ($) | Profit ($) | Orders | % of Total Sales | % of Total Profit |
|-------------|----------|-----------|--------|------------------|------------------|
| **Nov**     | 48,469   | 10,253    | 46     | 11.07%           | 27.74%           |
| **Jan**     | 61,632   | 9,684     | 61     | 14.08%           | 26.2%            |
| **Feb**     | 38,962   | 8,465     | 54     | 8.9%             | 22.9%            |
| **Mar**     | 60,694   | 7,793     | 58     | 13.86%           | 21.08%           |
| **Apr**     | 34,330   | 4,192     | 44     | 7.84%            | 11.34%           |

### **Observations**
- **November was the most profitable month (27.74% of total profit)** despite being **only the fourth-highest in sales**, suggesting:
  - **Premium-priced products or reduced discounting strategies.**
  - **High-margin categories dominated sales** (Electronics and Furniture).
- **January had the highest sales ($61,632) but a lower profit share (26.2%)**, possibly due to:
  - **High holiday discounts or promotional campaigns.**
  - **Increased operational or return costs.**
- **March also had strong sales but lower profitability (21.08%)**, indicating:
  - **A mix of high-selling, low-margin products.**
  - **Potential return/refund issues affecting margins.**
- **April's profit percentage (11.34%) is lower than its sales contribution (7.84%)**, suggesting:
  - **A mix of profitable and unprofitable products.**
  - **Lower discounting compared to other months.**

---

## **Lowest Profitable Months**
| Month        | Sales ($) | Profit ($) | Orders | % of Total Sales | % of Total Profit |
|-------------|----------|-----------|--------|------------------|------------------|
| **May**     | 29,093   | -3,730    | 31     | 6.65%            | -10.09%          |
| **Jul**     | 12,966   | -2,138    | 31     | 2.96%            | -5.78%           |
| **Dec**     | 37,579   | -1,604    | 41     | 8.58%            | -4.34%           |
| **Sep**     | 27,283   | -1,399    | 30     | 6.23%            | -3.78%           |
| **Jun**     | 23,658   | 420       | 30     | 5.4%             | 1.14%            |

### **Observations**
- **May was the least profitable month (-10.09% profit loss)**, suggesting:
  - **Excessive discounting or clearance sales.**
  - **High return rates or defective products.**
- **July had the lowest revenue ($12,966) and a significant loss (-$2,138)**, indicating:
  - **Low seasonal demand.**
  - **A high percentage of low-margin products sold.**
- **December had strong sales but still ended in negative profit (-$1,604)**, suggesting:
  - **Holiday promotions eroded margins.**
  - **Increased operational costs or shipping expenses.**
- **June had minimal profit ($420) despite moderate sales ($23,658)**, meaning:
  - **Profitability was squeezed by potential high costs of goods sold.**
  - **This could indicate a category with high variable costs or increased returns.**

----

## **Comparing Negative vs. Positive Profits**

### **By State**
| State              | Negative Orders | Total Negative Profit ($) | Avg Negative Profit per Order ($) | Positive Orders | Total Positive Profit ($) | Avg Positive Profit per Order ($) |
|-------------------|----------------|----------------------------|----------------------------------|----------------|----------------------------|----------------------------------|
| Maharashtra      | 48             | -9,434                     | -86.55                           | 78             | 16,397                     | 86.3                            |
| Madhya Pradesh  | 53             | -6,991                     | -55.93                           | 70             | 14,373                     | 76.05                           |
| Rajasthan       | 10             | -2,737                     | -152.06                          | 29             | 2,414                      | 43.11                           |
| Andhra Pradesh  | 8              | -2,613                     | -217.75                          | 11             | 2,333                      | 77.77                           |
| Uttar Pradesh   | 13             | -1,954                     | -63.03                           | 23             | 5,312                      | 94.86                           |

### **Observations**
- **Maharashtra had the highest absolute negative profit (-$9,434)** but also the highest **positive profit ($16,397)**, meaning:
  - The state had **high-volume transactions** but a **significant portion of unprofitable orders**.
  - The issue could stem from **high return rates, fraud, or regional pricing strategies**.
- **Madhya Pradesh had a similar pattern**, indicating **regional differences in profitability strategies**.
- **Rajasthan and Andhra Pradesh had significantly lower transaction volumes but still showed negative profitability**, suggesting that:
  - **Operational inefficiencies (e.g., logistics costs) could be affecting profits.**
  - **Product demand in these states may be inconsistent.**

---

### **By Month**
| Month | Negative Orders | Total Negative Profit ($) | Avg Negative Profit per Order ($) | Positive Orders | Total Positive Profit ($) | Avg Positive Profit per Order ($) |
|-------|----------------|----------------------------|----------------------------------|----------------|----------------------------|----------------------------------|
| Jan   | 22             | -2,176                     | -72.53                           | 56             | 11,860                     | 73.21                            |
| Feb   | 12             | -420                       | -24.71                           | 50             | 8,885                      | 72.24                            |
| Mar   | 20             | -2,641                     | -91.07                           | 54             | 10,434                     | 59.28                            |
| May   | 26             | -6,036                     | -70.19                           | 15             | 2,306                      | 72.06                            |
| Jul   | 27             | -3,224                     | -68.6                            | 12             | 1,086                      | 63.88                            |

### **Observations**
- **May had the highest total negative profit (-$6,036), with fewer positive orders.**
- **July had a high number of negative orders, but very few positive ones, indicating a severe business slowdown.**
- **March saw a high average loss per negative order (-$91.07)**, but a reasonable number of profitable orders.

---

### **By Quarter**
| Quarter | Negative Orders | Total Negative Profit ($) | Avg Negative Profit per Order ($) | Positive Orders | Total Positive Profit ($) | Avg Positive Profit per Order ($) |
|---------|----------------|----------------------------|----------------------------------|----------------|----------------------------|----------------------------------|
| Q1      | 54             | -5,237                     | -68.91                           | 160            | 31,179                     | 67.63                            |
| Q2      | 79             | -12,645                    | -60.5                            | 66             | 13,527                     | 121.86                           |
| Q3      | 78             | -11,699                    | -64.99                           | 48             | 10,230                     | 117.59                           |
| Q4      | 37             | -8,498                     | -132.78                          | 123            | 20,106                     | 64.44                            |

### **Observations**
- **Q2 and Q3 saw the highest negative profits ($12,645 and $11,699, respectively), signaling possible issues with seasonal trends.**
- **Q4 had the highest average loss per negative order (-$132.78), indicating large-ticket items selling at a loss.**
- **Q1 had the strongest profit performance, possibly due to strong January sales.**

---

## **Final Insights & Actionable Steps**

### **1. Investigate High Negative Profits in Q2 and Q3**
- Identify **specific products, categories, or discount strategies** contributing to losses.
- Were **pricing errors, excessive markdowns, or refunds** impacting margins?

### **2. Analyze December's Negative Profit Margin Despite High Sales**
- Did **holiday discounts** reduce overall profitability?
- Were **high-cost, low-margin products** disproportionately sold?

### **3. Optimize Clothing Profitability Across Quarters**
- Clothing showed **negative profits in Q2 and Q3** despite moderate sales.
- Consider **reducing markdowns** or adjusting pricing for **high-cost, low-profit items**.

### **4. Leverage Electronics as a High-Performing Category**
- **Electronics had the highest profits in Q1 and Q4**, suggesting **seasonal demand spikes**.
- Further analyze **which specific products contributed most** to profitability.

### **5. Investigate Poor-Performing Product Types**
- **Phones in Q3 (-$2,114)** and **Electronic Games in Q2 (-$1,711)** were major loss drivers.
- Assess whether these items had **high return rates, pricing issues, or seasonal demand declines**.

### **6. Compare Seasonal Trends in High vs. Low Profitability Products**
- Are **high-margin products (Printers, Bookcases)** actively promoted during profitable quarters?
- Are **low-performing products** being **overstocked or discounted too aggressively**?

### **7. Further Investigate States with High Negative Profit Orders**
- Should **regional pricing adjustments** be made?
- Are **certain cities consistently unprofitable**, and why?

### **8. Refine Pricing Strategies Based on Product Performance**
- Identify **consistent best-selling, high-margin products** to prioritize promotions.
- Phase out **low-margin, high-return products** to reduce financial inefficiencies.

---
# Monthly & Quarterly Sales Analysis

## Objective
Analyze monthly and quarterly sales, profits, and order volume to understand performance trends over time. Identify the best and worst performing months and quarters to optimize sales strategies and business operations.

## Business Impact
- **Identifying peak sales months and slow periods** allows for better inventory and marketing planning.
- **Understanding seasonal trends** helps in forecasting demand and preparing for high or low sales periods.
- **Examining profit margins by category and quarter** ensures that pricing strategies align with profitability goals.
- **Detecting loss-generating months** allows businesses to take corrective actions, such as reducing unnecessary discounts or optimizing promotional strategies.

---

## **Key Findings**

### **Best Performing Months (Highest Sales)**
| Month      | Total Sales ($) | Profit ($) | Orders | % of Total Sales | % of Total Profit |
|-----------|----------------|------------|--------|------------------|------------------|
| **Jan**   | 61,632         | 9,684      | 61     | 14.08%           | 26.2%            |
| **Mar**   | 60,694         | 7,793      | 58     | 13.86%           | 21.08%           |
| **Nov**   | 48,469         | 10,253     | 46     | 11.07%           | 27.74%           |
| **Feb**   | 38,962         | 8,465      | 54     | 8.9%             | 22.9%            |
| **Dec**   | 37,579         | -1,604     | 41     | 8.58%            | -4.34%           |

### **Observations**
- **January had the highest total sales, followed closely by March.**  
- **November was the most profitable month** despite being third in total sales, indicating higher-margin products or successful pricing strategies.  
- **December had positive sales but a negative profit margin, suggesting high discounts or refunds.**

---

### **Months with the Most Orders**
| Month      | Total Sales ($) | Profit ($) | Orders | % of Total Sales | % of Total Profit |
|-----------|----------------|------------|--------|------------------|------------------|
| **Jan**   | 61,632         | 9,684      | 61     | 14.08%           | 26.2%            |
| **Mar**   | 60,694         | 7,793      | 58     | 13.86%           | 21.08%           |
| **Feb**   | 38,962         | 8,465      | 54     | 8.9%             | 22.9%            |
| **Nov**   | 48,469         | 10,253     | 46     | 11.07%           | 27.74%           |
| **Apr**   | 34,330         | 4,192      | 44     | 7.84%            | 11.34%           |

### **Observations**
- **January, March, and February also had the highest number of orders, confirming their strong overall performance.**  
- **April had a moderate number of orders but significantly lower sales, indicating smaller order sizes.**  

---

### **Worst Performing Months (Lowest Sales)**
| Month      | Total Sales ($) | Profit ($) | Orders | % of Total Sales | % of Total Profit |
|-----------|----------------|------------|--------|------------------|------------------|
| **Jul**   | 12,966         | -2,138     | 31     | 2.96%            | -5.78%           |
| **Jun**   | 23,658         | 420        | 30     | 5.4%             | 1.14%            |
| **Sep**   | 27,283         | -1,399     | 30     | 6.23%            | -3.78%           |
| **May**   | 29,093         | -3,730     | 31     | 6.65%            | -10.09%          |
| **Apr**   | 34,330         | 4,192      | 44     | 7.84%            | 11.34%           |

### **Observations**
- **July had the lowest sales, and also negative profits, indicating poor performance.**  
- **May and September also showed significant negative profits despite moderate sales volumes.**  
- **June had lower sales but still managed to generate a positive profit margin, indicating cost efficiency.**  

---

## **Quarterly Breakdown: Sales, Profits & Orders**
| Quarter  | Total Sales ($) | Profit ($) | Orders | % of Total Sales | % of Total Profit |
|---------|----------------|------------|--------|------------------|------------------|
| **Q1**  | 161,288        | 25,942     | 173    | 36.84%           | 70.18%           |
| **Q2**  | 87,081         | 882        | 105    | 19.89%           | 2.39%            |
| **Q3**  | 71,741         | -1,469     | 92     | 16.39%           | -3.97%           |
| **Q4**  | 117,661        | 11,608     | 132    | 26.88%           | 31.4%            |

### **Observations**
- **Q1 (January - March) was the strongest quarter, contributing to nearly 37% of total sales and 70% of total profit.**  
- **Q2 and Q3 performed significantly worse in terms of profit, with Q3 generating a net loss.**  
- **Q4 recovered well, but still lagged behind Q1 in overall profitability.**  

---

## **Best & Worst Performing Categories (Sales & Profit) by Quarter**

### **Top Performing Categories by Quarter**
| Quarter  | Category     | Total Sales ($) | Profit ($) | Orders |
|---------|-------------|----------------|------------|--------|
| **Q1**  | Electronics | 61,169         | 11,974     | 73     |
| **Q1**  | Clothing    | 45,941         | 8,763      | 140    |
| **Q2**  | Clothing    | 33,930         | -753       | 82     |
| **Q2**  | Furniture   | 19,873         | 2,691      | 39     |
| **Q3**  | Clothing    | 26,768         | -1,004     | 66     |
| **Q3**  | Furniture   | 21,725         | 1,634      | 34     |
| **Q4**  | Electronics | 48,572         | 4,343      | 50     |

### **Observations**
- **Electronics consistently performed well in Q1 and Q4, suggesting seasonal demand trends.**  
- **Clothing struggled in Q2 and Q3, with negative profits in both quarters, possibly due to discounts or returns.**  
- **Furniture sales remained steady but generated mixed profits across different quarters.**  

---
# Monthly & Quarterly Sales Analysis (Continued)

## **Best & Worst Performing Categories by Profit (Quarterly)**

| Quarter  | Category     | Total Sales ($) | Total Profit ($) | Orders |
|---------|-------------|----------------|----------------|--------|
| **Q1**  | Electronics | 61,169         | 11,974         | 73     |
| **Q1**  | Clothing    | 45,941         | 8,763          | 140    |
| **Q2**  | Furniture   | 19,873         | 2,691          | 39     |
| **Q2**  | Clothing    | 33,930         | -753           | 82     |
| **Q3**  | Furniture   | 21,725         | 1,634          | 34     |
| **Q3**  | Clothing    | 26,768         | -1,004         | 66     |
| **Q4**  | Electronics | 48,572         | 4,343          | 50     |

### **Observations**
- **Electronics had the highest profits in Q1 and Q4, confirming its strong performance in peak sales periods.**
- **Clothing had negative profits in Q2 and Q3, reinforcing concerns about over-discounting or ineffective pricing strategies.**
- **Furniture was more stable, with positive profits in Q2 and Q3, showing resilience compared to clothing.**

---

## **Best & Worst Performing Product Types by Quarter**
| Quarter  | Sub-Category       | Total Profit ($) |
|---------|------------------|----------------|
| **Q1**  | Printers         | 4,888          |
| **Q1**  | Skirt           | -120           |
| **Q2**  | Tables          | 1,758          |
| **Q2**  | Electronic Games | -1,711         |
| **Q3**  | Bookcases       | 2,117          |
| **Q3**  | Phones         | -2,114         |
| **Q4**  | Printers        | 2,791          |
| **Q4**  | Tables         | -838           |

### **Observations**
- **Printers were consistently among the most profitable products, leading in Q1 and Q4.**  
- **Phones had the highest loss in Q3 (-$2,114), indicating potential issues with pricing, returns, or high product costs.**  
- **Electronic Games showed significant losses in Q2 (-$1,711), which may indicate low demand or excessive discounts.**  
- **Tables fluctuated between profit in Q2 and loss in Q4, suggesting inconsistent performance due to demand shifts.**  

---

## **Final Insights & Actionable Steps (Refined & Consolidated)**

### **1. Reevaluate Clothing Profitability Across Quarters**
- Clothing had **negative profits in Q2 and Q3**, despite moderate sales.
- Identify **high-cost, low-margin items** and reconsider **markdown strategies**.

### **2. Leverage Electronics as a High-Performing Category**
- **Electronics had the highest profits in Q1 and Q4**, indicating **seasonal demand trends**.
- Further analyze **which specific products contributed most** to profitability.

### **3. Investigate Poor-Performing Product Types**
- **Phones in Q3 (-$2,114)** and **Electronic Games in Q2 (-$1,711)** were major loss drivers.
- Assess whether these items had **high return rates, pricing issues, or seasonal demand declines**.

### **4. Identify Pricing & Promotion Strategies for Consistently Profitable Products**
- **Printers performed well in Q1 and Q4**, showing **consistent profitability**.
- Consider whether **marketing efforts, discounts, or pricing strategies** contributed to strong sales.

### **5. Compare Seasonal Trends in High vs. Low Profitability Products**
- Are **high-margin products (Printers, Bookcases)** actively promoted during profitable quarters?
- Are **low-performing products** being **overstocked, discounted too aggressively, or suffering from high return rates**?


---

# **Category & Product Performance**

## **Objective**
Analyze sales and profitability trends across different product categories and sub-categories to:
- Identify **top-performing** and **underperforming** products.
- Determine which sub-categories contribute most to **sales and profit** at monthly and yearly levels.
- Uncover **seasonal trends** to optimize inventory and marketing strategies.

## **Business Impact**
1. **Optimize Inventory & Sales Strategies**  
   - Focus on **high-demand, high-margin** products to maximize revenue.  
   - Adjust stock levels based on **seasonal demand patterns**.  

2. **Increase Profitability & Reduce Losses**  
   - Identify **unprofitable products** and evaluate **pricing, promotions, or discontinuation**.  
   - Reduce financial inefficiencies by **minimizing overstock on low-performing items**.  

3. **Improve Promotional & Pricing Strategies**  
   - Align **discounts and marketing efforts** with products that drive the most profit.  
   - Prevent **aggressive discounting** on products with consistently **low margins**.  

4. **Strategic Decision-Making Based on Trends**  
   - Use **monthly and yearly product trends** to refine **sales forecasting**.  
   - Detect **negative profit trends** early to implement corrective measures.  

---

## **Key Findings**

### **Best Performing Categories by Month (Sales & Profit)**

#### **Highest Sales by Category (Monthly)**
| Month      | Category    | Total Sales ($) | Total Profit ($) | Orders |
|-----------|------------|----------------|----------------|--------|
| **Jan**   | Electronics | 26,716         | 4,785          | 28     |
| **Mar**   | Clothing    | 22,175         | 4,770          | 54     |
| **Dec**   | Electronics | 18,560         | -1,856         | 16     |
| **Nov**   | Clothing    | 16,653         | 3,162          | 40     |
| **Feb**   | Furniture   | 16,262         | 2,168          | 21     |

#### **Most Profitable Categories by Month**
| Month      | Category    | Total Sales ($) | Total Profit ($) | Orders |
|-----------|------------|----------------|----------------|--------|
| **Nov**   | Electronics | 16,651         | 3,938          | 18     |
| **Apr**   | Furniture   | 8,121          | 3,151          | 15     |
| **Oct**   | Electronics | 13,361         | 2,261          | 16     |
| **Dec**   | Clothing    | 9,545          | 1,143          | 34     |
| **Sep**   | Furniture   | 8,704          | 1,096          | 10     |

### **Observations**
- **Electronics consistently had the highest sales but was not always the most profitable.**  
- **Clothing saw strong sales in multiple months but had fluctuating profit margins.**  
- **Furniture showed stable profitability but struggled with sales volume.**  
- **December saw high sales but negative profits, reinforcing the likelihood of heavy discounting or return issues.**  

---

## **Worst Performing Categories by Month (Sales & Profit)**

#### **Lowest Sales by Category (Monthly)**
| Month      | Category    | Total Sales ($) | Orders |
|-----------|------------|----------------|--------|
| **Jul**   | Clothing   | 2,981          | 21     |
| **Jun**   | Furniture  | 5,532          | 12     |
| **May**   | Furniture  | 6,220          | 12     |
| **Sep**   | Electronics | 7,207          | 12     |
| **Aug**   | Furniture  | 9,538          | 13     |

#### **Lowest Profit by Category (Monthly)**
| Month      | Category    | Total Profit ($) | Orders |
|-----------|------------|----------------|--------|
| **May**   | Electronics | -2,523         | 14     |
| **Jul**   | Electronics | -1,633         | 10     |
| **Sep**   | Clothing    | -1,585         | 21     |
| **Oct**   | Furniture   | -1,316         | 13     |
| **Jun**   | Clothing    | -544           | 24     |

### **Observations**
- **Electronics had two of the worst-performing months in terms of profit (May and July), despite high sales.**  
- **Clothing had multiple low-profit months, indicating pricing inefficiencies or costly production.**  
- **Furniture had low sales but remained somewhat stable in profitability, showing a possible niche customer base.**  

---

## **Category Sales & Profitability Overview (Yearly)**

#### **Highest Category Sales by Year**
| Category    | Total Sales ($) |
|------------|----------------|
| **Electronics** | 166,267       |
| **Clothing**    | 144,323       |
| **Furniture**   | 127,181       |

#### **Highest Profitable Category by Year**
| Category    | Total Profit ($) |
|------------|----------------|
| **Clothing**    | 13,325        |
| **Electronics** | 13,162        |
| **Furniture**   | 10,476        |

#### **Number of Orders by Category (Yearly)**
| Category    | Number of Orders |
|------------|----------------|
| **Clothing**    | 393            |
| **Electronics** | 204            |
| **Furniture**   | 186            |

### **Observations**
- **Electronics generated the highest total sales but was not the most profitable category.**  
- **Clothing, despite volatility in monthly profits, ended up as the most profitable category for the year.**  
- **Furniture had lower sales but relatively stable profitability.**  
- **Electronics had fewer orders than Clothing but a higher average revenue per order.**  

---

## **Most Profitable Product Types (Top 5 of 17) by Year**
| Sub-Category  | Total Sales ($) | Total Profit ($) | Orders |
|-------------|----------------|----------------|--------|
| **Printers**    | 59,252         | 8,606          | 67     |
| **Bookcases**   | 56,861         | 6,516          | 72     |
| **Saree**       | 59,094         | 4,057          | 156    |
| **Accessories** | 21,728         | 3,353          | 65     |
| **Tables**      | 22,614         | 3,139          | 16     |

### **Observations**
- **Printers were the most profitable product type, outperforming even high-sales clothing items like Sarees.**  
- **Bookcases and Accessories were strong contributors to profit despite lower overall sales.**  
- **Tables, though profitable, had a much lower number of total orders, indicating a niche demand.**  

---

## **Key Findings**

### **Top-Selling Product Types by Year**
| Sub-Category      | Total Sales ($) | Total Profit ($) | Orders |
|------------------|----------------|----------------|--------|
| **Printers**     | 59,252         | 8,606          | 67     |
| **Saree**        | 59,094         | 4,057          | 156    |
| **Bookcases**    | 56,861         | 6,516          | 72     |
| **Phones**       | 46,119         | 1,847          | 71     |
| **Electronic Games** | 39,168         | -644           | 73     |

### **Observations**
- **Printers led in sales and profitability, making them a priority product for future promotions.**  
- **Sarees sold at a similar volume as Printers but had significantly lower profit margins.**  
- **Phones were a strong-selling product, but their profit contribution was much lower than expected.**  
- **Electronic Games ranked among the top-selling products but resulted in a net loss (-$644).**  
  - **Key Question:** Is this a strategic loss for customer retention, or are shipping costs/losses driving the negative profit?  

---

### **Least Profitable Product Types by Year**
| Sub-Category      | Total Sales ($) | Total Profit ($) | Orders |
|------------------|----------------|----------------|--------|
| **Furnishings**  | 13,484         | -806           | 66     |
| **Electronic Games** | 39,168         | -644           | 73     |
| **Kurti**        | 3,361          | -401           | 41     |
| **Skirt**        | 1,946          | -315           | 56     |
| **Leggings**     | 2,106          | -130           | 49     |

### **Observations**
- **Furnishings and Electronic Games had the worst overall profit performances.**  
- **Clothing sub-categories like Skirt, Kurti, and Leggings had low sales and negative profits.**  
  - These may be items that are heavily discounted or have high return rates.  

---

### **Lowest Selling Product Types by Year**
| Sub-Category  | Total Sales ($) | Total Profit ($) | Orders |
|-------------|----------------|----------------|--------|
| **Skirt**   | 1,946          | -315           | 56     |
| **Leggings** | 2,106          | -130           | 49     |
| **Kurti**   | 3,361          | -401           | 41     |
| **T-shirt** | 7,382          | 1,500          | 70     |
| **Shirt**   | 7,555          | 1,513          | 66     |

### **Observations**
- **Skirts and Leggings had the lowest total sales and negative profit margins, making them likely candidates for inventory reduction.**  
- **T-shirts and Shirts had higher sales but relatively lower profits, possibly due to price sensitivity or discounting strategies.**  

---

## **Top-Selling Sub-Category by Month**
| Sub-Category  | Month  | Total Sales ($) | Total Profit ($) | Orders |
|-------------|--------|----------------|----------------|--------|
| **Bookcases**    | Jan    | 15,564         | 2,458          | 18     |
| **Tables**       | Feb    | 6,108          | 427            | 2      |
| **Printers**     | Mar    | 11,799         | 1,846          | 10     |
| **Saree**        | Apr    | 8,401          | -46            | 17     |
| **Phones**       | Jul    | 4,932          | -1,847         | 7      |
| **Printers**     | Nov    | 6,290          | 1,877          | 7      |

### **Observations**
- **Bookcases and Printers were consistently top sellers, generating strong profits.**  
- **Sarees and Phones showed high sales volumes but generated negative profits, requiring further analysis.**  
- **Phones had the most significant negative profit ($-1,847) in July, indicating potential cost issues.**  

---

## **Most Profitable Sub-Categories by Month**
| Sub-Category  | Month  | Total Profit ($) | Total Sales ($) | Orders |
|-------------|--------|----------------|----------------|--------|
| **Bookcases**    | Jan    | 2,458          | 15,564         | 18     |
| **Phones**       | Feb    | 2,254          | 4,688          | 7      |
| **Printers**     | Mar    | 1,846          | 11,799         | 10     |
| **Tables**       | Apr    | 1,864          | 1,364          | 1      |
| **Printers**     | Nov    | 1,877          | 6,290          | 7      |

### **Observations**
- **Bookcases, Phones, and Printers were consistently the most profitable sub-categories.**  
- **Tables had the highest profit in April but with only one order, indicating a high-margin product.**  

---

## **Least Profitable Sub-Categories by Month**
| Sub-Category  | Month  | Total Profit ($) |
|-------------|--------|----------------|
| **Electronic Games** | Mar    | -752           |
| **Saree**           | Jun    | -573           |
| **Phones**          | Jul    | -1,847         |
| **Bookcases**       | Oct    | -1,730         |
| **Phones**          | Dec    | -1,338         |

### **Observations**
- **Electronic Games and Phones had consistent losses across multiple months.**  
- **Sarees generated losses in multiple months despite high sales volume, likely due to returns or high cost per item.**  

---

## **Negative Profit Orders by Product Type**
| Sub-Category      | Total Orders | Negative Profit Orders | Total Profit ($) |
|------------------|--------------|----------------------|----------------|
| **Saree**       | 156          | 73                   | -5,301         |
| **Electronic Games** | 73           | 41                   | -5,275         |
| **Bookcases**    | 72           | 22                   | -4,508         |
| **Printers**     | 67           | 21                   | -3,042         |
| **Chairs**       | 64           | 32                   | -2,979         |

### **Observations**
- **Sarees had the highest number of orders that resulted in negative profits.**  
- **Electronic Games had nearly half of its orders return a loss, suggesting potential pricing or inventory mismanagement.**  
- **Bookcases and Printers, despite being top sellers, still had some negative-profit orders, possibly due to discounting.**  

---

## **Final Insights & Actionable Steps**

### **1. Address Unprofitable Product Types**
- **Electronic Games and Phones consistently resulted in losses.**  
- **Analyze whether discounts, return rates, or cost structures are causing these losses.**  
- **Consider discontinuing or adjusting pricing strategies for these underperforming products.**  

### **2. Leverage High-Performing Sub-Categories**
- **Printers and Bookcases had high sales and profitability.**  
- **Increasing inventory or implementing targeted marketing strategies for these products could drive further growth.**  

### **3. Optimize Profitability for Negative Profit Drivers**
- **Sarees had high sales but significant losses.**  
- **Investigate if losses stem from high return rates, manufacturing costs, or excessive discounting.**  
- **Adjust pricing or promotional strategies accordingly.**  

### **4. Reevaluate Inventory for Low-Selling Products**
- **Skirts, Leggings, and Kurti had the lowest sales and profitability.**  
- **Assess whether these products should be discontinued or repositioned to improve demand.**  

### **5. Improve Electronics Profitability**
- **Electronics drive high revenue but require profit optimization.**  
- **Examine pricing and return policies to ensure profitability in low-performing months.**  
- **Focus on high-margin electronic products like **Printers** rather than loss-generating ones like **Phones**.**  

### **6. Refine Clothing Profitability Strategy**
- **Clothing has strong sales but inconsistent profitability.**  
- **Reduce discounting in historically weak months (**June, September**).**  
- **Identify which clothing products contribute most to net profits and prioritize them in marketing efforts.**  

### **7. Assess Furniture Performance & Pricing**
- **Furniture, despite lower sales, maintains stability.**  
- **Consider expanding high-margin furniture items like **Bookcases** to boost revenue.**  
- **Analyze demand elasticity—do customers buy more when prices are reduced?**  

### **8. Investigate Seasonal Profit Losses**
- **May, July, and September show the worst losses.**  
- **Further analysis is needed on inventory costs, refund rates, and seasonal demand fluctuations.**  

### **9. Expand Profitable Product Lines**
- **Printers and Bookcases consistently generate profits—prioritize their marketing and inventory expansion.**  
- **Loss-making products like Phones and Electronic Games should be reevaluated to determine whether they should be discontinued or repriced.**  
 

----

# Geographical Insights

## **Objective**
To analyze sales and profitability trends across different **cities and states** to identify high-performing and underperforming regions. Understanding geographical performance helps businesses optimize marketing, inventory distribution, and localized pricing strategies.

## **Business Impact**
- Identifying **high-revenue cities** ensures targeted marketing and better stock distribution.
- Recognizing **low-profit regions** helps in **cost-cutting measures** and **potential pricing adjustments**.
- Investigating **negative profit trends by location** can reveal operational inefficiencies.

---

## **Key Findings**

### **Cities & States with the Highest Sales**
| State           | City                  | Total Sales ($) | Total Orders |
|---------------|----------------------|----------------|--------------|
| **Maharashtra**  | **Mumbai**             | 58,886         | 67           |
| **Maharashtra**  | **Pune**               | 43,612         | 27           |
| **Uttar Pradesh** | **Mathura**           | 28,747         | 6            |
| **Madhya Pradesh** | **Bhopal**           | 23,783         | 22           |
| **Delhi**        | **Delhi**              | 22,957         | 24           |

### **Observations**
- **Mumbai & Pune are the strongest sales contributors**, making Maharashtra a key sales hub.
- **Smaller cities like Mathura and Bhopal had significant sales despite fewer orders**, indicating high-value transactions.
- **Delhi and Kolkata performed well in sales, suggesting strong e-commerce adoption in these cities.**

---

### **Cities & States with the Highest Profit**
| State           | City                  | Total Profit ($) | Total Orders |
|---------------|----------------------|----------------|--------------|
| **Madhya Pradesh** | **Indore**           | 6,763          | 71           |
| **Maharashtra**  | **Pune**               | 6,160          | 27           |
| **Uttar Pradesh** | **Mathura**           | 3,335          | 6            |
| **Tamil Nadu**   | **Chennai**            | 2,602          | 8            |
| **Kerala**       | **Thiruvananthapuram**  | 2,435          | 16           |

### **Observations**
- **Indore led in profitability, despite not being the top sales city.**
- **Pune maintained a balance between high sales and profit, reinforcing its importance.**
- **Mathura had a high average profit per order, suggesting premium-priced products were sold here.**
- **Chennai and Thiruvananthapuram performed well in profits but had a low number of total orders, indicating high-margin sales.**

---

### **Cities & States with the Lowest Sales**
| State           | City                  | Total Sales ($) | Total Orders |
|---------------|----------------------|----------------|--------------|
| **Uttar Pradesh** | **Prayagraj**         | 3,889          | 6            |
| **Punjab**       | **Amritsar**           | 4,507          | 9            |
| **Sikkim**       | **Gangtok**            | 5,276          | 12           |
| **Uttar Pradesh** | **Lucknow**           | 5,726          | 13           |
| **Tamil Nadu**   | **Chennai**            | 6,276          | 8            |

### **Observations**
- **Prayagraj, Amritsar, and Gangtok had the lowest sales**, potentially due to limited e-commerce adoption.
- **Chennai had both high profit and low sales, suggesting higher-margin products were sold in fewer transactions.**
- **Lucknow and Surat had mid-range sales but were outperformed by other cities in their respective states.**

---

### **Cities & States with the Lowest Profit**
| State           | City                  | Total Profit ($) | Total Orders |
|---------------|----------------------|----------------|--------------|
| **Andhra Pradesh** | **Hyderabad**       | -280           | 15           |
| **Rajasthan**      | **Jaipur**           | -275           | 19           |
| **Uttar Pradesh**  | **Prayagraj**        | -133           | 6            |
| **Rajasthan**      | **Udaipur**          | -48            | 13           |
| **Nagaland**       | **Kohima**           | 40             | 15           |

### **Observations**
- **Hyderabad and Jaipur had the most significant negative profits**, indicating a need for cost or pricing review.
- **Prayagraj, the lowest-selling city, also ranked among the least profitable, reinforcing its poor performance.**
- **Despite a high number of orders, Jaipur still suffered a net loss.**
- **Udaipur and Kohima had the smallest profit margins, potentially due to high operational costs.**

---

## **Negative Profits Concentrated in Certain Cities**
| State           | City                  | Negative Orders | Total Negative Profit ($) |
|---------------|----------------------|----------------|----------------------|
| **Maharashtra**  | **Mumbai**             | 82             | -7,179               |
| **Madhya Pradesh** | **Indore**           | 97             | -4,832               |
| **Andhra Pradesh** | **Hyderabad**        | 12             | -2,613               |
| **Maharashtra**  | **Pune**               | 27             | -2,255               |
| **Madhya Pradesh** | **Bhopal**           | 28             | -2,159               |

### **Observations**
- **Mumbai, despite being a top sales city, had the highest number of negative-profit orders.**
- **Indore had the second-highest negative profits, despite being the highest-profit city overall.**
- **Hyderabad and Bhopal had fewer negative orders but still had significant losses, requiring further cost analysis.**

---

## **Do Certain Payment Methods Correlate with Negative Profits?**
| Payment Mode | Total Orders | Total Profit ($) | Negative Orders | Negative Profit (%) |
|-------------|-------------|----------------|----------------|--------------------|
| **Credit Card** | 163         | 12,612        | 57             | 34.97%             |
| **COD**        | 684         | 12,547        | 244            | 35.67%             |
| **EMI**        | 120         | 4,824         | 41             | 34.17%             |
| **Debit Card** | 202         | 3,694         | 64             | 31.68%             |
| **UPI**        | 331         | 3,286         | 123            | 37.16%             |

### **Observations**
- **UPI had the highest percentage (37.16%) of negative-profit orders, suggesting issues with refund policies or fraud risks.**
- **COD (Cash on Delivery) had the highest number of negative-profit orders (244), possibly due to cancellations or returns.**
- **Credit Card transactions also showed high negative profit percentages, indicating potential chargebacks or refund issues.**
- **Debit Card and EMI had lower negative profit percentages but still contributed significantly to losses.**

---

## **Final Insights & Actionable Steps**

### **1. Optimize High-Profit Regions**
- **Invest in marketing for high-profit cities like Indore, Pune, and Mathura to increase sales further.**  
- **Analyze key factors driving profitability in these areas and replicate successful strategies in lower-performing cities.**  

### **2. Address Negative Profit Trends**
- **Mumbai and Indore had the highest number of negative-profit orders—further analysis is required.**  
- **Determine if losses stem from returns, excessive discounting, or operational inefficiencies.**  
- **Implement stricter return policies in cities with high refund-related losses.**  

### **3. Evaluate Payment Methods Impacting Negative Profits**
- **UPI and COD transactions should be closely monitored for fraud and high return rates.**  
- **Offer incentives for digital payments (Credit/Debit Card), which have lower refund risks.**  
- **Analyze COD-related losses and consider limiting COD eligibility for high-risk products.**  

### **4. Strategically Address Low-Sales Cities**
- **Prayagraj, Amritsar, and Gangtok recorded the lowest sales and profitability.**  
- **Assess whether to reduce marketing spend or explore targeted promotions to boost sales in these regions.**  

### **Key Takeaway**  
By **focusing on profitable cities, reducing losses from negative-profit transactions, and optimizing regional payment strategies**, the business can **maximize sales while improving overall profitability**.  


------


# Customer & Payment Insights

## **Objective**
To analyze customer purchasing behavior and preferred payment methods to optimize checkout processes, minimize negative profits, and improve overall transaction efficiency.

## **Business Impact**
- Understanding **popular payment methods** helps in **reducing checkout friction** and **optimizing payment processing fees**.
- Analyzing **negative profit trends** by payment type can help in mitigating losses from **refunds, fraud, or cancellations**.
- Evaluating **average order value (AOV)** assists in **upselling strategies** and adjusting **minimum order thresholds**.

---

## **Key Findings**

### **Most Popular Payment Modes**
| Payment Mode  | Percentage of Total Transactions (%) |
|--------------|----------------------------------|
| **COD** (Cash on Delivery)  | **45.6%**  |
| **UPI** (Unified Payments Interface) | **22.07%** |
| **Debit Card**  | **13.47%**  |
| **Credit Card**  | **10.87%**  |
| **EMI** (Equated Monthly Installment)  | **8%**  |

### **Observations**
- **COD is the most preferred payment method (45.6%)**, indicating that many customers prefer to pay upon product delivery.
- **UPI (22.07%) is the second most popular, highlighting the adoption of digital wallets and instant payments.**
- **Credit and Debit Cards combined make up 24.34% of transactions, reflecting the use of direct bank-linked payments.**
- **EMI (8%) is the least used payment option**, suggesting that installment-based payments are not a primary choice for this customer base.

---

### **Average Order Value (AOV)**
| Metric  | Value ($) |
|---------|---------|
| **Average Order Value (AOV)** | **$875.54** |

### **Observations**
- **AOV of $875.54** suggests that customers are making mid-to-high-value purchases.
- **Clothing and Electronics categories drive most of the transactions**, influencing this AOV.
- **This metric can be used to design promotions**, such as **discounts on orders above a certain threshold** to encourage higher spending.

---

### **Number of Orders by Category (Yearly)**
| Category   | Number of Orders |
|------------|----------------|
| **Electronics**  | **204** |
| **Clothing**  | **393** |
| **Furniture**  | **186** |

### **Observations**
- **Clothing had the highest number of orders (393)**, suggesting **frequent repeat purchases**.
- **Electronics had fewer orders (204) but higher individual order value**, likely due to **higher ticket items**.
- **Furniture had the fewest orders (186), possibly due to infrequent purchases or higher price sensitivity.**
- **Segmenting customers by category preference** can help in **targeting personalized marketing efforts**.

---

### **Do Certain Payment Methods Correlate with Negative Profits?**
| Payment Mode  | Total Orders | Total Profit ($) | Negative Profit Orders | Negative Profit (%) |
|--------------|-------------|----------------|----------------|--------------------|
| **Credit Card** | 163 | 12,612 | 57 | 34.97% |
| **COD** | 684 | 12,547 | 244 | 35.67% |
| **EMI** | 120 | 4,824 | 41 | 34.17% |
| **Debit Card** | 202 | 3,694 | 64 | 31.68% |
| **UPI** | 331 | 3,286 | 123 | 37.16% |

### **Observations**
- **UPI transactions had the highest percentage of negative-profit orders (37.16%)**, indicating potential refund or fraud risks.
- **COD transactions had the highest absolute number of negative orders (244)**, confirming risks of order cancellations and returns.
- **Credit Card orders had a 34.97% negative profit rate**, suggesting possible chargebacks or refunds.
- **Debit Card and EMI transactions had relatively lower negative profit percentages**, making them more stable payment options.

---

## **Final Insights & Actionable Steps**

### **1. Optimize Payment Methods to Reduce Losses**
- **Reduce COD dependency** (45.6% of total orders) by offering **incentives for prepaid transactions** (e.g., extra discounts on card/UPI payments).  
- **Analyze refund policies for UPI transactions**, which have the highest negative profit percentage (37.16%).  
- **Encourage EMI options for high-ticket purchases**, as they have lower refund risks.  

### **2. Increase Average Order Value (AOV)**
- **Implement free shipping or discounts for orders above a certain threshold** to encourage higher spending.  
- **Introduce bundled product promotions**, especially in high-revenue categories like **Electronics and Clothing**.  

### **3. Target Marketing Based on Category Preferences**
- **Clothing had the highest order volume**, indicating strong customer engagement—potential for repeat purchases.  
- **Electronics had fewer orders but higher value**, suggesting a focus on **promoting high-ticket tech products**.  
- **Furniture purchases were limited**, signaling possible **price sensitivity or lower purchase frequency**—explore financing or discounts to boost sales.  

### **Key Takeaway**
By **strategically improving payment processes, reducing negative-profit transactions, and optimizing customer purchase behaviors**, the business can **increase revenue while minimizing risk**.  

