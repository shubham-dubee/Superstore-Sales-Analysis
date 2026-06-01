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
