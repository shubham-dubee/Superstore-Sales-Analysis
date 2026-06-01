# Superstore Sales & Customer Analysis

## 1. The Goal
I analyzed a retail dataset with 9,800 sales records to answer three main business questions:
* Where are we making the most money?
* What types of products are selling best?
* Are we relying too heavily on just a few big customers to evaluate business concentration risk?

## 2. Tech Stack & Tools Used
* **Excel:** Used Pivot Tables to clean data and group sales by region, category, and market segment.
* **SQL (SQLite in Google Colab):** Wrote advanced queries using Window Functions (`RANK()`, `PARTITION BY`, and `SUM() OVER()`) to rank over 790 unique customers.
* **Dashboard:** Designed a clean visual dashboard layout to present final executive metrics clearly.

## 3. Core Insights
* **Total Sales:** The business generated **$2.26 Million** in total revenue.
* **Top Products:** *Technology* items brought in the most revenue (~$827k), closely followed by *Furniture* (~$728k).
* **Top Location:** The *West* region is our strongest market, bringing in ~$710k. 
* **Low Risk Profile:** Our top customer (*Sean Miller*) spent $25,043, representing only **1.11%** of total revenue. This means our income is safely distributed across a broad consumer base rather than relying heavily on single buyers.

* ## 4. SQL Analysis & Queries
Here are the core SQLite queries I executed within Google Colab to perform advanced customer segmentations:

## 4. SQL Analysis & Queries
Here are the core SQLite queries I executed within Google Colab to perform advanced customer segmentations:

### A. Customer Ranking by Revenue
This query aggregates total sales per customer and ranks them from highest to lowest.
```sql
SELECT 
    "Customer Name",
    SUM(Sales) AS Total_Sales,
    RANK() OVER (ORDER BY SUM(Sales) DESC) AS Customer_Rank
FROM superstore
GROUP BY 1;
```
### B.Top Customer by Region
This query uses a Common Table Expression (CTE) and a window function to find the single highest-spending customer in each geographic region.
```sql
WITH RegionalRanking AS (
    SELECT 
        Region,
        "Customer Name",
        SUM(Sales) AS Total_Sales,
        ROW_NUMBER() OVER (PARTITION BY Region ORDER BY SUM(Sales) DESC) AS rn
    FROM superstore
    GROUP BY 1, 2
)
SELECT Region, "Customer Name", Total_Sales
FROM RegionalRanking
WHERE rn = 1;
```
### C. Customer Revenue Contribution Percentage
This query calculates the exact percentage of global superstore sales contributed by each top customer to evaluate revenue concentration risk.
```sql
SELECT 
    "Customer Name",
    SUM(Sales) AS Total_Sales,
    (SUM(Sales) / SUM(SUM(Sales)) OVER ()) * 100 AS Contribution_Percentage
FROM superstore
GROUP BY 1
ORDER BY Total_Sales DESC
LIMIT 5;
```

