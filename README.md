# Power-BI-Supply-Chain-Dashboard
Supply Chain Sales, Customer, and Shipping Performance Dashboard using Power BI

## Background & Objective 
In today’s competitive supply chain environment, businesses must rely on data-driven insights to optimize performance across sales, customer management, and delivery operations.
This Power BI dashboard was developed to provide a comprehensive end-to-end overview of the supply chain — from sales generation to customer behavior and final shipment delivery.

The project focuses on three major analytical domains:

🛍️ Sales Performance

- To analyze total revenue, profit, profit margin, and total orders. 
- Identify top-performing products that drive sales.
- Track revenue and profit trends over time to uncover seasonal or performance-based patterns.

👥 Customer Insights

- To identify the top customers contributing to revenue, measure their relative impact, and segment customers based on order and revenue behavior.
- This analysis helps understand which customer groups (Consumer, Corporate, or Home Office) are the most valuable and consistent.

🚚 Shipping & Delivery Performance

- To evaluate operational efficiency by measuring delivery timeliness, comparing on-time vs. late deliveries, and analyzing average shipping times across shipping modes.
- It also identifies the most used and fastest shipping methods, helping improve delivery strategy and customer satisfaction.

Overall, the objective of this dashboard is to turn raw supply chain data into actionable insights that empower management to enhance profitability, customer retention, and delivery performance efficiency.

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

All relationships were set to active, except for the Calendar table which has two relationships with the Fact Table—one active (Order Date) and one inactive (Shipping Date), enabling flexibility in time-based analysis when needed.

📌 Modeling Highlights & DAX Logic

Special attention was paid to:

•	Using explicit DAX measures only (no implicit aggregations)

•	Activating time intelligence via Calendar Lookup and functions like DATEADD, TREATAS, and CALCULATE

•	Using dynamic KPIs that adjust based on filters and product selection

•	Handling blanks in visuals using IF(ISBLANK(), 0) or COALESCE() to prevent distortion in KPI cards

Key KPIs modeled include:

| Metric                                          | Description                                                                                |
| ----------------------------------------------- | ------------------------------------------------------------------------------------------ |
|  Total Revenue, Total Profit, Total Orders      | Core financial and volume metrics                                                          |
|  Profit Margin                                  | Calculated using dynamic DAX                                                               |
|  Last Available Month Revenue                   | Adjusts based on latest non-blank sales by filter context                                  |
|  Top Customer by Revenue                        | Extracted using `TOPN` and `MAXX`                                                          |
|  Top Customer Contribution %                    | Shows how dominant the top customer is in total revenue                                    |
|  On-Time Delivery %  vs Late Delivery %         | Calculated from delivery status field                                                      |
|  Delivery Trend Over Time                       | Combines inactive relationship with parameterized visuals (e.g., slicers or chart toggles) |
________________________________________


📌 Handling Time Intelligence and Data Gaps

One key challenge was the presence of many blank values in time-based visuals, especially in recent months where certain products or categories had no recorded sales.

To resolve this, a dynamic DAX measure was introduced to calculate “Last Available Month”, which filters KPIs and visuals to reflect the most recent complete month with actual sales data.
This ensures that KPI cards and trend visuals stay relevant, even if the most recent calendar month has missing values.

---------------------------------------------------------------------------------------------------------------------------

## Executive Summary

This Power BI project delivers a comprehensive view of sales, customer behavior, and shipping performance for a global supply chain business, based on a cleaned dataset of 181K rows spanning from 2015 to 2018.

Across three interactive dashboards—Sales Performance, Customer Insights, and Shipping & Delivery—the analysis reveals critical trends, performance KPIs, and optimization opportunities.

🛍️ Sales Performance Highlights

Total Revenue: $33.05M

Total Orders: 66K

Total Profit: $3.97M

Overall Profit Margin: 12%

 Key insights include:

