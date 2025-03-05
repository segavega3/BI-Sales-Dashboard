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

### **Gross & Net Sales Overview**
- **Total Gross Sales:** $437,771
- **Total Net Profit:** $36,963
- **Gross Profit:** $75,042
- **Negative Profits:** -$38,079
- **Profit Margin:** **8.44%**
- **Profit Margin by Category (Yearly):**
  - **Clothing:** 9.23%
  - **Furniture:** 8.24%
  - **Electronics:** 7.92%

---

## **Most & Least Profitable Months**

### **Most Profitable Months**
| Month        | Sales ($) | Profit ($) | Orders | % of Total Sales | % of Total Profit |
|-------------|----------|-----------|--------|------------------|------------------|
| **Nov**     | 48,469   | 10,253    | 46     | 11.07%           | 27.74%           |
| **Jan**     | 61,632   | 9,684     | 61     | 14.08%           | 26.2%            |
| **Feb**     | 38,962   | 8,465     | 54     | 8.9%             | 22.9%            |
| **Mar**     | 60,694   | 7,793     | 58     | 13.86%           | 21.08%           |
| **Apr**     | 34,330   | 4,192     | 44     | 7.84%            | 11.34%           |

### **Lowest Profitable Months**
| Month        | Sales ($) | Profit ($) | Orders | % of Total Sales | % of Total Profit |
|-------------|----------|-----------|--------|------------------|------------------|
| **May**     | 29,093   | -3,730    | 31     | 6.65%            | -10.09%          |
| **Jul**     | 12,966   | -2,138    | 31     | 2.96%            | -5.78%           |
| **Dec**     | 37,579   | -1,604    | 41     | 8.58%            | -4.34%           |
| **Sep**     | 27,283   | -1,399    | 30     | 6.23%            | -3.78%           |
| **Jun**     | 23,658   | 420       | 30     | 5.4%             | 1.14%            |

---

## **Statistical Analysis**
- **Median Monthly Sales:** $31,613
- **Standard Deviation of Sales:** $14,396.02

---

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
- **Maharashtra and Madhya Pradesh** experienced the highest number of negative profit orders.
- **Andhra Pradesh had the highest loss per negative order (-$217.75)**, indicating that **specific high-cost products might be underperforming**.
- **Some states with high negative orders still have strong overall profits**, suggesting potential pricing or demand-based losses.

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
1. **Identify the reasons for high negative profits in Q2 and Q3.**  
   - Are specific **products** driving losses?  
   - Were there **pricing errors, discounts, or refunds** impacting margins?  

2. **Analyze why December, despite high sales, had a negative profit margin.**  
   - Were **excessive holiday discounts** the reason?  
   - Did **expensive products underperform** during the season?  

3. **Further investigate states with high negative profit orders.**  
   - Should pricing be adjusted regionally?  
   - Are certain cities consistently unprofitable?  

4. **Compare products sold in profitable months vs. unprofitable months.**  
   - Identify the **best-performing products** and **phase out low-margin items**.
  
5. **Reevaluate Clothing Profitability Across Quarters**
   - Clothing had **negative profits in Q2 and Q3** despite moderate sales, indicating pricing or discounting issues.
   - Consider reducing **markdowns** or identifying **high-cost, low-profit items** within this category.

6. **Leverage Electronics as a High-Performing Category**
   - **Electronics had the highest profits in Q1 and Q4**, suggesting **seasonal demand trends**.
   - Further analyze which **products within Electronics** contributed most to profitability.

7. **Investigate Poor-Performing Product Types**
   - **Phones in Q3 (-$2,114)** and **Electronic Games in Q2 (-$1,711)** saw major losses.
   - Assess whether these products **had high return rates, pricing issues, or seasonal demand declines**.

8. **Identify Pricing Trends for Consistently Profitable Products**
   - **Printers performed well in Q1 and Q4**, showing **consistent profitability**.
   - Consider whether **marketing efforts or price adjustments** contributed to strong sales.

9. **Compare Seasonal Trends in High vs. Low Profitability Products**
   - Investigate whether **high-margin products (Printers, Bookcases) are promoted during profitable quarters**.
   - Analyze whether **low-performing products are being overstocked or discounted too aggressively**.

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

