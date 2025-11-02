**Quantium Virtual Internship - Retail Data Analytics**

This repository contains the analysis performed as part of the Quantium Data Analytics Virtual Internship. The project focuses on analyzing retail transaction and customer data to understand customer purchasing behavior, identify key trends, and evaluate the impact of a store-level trial.

**Project Overview**

**Objective:**

To leverage transactional and demographic data to uncover insights into chip purchasing habits, assess the performance of specific product/store trials, and provide actionable recommendations.

**Datasets Used:**

QVI_transaction_data.xlsx: Contains detailed transaction-level information, including product details, quantities, and sales.
QVI_purchase_behaviour.csv: Contains customer demographic data, including loyalty card numbers, lifestage, and premium/mainstream/budget segment.


**Part 1: Data Preparation and Exploratory Data Analysis (EDA)**

**Objective & Purpose**

The primary goal of Task 1 was to prepare the raw transaction and customer datasets for analysis. This involved initial data cleaning, handling missing values and outliers, enriching the data with new features, and performing exploratory data analysis to understand overall market trends in the chips category.
How it was Resolved
Data Loading & Initial Inspection: Loaded QVI_transaction_data.xlsx and QVI_purchase_behaviour.csv into Pandas DataFrames. Performed initial checks using data.info(), data.describe(), and data.isnull().sum() to understand data types, distributions, and missing values.
Outlier Handling: Identified and removed a significant outlier in PROD_QTY (a single transaction with 200 units of chips), which would skew aggregated metrics.
**Feature Engineering:**

Extracted PACK_SIZE (e.g., 175g, 150g) from PROD_NAME using regular expressions and converted it to an integer.
Derived BRAND_NAME (e.g., 'Kettle', 'Doritos') from PROD_NAME by taking the first word and standardizing common variations (e.g., 'RRD' to 'Red Rock Deli').
Converted the DATE column in the transaction data to datetime objects for time-series analysis.
Data Merging: Combined the transaction_data and customer_data DataFrames using LYLTY_CARD_NBR (Loyalty Card Number) as the common key, resulting in a comprehensive dataset for further analysis.
Time-Series Analysis & Missing Dates: Aggregated daily sales and identified a missing date (2018-12-25, Christmas Day) where sales were legitimately zero, confirming data integrity after filling.
**Exploratory Data Analysis (EDA):**

Visualized Total Sales Over Time to observe overall trends and confirm data consistency (e.g., Christmas Day dip).
Analyzed Top 10 Pack Sizes by Total Sales using bar charts to identify popular product sizes.
Investigated Top 10 Brands by Total Sales to highlight leading chip brands in terms of revenue.
Examined Total Sales by Lifestage and Premium Customer Segment to understand which demographic groups are the biggest spenders in the chips category.
Key Outcomes & Insights (Task 1)

**Data Quality:** Successfully cleaned and prepared two datasets, handling outliers and standardizing text features.

**Market Snapshot:** Gained a high-level understanding of the chips market, identifying dominant brands (e.g., Kettle, Doritos, Smiths) and popular pack sizes (e.g., 175g, 150g).
Customer Segmentation: Revealed that OLDER FAMILIES (Budget) and YOUNG SINGLES/COUPLES (Mainstream) are the highest-spending customer segments for chips. Other significant segments include RETIREES (Mainstream) and YOUNG FAMILIES (Budget).

**Data Integrity:** Confirmed consistent daily sales patterns, with expected zero sales on major holidays like Christmas.


**Part 2: Store Trial Evaluation**

**Objective & Purpose**

Task 2 aimed to evaluate the effectiveness of a store trial implemented in three specific stores (77, 86, 88). The purpose was to determine if the trial successfully increased sales and customer engagement by comparing their performance against carefully selected "control" stores.
How it was Resolved

**Monthly Performance Metrics:** 

Calculated key monthly metrics for all stores, including Total Sales, Number of Customers, Transactions per Customer, Units per Customer, and Average Price per Unit.

**Pre-Trial Visualization:** Plotted Total Sales and Number of Customers for trial stores during the pre-trial period to establish a baseline and ensure normal behavior before the intervention.

**Control Store Selection:**

Implemented a custom function find_control_store to identify the best control store for each trial store.
Control stores were selected based on the highest Pearson correlation of their TOTAL_SALES trend with the respective trial store's TOTAL_SALES trend during the pre-trial period.
Confirmed selections with visualizations comparing pre-trial trends of trial and chosen control stores.

**Mapping:**

Store 77 & 86 were mapped to Control Store 31, and Store 88 was mapped to Control Store 159.
Scaling Control Store Data: Calculated SALES_FACTOR and CUSTOMERS_FACTOR for each control store relative to its trial store based on pre-trial performance. This allowed for scaled comparison, normalizing for differences in absolute magnitude.

**Trial Period Comparison & Visualization:**

Merged the actual trial store data with the scaled control store data for the entire period (pre, during, post-trial).
Generated line plots comparing Actual Total Sales vs. Scaled Expected Sales and Actual Number of Customers vs. Scaled Expected Customers for each trial-control pair, highlighting the trial period.

**Quantifying Trial Impact:**

Calculated SALES_DIFF_% and CUSTOMERS_DIFF_% during the trial period for each pair, representing the percentage difference between actual trial performance and scaled expected performance.
Analyzed granular metrics like Avg Price Per Unit and Units Per Customer during the trial to understand drivers of change.
Key Outcomes & Insights (Task 2)

Trial Store 77: The trial in Store 77 showed no significant average change in total sales or customer numbers compared to its control store (31).

Trial Store 86: Similarly, Store 86 also recorded no significant average change in total sales or customer numbers against its control store (31).

Trial Store 88: Analysis revealed a significant average decrease in total sales (approx. -24.73%) and customer numbers (approx. -12.29%) in Store 88 compared to its control store (159) during the trial period.

**Overall Conclusion:** The store trial implemented in Stores 77, 86, and 88 was not successful in driving positive increases in sales or customer numbers. Store 88, in particular, saw a notable decline.
Recommendation: The trial strategies need to be re-evaluated. Further investigation is required to understand the specific reasons for underperformance across all trial stores, especially the significant decline in Store 88, before considering any broader rollout or similar initiatives. Customer insights from Task 1 can inform future, more targeted trial designs.