Revenue and Profit Trends show strong seasonality and a decline in late 2017–2018, possibly due to product lifecycle or market saturation.

Top Performing Categories like Fishing, Cleats, and Camping contributed the most to profit.

Product-Level Performance identified high-selling products with low profit (e.g., Nike Football Cleats) and vice versa, guiding SKU-level pricing strategy.

Last Available Month Revenue dynamically updates based on selection, with comparative metrics to previous months.

👥 Customer Behavior & Segmentation

Total Unique Customers: 21K

Avg Orders per Customer: 3.18

Avg Revenue per Customer: $1.6K

 Behavioral insights:

The Corporate Segment generates the highest revenue share (51.93%) and order volume.

Mary Smith alone accounts for 13% of total revenue, highlighting significant customer concentration risk.

Geographic Analysis across states and countries shows the United States as the primary market, with key states contributing disproportionately to sales.

🚚 Shipping & Delivery Performance

Delivery metrics revealed potential operational inefficiencies:

On-Time Delivery %: 18%

Late Delivery %: 55%

Avg Scheduled Days: 2.93 | Actual Shipping Days: 3.5

 Key findings:

Standard Class is the most frequently used shipping mode, but shows high late delivery rates, impacting overall SLA adherence.

Same Day Delivery has the best on-time performance but is underutilized.

Regional Analysis shows Western Europe and the US West having the highest volume of late deliveries.

-------------------------------------------------------------------------------------------------------------------------------------

## Insights Deep Dive
🛍️ Sales Insights

Total revenue reached $33.05M, with an overall profit margin of 12%.

A sharp decline in revenue and profit occurred at the end of 2017, likely due to seasonal or operational challenges.

Some high-revenue products (e.g., Nike Football Cleats) had relatively low profit, indicating potential pricing or cost issues.

Advanced DAX was used to dynamically calculate KPIs based on the last available month to avoid misleading blanks caused by inactive products.

👥 Customer Insights

The top customer (Mary Smith) contributed 13% of total revenue and made over 7,900 orders, signaling over-reliance on a single customer.
![Top Customers table](

The Consumer segment dominated both order volume and revenue (over 51%), followed by Corporate and Home Office.

Geographical visuals show most customers are based in the United States, with dense clusters in California, Texas, and New York.

🚚 Shipping & Delivery Insights

Only 18% of orders were delivered on time, while 55% were late — highlighting major fulfillment issues.

Standard Class was the most-used shipping method but showed the worst delivery performance after the first class shipping mode.

Average scheduled shipping days (2.93) were consistently lower than actual shipping days (3.5), indicating persistent delays.

-----------------------------------------------------------------------------------------------------------------------------------------------

## Recommendations & Next Steps

🛍️ Sales Optimization

Identify low-value, high-volume products

Use scatter plots or matrix visuals to detect products with high sales volume but low revenue and profit margins. These products typically generate a large number of orders yet contribute little to overall profitability.

Investigating these items can uncover pricing inefficiencies or high cost structures. Consider reviewing pricing strategies or renegotiating supplier terms to improve margins.

👥 Customer Strategy

Reduce over-reliance on top customers

Mary Smith alone contributes over 13% of total revenue. To mitigate risk, implement customer diversification strategies and loyalty programs that incentivize mid-tier customers to increase their share.

Explore untapped segments and regions
The "Home Office" segment has the smallest share of orders and revenue. Similarly, several states have low customer density. 

Consider targeted marketing campaigns or localized promotions to drive growth in underrepresented areas.

🚚 Delivery Improvements

Optimize shipping for performance and speed

While Standard Class is the most used shipping mode, it also shows high delivery delays.

On the other hand, First Class has the worst on-time performance ratio.

A detailed review of carrier partnerships and delivery workflows is needed to boost speed and reliability.

Improve on-time delivery rate

The current on-time delivery rate stands at only 18%.

Prioritize logistics coordination and reduce the gap between scheduled and actual shipping days to improve service levels.
