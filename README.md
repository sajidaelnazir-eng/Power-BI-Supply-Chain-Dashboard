# Power-BI-Supply-Chain-Dashboard
Supply Chain Sales, Customer, and Shipping Performance Dashboard using Power BI

## Background & Objective 

This Power BI dashboard provides an end-to-end view of supply chain performance, covering sales generation, customer behavior, and shipment delivery.

The objective is to answer practical business questions around revenue, profitability, customer value, and delivery efficiency—and highlight where performance gaps exist across the supply chain.

The analysis focuses on three areas:

Sales Performance: revenue, profit, margin, and product-level performance to identify profit drivers and leakage.

Customer Insights: customer contribution, segmentation, and concentration to understand value and risk.

Shipping & Delivery Performance: on-time delivery, delays, and shipping mode efficiency to evaluate operational reliability.

Overall, the dashboard is designed to support data-driven decision-making by turning raw supply chain data into clear, actionable insights.

-----------------------------------------------------------------------------------------------------------------------------------------

## Data Structure Overview & Modeling

📌 Dataset  Summary

The original dataset contained over 180,000+ rows. It covers sales, customer behavior, product details, and shipping performance across a multinational supply chain between 2015 and 2018.
However, it was initially structured as a flat, denormalized table with duplicated fields, missing values, and inconsistent formatting.
To enable efficient analysis and improve performance, the data was thoroughly cleaned: duplicates were removed, missing values handled, and unnecessary columns excluded.

The final model retained only the relevant fields required for KPIs, filtering, and visualization logic. Key information includes: 

•	Sales Transactions: Order ID, Order Date, Revenue, Profit, Quantity, ...etc

•	Customer Details: Full Name, Segment, Country, State, ...etc

•	Product Info: Product Name, Category, Unit Price, Discount Rate, ...etc

•	Shipping Details: Ship Mode, Scheduled vs Actual Days, Delivery Status, ..etc

•	Geographical Attributes: Country, State, City, Region

📌 Data Cleaning and Transformation

The original flat table was manually decomposed into a star schema, ensuring better structure and scalability. Key transformation steps included:

•	Dropping irrelevant/redundant columns (e.g., Product Image, Order Zipcode, Department Info)

•	Renaming columns for clarity (e.g., “Benefit per Order” → “Profit”)

•	Fixing data types (e.g., Currency, Decimal, DateTime)

•	Handling blanks and missing values, especially for product-level sales gaps in later months

•	Creating calculated columns and measures via DAX, including:
	Profit Margin, Total Orders, Total Revenue, Last Available Month Revenue, Previous Month Orders, Top Customer by Revenue and their Contribution %, On-Time Delivery % & Late Delivery %

All data cleaning and reshaping was done through Power Query Editor, before loading into Power BI’s semantic layer.

📌 Data Modeling: Fact and Dimension Structure

The cleaned dataset was restructured into a star schema to improve performance and maintain clarity.
It consists of a central Fact Table (Orders Data) that holds transactional metrics such as revenue, profit, quantity, discount, and shipping times. This fact table is connected to several dimension tables, including:

•	Products Lookup

•	Customers Lookup

•	Category Lookup

•	Location Lookup

•	Calendar Lookup

•	Department Lookup (included in schema, but not used in visualizations)

All relationships were set to active, except for the Calendar table which has two relationships with the Fact Table, one active (Order Date) and one inactive (Shipping Date), enabling flexibility in time-based analysis when needed.

📌 Modeling Highlights & DAX Logic

Special attention was paid to:

•	Using explicit DAX measures only (no implicit aggregations)

•	Activating time intelligence via Calendar Lookup and functions like DATEADD, TREATAS, and CALCULATE

•	Using dynamic KPIs that adjust based on filters and product selection

•	Handling blanks in visuals using IF(ISBLANK(), 0) or COALESCE() to prevent distortion in KPI cards

Key KPIs modeled include:

Total Revenue, Total Profit, Total Orders, Profit Margin (%), Last Available Month Revenue, Top Customer by Revenue
, Top Customer Contribution % , On-Time Delivery %, Late Delivery %,  Delivery Trend Over Time.
________________________________________


📌 Handling Time Intelligence and Data Gaps

One key challenge was the presence of many blank values in time-based visuals, especially in recent months where certain products or categories had no recorded sales.

To resolve this, a dynamic DAX measure was introduced to calculate “Last Available Month”, which filters KPIs and visuals to reflect the most recent complete month with actual sales data.
This ensures that KPI cards and trend visuals stay relevant, even if the most recent calendar month has missing values.

---------------------------------------------------------------------------------------------------------------------------

## Executive Summary

This project analyzes sales, customer behavior, and shipping performance using a cleaned dataset of 181K transactions from 2015 to 2018. The goal is to assess profitability, customer value, and delivery efficiency across the supply chain.