## **Final Insights & Actionable Steps**
1. **Reevaluate Clothing Profitability Across Quarters**
   - Clothing had **negative profits in Q2 and Q3** despite moderate sales, indicating pricing or discounting issues.
   - Consider reducing **markdowns** or identifying **high-cost, low-profit items** within this category.

2. **Leverage Electronics as a High-Performing Category**
   - **Electronics had the highest profits in Q1 and Q4**, suggesting **seasonal demand trends**.
   - Further analyze which **products within Electronics** contributed most to profitability.

3. **Investigate Poor-Performing Product Types**
   - **Phones in Q3 (-$2,114)** and **Electronic Games in Q2 (-$1,711)** saw major losses.
   - Assess whether these products **had high return rates, pricing issues, or seasonal demand declines**.

4. **Identify Pricing Trends for Consistently Profitable Products**
   - **Printers performed well in Q1 and Q4**, showing **consistent profitability**.
   - Consider whether **marketing efforts or price adjustments** contributed to strong sales.

5. **Compare Seasonal Trends in High vs. Low Profitability Products**
   - Investigate whether **high-margin products (Printers, Bookcases) are promoted during profitable quarters**.
   - Analyze whether **low-performing products are being overstocked or discounted too aggressively**.

By implementing these insights, the business can **optimize pricing, improve profitability, and enhance sales strategies** for long-term success.
---

# Category & Product Performance

## Objective
Analyze sales and profitability trends across different product categories and sub-categories to determine which products drive the most revenue and which underperform.

## Business Impact
- **Identifying top-performing categories and products** helps optimize inventory, marketing, and sales strategies.
- **Understanding seasonal and monthly trends** ensures that the right products are promoted at the right time.
- **Detecting consistently unprofitable categories** allows for adjustments in pricing, promotions, or discontinuation of underperforming products.

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



## Objective
Analyze which sub-categories contribute the most to sales and profitability while identifying the least profitable and lowest-selling products. Understand product trends at a monthly and yearly level to optimize product offerings.

## Business Impact
- **Understanding the top-selling product types** allows the business to focus on promoting high-demand items.
- **Identifying unprofitable products** helps optimize inventory, reducing losses and increasing overall profitability.
- **Tracking negative profit trends by product type** allows for potential adjustments in pricing, promotions, or discontinuation.

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
1. **Discontinue or adjust pricing for unprofitable product types.**  
   - **Electronic Games and Phones consistently resulted in losses.**  
   - **Assess if discounts or return rates are causing these losses.**  

2. **Leverage high-performing sub-categories.**  
   - **Printers and Bookcases had high sales and profitability.**  
   - **Increasing inventory or marketing these items could drive further growth.**  

3. **Address negative profit drivers.**  
   - **Sarees had high sales but major losses—analyze if returns or cost structures are the issue.**  
   - **If losses are due to discounts, consider adjusting pricing strategies.**  

4. **Reevaluate inventory for lowest-selling product types.**  
   - **Skirts, Leggings, and Kurti had the lowest sales and profitability.**  
   - **Determine if they should be discontinued or adjusted for higher demand.**  


5. **Electronics drives high revenue but requires profit optimization.**  
   - Examine pricing and return policies to ensure profitability in low-performing months.  
   - Focus on high-margin electronic products like **Printers** instead of loss-generating ones like **Phones**.  

6. **Clothing has strong sales but needs a refined profitability strategy.**  
   - Reduce discounting in historically weak months (**June, September**).  
   - Identify which clothing products contribute most to net profits and prioritize them in marketing efforts.  

7. **Furniture, despite lower sales, maintains stability.**  
   - Consider whether increasing **high-margin furniture items like Bookcases** could improve revenue.  
   - Assess demand elasticity—do customers buy more when prices are reduced?  

8. **Identify why certain months have sharp losses.**  
   - **May, July, and September show the worst losses.**  
   - Further investigation needed into **inventory costs, refund rates, and seasonal demand drops.**  

9. **Expand profitable product lines based on top-performing sub-categories.**  
   - **Printers and Bookcases** generated consistent profits and should be further promoted.  
   - **Loss-making products like Phones and Electronic Games should be reevaluated** to determine if they should be discontinued or repriced.  

