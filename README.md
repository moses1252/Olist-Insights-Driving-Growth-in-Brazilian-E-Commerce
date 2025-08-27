# Brazilian E-Commerce Sales & Logistics Analysis

## Table of Contents

- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning / Preparation](#data-cleaning--preparation)
- [Data Model](#data-model)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Findings](#findings)
- [Recommendations](#recommendations)
- [References](#references)

### Project Overview
This data analysis project explores the public Olist Brazilian E-Commerce dataset using Power Query for data cleaning and transformation, and Power BI for data modeling and creating an interactive dashboard. The goal was to analyze sales performance, evaluate delivery logistics, and assess customer behavior to provide actionable business insights. Key areas analyzed include sales trends by product category and season, on-time delivery rates, and the impact of delivery performance on customer satisfaction.

To simulate a real-world business scenario, I collaborated with ChatGPT acting as a Product Manager to define objectives, KPIs, and reporting requirements. The entire process—from raw data to final dashboard—was completed independently, showcasing my ability to deliver a complete data project from start to finish. This project highlights my proficiency in data engineering, DAX, and building professional-grade dashboards in Power BI.

*<!-- You can upload a screenshot and add the link here -->*

### Data Sources
**olist.zip** – The primary dataset used for this analysis is from Olist, the largest department store in Brazilian marketplaces. The dataset contains information on 100,000 orders from 2016 to 2018 made at multiple marketplaces in Brazil. Its features allow viewing an order from multiple dimensions: order status, price, payment, freight performance, customer location, product attributes, and reviews.

### Tools
- **Power Query / Excel** – Used for the initial ETL process: ingesting 9 separate CSV files, cleaning data, removing duplicates, creating calculated columns, and building a star schema data model.
- **Power BI** – Used for relationship modeling, creating calculated measures with DAX, and designing an interactive dashboard to visualize KPIs, sales trends, and delivery performance.
- **Simulated Stakeholder Collaboration** – Defined business goals, KPIs, and project requirements through a guided, real-world style workflow to ensure the analysis addressed critical business questions.

### Data Cleaning / Preparation

During the data preparation phase, I performed several steps to ensure the dataset was accurate, consistent, and ready for analysis:

1.  **Built a Modular ETL Pipeline:** Created separate "raw" and "clean" queries in Power Query. All original CSV files were loaded as connection-only "raw" queries to preserve the source data. Transformations were applied to create new "clean" fact (`f_*`) and dimension (`dim_*`) tables.
2.  **Standardized Data Types & Removed Duplicates:** Ensured all ID and zip code columns were formatted as Text to preserve leading zeros. Removed duplicates on key columns (e.g., `customer_id`, `product_id`) in dimension tables to ensure clean joins.
3.  **Enriched Datasets with New Columns:**
    -   **In `f_orders`:** Created `order_date`, calculated `delivery_days`, and added a binary `on_time_delivery` flag.
    -   **In `f_order_items`:** Created an `item_revenue` column.
    -   **In `dim_products`:** Merged with a translation table to convert Portuguese category names to English.
4.  **Optimized Large Datasets:** The `geolocation` dataset (over 1M rows) was grouped by zip code prefix and averaged to reduce its size to ~20k rows for better performance, creating `dim_geolocation`.
5.  **Created a Date Table:** Built a `dim_calendar` table for robust time intelligence analysis.

### Data Model
A star schema was implemented in Power BI for efficient analysis. The model centers around the `f_orders` and `f_order_items` fact tables.

**Key Relationships:**
- `f_orders[customer_id]` → `dim_customers[customer_id]`
- `f_order_items[order_id]` → `f_orders[order_id]`
- `f_order_items[product_id]` → `dim_products[product_id]`
- `f_orders[order_date]` → `dim_calendar[date]`
- `dim_customers[customer_zip_code_prefix]` → `dim_geolocation[geolocation_zip_code_prefix]`

*<!-- You can upload a screenshot of your model view here -->*

### Exploratory Data Analysis

During the EDA phase, I explored the dataset to uncover initial patterns:

-   Noticed that a small subset of product categories (`health_beauty`, `watches_gifts`) drove a disproportionate amount of revenue.
-   Discovered a strong seasonal pattern, with sales consistently peaking between March and August.
-   Found that delivery delays had a significant negative correlation with customer review scores.
-   Identified that the state of São Paulo was a notable hotspot for delivery delays.
-   These findings helped guide the KPIs and the structure of the final dashboard.

### Data Analysis

Once KPIs were defined, I created them using DAX in Power BI for interactive filtering:

-   **Total Sales:** R $ 13.5M
-   **Total Orders:** 99K
-   **Average Order Value:** R $ 136
-   **On-Time Delivery Rate:** 89%
-   **Average Review Score:** 4.09 / 5
-   **Delayed Orders:** 11K
-   **Top Categories:** `health_beauty`, `watches_gifts`

All metrics were connected to slicers for dynamic filtering by year, customer type, and delivery status.

### Findings

-   **Customer retention is the largest growth opportunity.** The vast majority of customers (97%) are one-time buyers, indicating a significant challenge with loyalty and repeat purchases.
-   **Delivery performance directly impacts customer satisfaction.** Orders delivered on time average a review score of 4.2, compared to 3.8 for delayed orders—a significant drop that can damage brand reputation.
-   **Logistics issues are geographically concentrated.** The state of São Paulo is a significant hotspot for delivery delays, suggesting regional carrier or infrastructure challenges.
-   **Revenue is highly seasonal.** Sales see a consistent, major peak between March and August, which must be factored into inventory and marketing planning.
-   **Revenue concentration is in lifestyle categories.** The `health_beauty` and `watches_gifts` categories are the top revenue drivers, far outperforming other categories.

### Recommendations
Based on the analysis, I recommend the following actions:

-   **Launch a targeted customer retention program**
    Given the heavy reliance on one-time buyers, implement a loyalty program, targeted newsletters, and exclusive offers to convert new customers into repeat, high-value buyers.

-   **Invest in logistics infrastructure in São Paulo**
    Partner with additional carriers or invest in local warehouse capacity in priority regions to address the root cause of delays and protect customer satisfaction scores.

-   **Implement a proactive recovery process for delayed orders**
    For orders that become delayed, proactively offer discounts, expedited shipping, or other compensations to mitigate negative customer sentiment.

-   **Align inventory with seasonal and category trends**
    Focus marketing budgets and ensure stock availability for the `health_beauty` and `watches_gifts` categories, especially during the high-growth period from March to August.

### References
1.  **Data Source:** [Olist Brazilian E-Commerce Dataset on Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
2.  **Full Project Documentation:** [Google Docs](https://docs.google.com/document/d/1S60ZvomIyd0ilG-7VkKODcn7GMerpiFFOxSPCxJCIr4/edit?usp=sharing)