Sales analysis shows total revenue of $33.05M with an overall profit margin of 12%. While several product categories generate high sales volume, some high-selling products contribute disproportionately low profit, indicating margin inefficiencies at the SKU level.

Customer analysis identifies 21K unique customers, with the Corporate segment generating the largest share of revenue. However, a single customer contributes 13% of total revenue, highlighting a potential concentration risk that could impact revenue stability.

Delivery performance reveals operational challenges, with only 18% of orders delivered on time and 55% delivered late. Standard Class shipping, despite being the most used mode, shows high delay rates, suggesting misalignment between shipping strategy and service performance.

Overall, the analysis highlights clear opportunities to improve profit margins, reduce customer dependency risk, and optimize shipping operations to enhance service levels and customer satisfaction.

-------------------------------------------------------------------------------------------------------------------------------------

## Insights Deep Dive
🛍️ Sales Insights

- Total revenue reached $33.05M, with an overall profit margin of 12%.

- A sharp decline in revenue and profit occurred at the end of 2017, likely due to seasonal or operational challenges.

![Revenue trending cgart](https://github.com/sajidaelnazir-eng/Power-BI-Supply-Chain-Dashboard/blob/main/Revenue%20trending%20over%20time%20line%20chart.png?raw=true)

![Profit trending chart](https://github.com/sajidaelnazir-eng/Power-BI-Supply-Chain-Dashboard/blob/main/Profit%20trending%20over%20time%20line%20chart.png?raw=true)

- Some high-volume, low-margin products show signs of inefficiency. For instance:

Nike Football Cleats received 18,783 orders but generated only $12K profit, representing a 2.4% profit margin.

- Advanced DAX was used to dynamically calculate KPIs based on the last available month to avoid misleading blanks caused by inactive products.

👥 Customer Insights

- The top customer (Mary Smith) contributed 13% of total revenue and made over 7,900 orders, signaling over-reliance on a single customer.

![Top Customers table](https://github.com/sajidaelnazir-eng/Power-BI-Supply-Chain-Dashboard/blob/main/Customer%20insights%20(Top%20customers%20table).png?raw=true)

- The Consumer segment dominated both order volume and revenue (over 51%), followed by Corporate and Home Office.

![customer segment](https://github.com/sajidaelnazir-eng/Power-BI-Supply-Chain-Dashboard/blob/main/Orders%20and%20Revenue%20by%20customer%20segment.png?raw=true)

- Geographical visuals show most customers are based in the United States, with dense clusters in California, Texas, and New York.

![customer distribution map](https://github.com/sajidaelnazir-eng/Power-BI-Supply-Chain-Dashboard/blob/main/Customers%20distribution%20map.png?raw=true)

🚚 Shipping & Delivery Insights

- Only 18% of orders were delivered on time, while 55% were late, highlighting major fulfillment issues.

- Average scheduled shipping days (2.93) were consistently lower than actual shipping days (3.5), indicating persistent delays.

- Standard Class was the most-used shipping method but showed the worst delivery performance after the first class shipping mode.

![Delivery Performance chart](https://github.com/sajidaelnazir-eng/Power-BI-Supply-Chain-Dashboard/blob/main/Delivery%20Performance%20bar%20chart.png?raw=true)


-----------------------------------------------------------------------------------------------------------------------------------------------

## Recommendations & Next Steps

🛍️ Sales Optimization

- Identify low-value, high-volume products

- Use scatter plots or matrix visuals to detect products with high sales volume but low revenue and profit margins. These products typically generate a large number of orders yet contribute little to overall profitability.

- Investigating these items can uncover pricing inefficiencies or high cost structures. Consider reviewing pricing strategies or renegotiating supplier terms to improve margins.

👥 Customer Strategy

- Reduce over-reliance on top customers

Mary Smith alone contributes over 13% of total revenue. To mitigate risk, implement customer diversification strategies and loyalty programs that incentivize mid-tier customers to increase their share.

- Explore untapped segments and regions
  
The "Home Office" segment has the smallest share of orders and revenue. Similarly, several states have low customer density. 

- Consider targeted marketing campaigns or localized promotions to drive growth in underrepresented areas.

🚚 Delivery Improvements

- Optimize shipping for performance and speed

  While Standard Class is the most used shipping mode, it also shows high delivery delays.

 On the other hand, First Class has the worst on-time performance ratio.

- A detailed review of carrier partnerships and delivery workflows is needed to boost speed and reliability.

- Improve on-time delivery rate. The current on-time delivery rate stands at only 18%.

- Prioritize logistics coordination and reduce the gap between scheduled and actual shipping days to improve service levels.


👉 [Full interactive dashboards will be available soon on GitHub Pages.]

