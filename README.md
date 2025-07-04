# Kultra Mega Stores (KMS) Inventory Data Analysis

### Objective:
Analyze historical sales and customer order data (2009–2012) for Kultra Mega Stores (KMS), supporting the Abuja division. The goal is to extract insights, identify top-performing segments, and offer actionable recommendations to management.

---

## Data Source:
- **Table Name:** `KMS Sql Case Study`
- **Platform:** Microsoft SQL Server
- **Time Period:** 2009 – 2012
- **Key Columns:**
- `Order_ID`, `Customer_Name`, `Customer_Segment`, `Product_Category`, `Product_Sub_Category`, `Sales`, `Profit`, `Region`, `Ship_Mode`, `Shipping_Cost`, `Order_Date`, `Order_Priority`

##  Case Scenario I — Regional, Product, and Cost Insights

###  Product Category with the Highest Sales

### SELECT TOP 1 Product_Category, SUM(Sales) AS [Total Sales]FROM [dbo].[KMS Sql Case Study] GROUP BY Product_Category ORDER BY [Total Sales] DESC
### Technology — ₦5,984,248.18
________________________________________
2️⃣ Top & Bottom 3 Regions by Sales
🔝 Top 3:
sql
CopyEdit
SELECT TOP 3 Region, SUM(Sales) AS [Total Sales]
FROM [dbo].[KMS Sql Case Study]
GROUP BY Region
ORDER BY [Total Sales] DESC
•	West: ₦3,597,549.27
•	Ontario: ₦3,063,212.48
•	Prarie: ₦2,837,304.61
🔻 Bottom 3:
sql
CopyEdit
SELECT TOP 3 Region, SUM(Sales) AS [Total Sales]
FROM [dbo].[KMS Sql Case Study]
GROUP BY Region
ORDER BY [Total Sales] ASC
•	Nunavut: ₦116,376.48
•	Northwest Territories: ₦800,847.33
•	Yukon: ₦975,867.38
________________________________________
3️⃣ Total Sales of Appliances in Ontario
sql
CopyEdit
SELECT SUM(Sales) AS [Total Sales]
FROM [dbo].[KMS Sql Case Study]
WHERE Product_Sub_Category = 'appliances'
AND Region = 'Ontario'
•	💰 ₦202,346.84
________________________________________
4️⃣ Bottom 10 Customers & Recommendations
sql
CopyEdit
SELECT TOP 10 Customer_Name, SUM(Sales) AS [Total Sales]
FROM [dbo].[KMS Sql Case Study1]
GROUP BY Customer_Name
ORDER BY [Total Sales] ASC
Recommendation:
1.	Investigate reasons for low revenue per customer
2.	Collect and act on customer feedback
3.	Provide higher discount margins
4.	Offer personalized product bundles
5.	Promote through ads and loyalty programs
________________________________________
5️⃣ Shipping Method with Highest Cost
sql
CopyEdit
SELECT TOP 1 Ship_Mode, SUM(Shipping_Cost) AS [Total Shipping Cost]
FROM [dbo].[KMS Sql Case Study]
GROUP BY Ship_Mode
ORDER BY [Total Shipping Cost] DESC
•	🚚 Delivery Truck — ₦51,971.94
________________________________________
📁 Case Scenario II — Customer & Segmentation Insights
6️⃣ Most Valuable Customers & Purchases
sql
CopyEdit
SELECT TOP 10 Customer_Name, Product_Category
FROM [KMS Sql Case Study]
ORDER BY Sales DESC
•	Top customers mostly purchased Technology
•	Notable names: Emily Phan, Jasper Cacioppo, Craig Carreira, Valerie Takahito
________________________________________
7️⃣ Highest Spending Small Business Customer
sql
CopyEdit
SELECT TOP 1 Customer_Name, Sales
FROM [KMS Sql Case Study]
WHERE Customer_Segment = 'Small Business'
ORDER BY Sales DESC
•	🏅 Dennis Kane — ₦33,367.85
________________________________________
8️⃣ Corporate Customer with Most Orders (2009–2012)
sql
CopyEdit
SELECT TOP 1 Customer_Name, COUNT(Order_ID) AS Total_Orders
FROM [KMS Sql Case Study]
WHERE Order_Date BETWEEN '2009-01-01' AND '2012-12-31'
AND Customer_Segment = 'Corporate'
GROUP BY Customer_Name
ORDER BY Total_Orders DESC
•	📦 Adam Hart — 27 Orders
________________________________________
9️⃣ Most Profitable Consumer Customer
sql
CopyEdit
SELECT TOP 1 Customer_Name, SUM(Sales) AS Total_Revenue, SUM(Profit) AS Total_Profit
FROM [KMS Sql Case Study1]
WHERE Customer_Segment = 'Consumer'
GROUP BY Customer_Name
ORDER BY Total_Profit DESC
•	💼 Emily Phan — ₦34,005.44 Profit
________________________________________
🔟 Customers Who Returned Items
sql
CopyEdit
SELECT DISTINCT Customer_Name, Customer_Segment
FROM [KMS Sql Case Study]
WHERE Order_ID = ANY (
  SELECT Order_ID
  FROM Order_Status
  WHERE Status = 'Returned'
)
•	Returned orders span across all segments: Consumer, Corporate, Small Business.
________________________________________
1️⃣1️⃣ Shipping Cost vs Order Priority
sql
CopyEdit
SELECT Order_Priority, Ship_Mode, COUNT(*) AS No_Of_Priority,
       SUM(Sales - Profit) AS Estimated_Shipping_Cost,
       AVG(DATEDIFF(DAY, Order_Date, Ship_Date)) AS AvgShipDays
FROM [dbo].[KMS Sql Case Study]
GROUP BY Order_Priority, Ship_Mode
ORDER BY Order_Priority
📝 Conclusion:
❌ Shipping costs were not aligned with order priorities.
High-priority orders were not consistently shipped via faster methods (e.g. Express Air), and low-priority orders used costly shipping options.
📌 Recommendation: Optimize shipping mode selection based on both cost and urgency to improve efficiency.
________________________________________
✅ Final Recommendations:
•	Align shipping methods with order priorities
•	Focus promotions on low-revenue regions and customers
•	Personalize product offerings for top buyers
•	Leverage Technology category trends
•	Improve return handling and customer satisfaction
________________________________________
📎 Project Files:
text
CopyEdit
📁 KMS-Case-Study/
├── 📄 KMS_SQL_Case_Study.sql
├── 📄 KMS_Data.xlsx
├── 📄 README.md (this file)
├── 📊 Dashboard.pbix (Power BI Dashboard)
└── 📄 KMS_Final_Report.pdf
________________________________________
🔧 Tools Used:
•	SQL Server Management Studio (SSMS)
•	Microsoft Excel
•	Power BI (Optional for visualization)

