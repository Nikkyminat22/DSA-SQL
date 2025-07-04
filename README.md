# DSA-SQL
#1. Which product category had the highest sales?
SELECT 
    Product_Category,
    SUM(Sales) AS Total_Sales
FROM KMS
GROUP BY Product_Category
ORDER BY Total_Sales DESC;

#2 What are the Top 3 and Bottom 3 regions in terms of sales?
SELECT TOP 3 
    Region,
    SUM(Sales) AS Total_Sales
FROM KMS
GROUP BY Region
ORDER BY Total_Sales DESC;
# Bottom 3 Regions:
SELECT TOP 3 
    Region,
    SUM(Sales) AS Total_Sales
FROM KMS
GROUP BY Region
ORDER BY Total_Sales ASC;
# What were the total sales of appliances in Ontario?
sql
Copy
Edit
SELECT 
    Province,
    Product_Category,
    SUM(Sales) AS Total_Sales
FROM KMS
WHERE 
    Province = 'Ontario' AND
    Product_Category = 'Appliances'
GROUP BY Province, Product_Category;

# 4. Advice to increase revenue from the bottom 10 customers
SELECT TOP 10 
    Customer_Name,
    SUM(Sales) AS Total_Sales
FROM KMS
GROUP BY Customer_Name
ORDER BY Total_Sales ASC;
# 5 KMS incurred the most shipping cost using which shipping method?
sql
Copy
Edit
SELECT 
    Ship_Mode,
    SUM(Shipping_Cost) AS Total_Shipping_Cost
FROM KMS
GROUP BY Ship_Mode
ORDER BY Total_Shipping_Cost DESC;
#Top 10 Most Valuable Customers
sql
Copy
Edit
SELECT TOP 10 
    Customer_Segment,
    Product_Sub_Category,
    Customer_Name,
    SUM(Sales) AS [Total Sales]
FROM [dbo].[KMS Sql Case Study]
GROUP BY 
    Customer_Segment,
    Product_Sub_Category,
    Customer_Name
ORDER BY [Total Sales] DESC

# 7 Top Small Business Customer by Sales
sql
Copy
Edit
SELECT TOP 1 *
FROM [dbo].[KMS Sql Case Study]
WHERE Customer_Segment = 'small business'
ORDER BY Sales DESC;

# 8 Corporate Customer with the Most Orders
sql
Copy
Edit
SELECT TOP 1 *
FROM [dbo].[KMS Sql Case Study]
WHERE Customer_Segment = 'corporate'
ORDER BY Order_Quantity DESC;

# 9 Most Profitable Consumer Customer
sql
Copy
Edit
SELECT TOP 1 *
FROM [dbo].[KMS Sql Case Study]
WHERE Customer_Segment = 'consumer'
ORDER BY Profit DESC;
#10 Customers Who Returned Items
sql
Copy
Edit
SELECT 
    Customer.Order_ID,
    Customer.Customer_Name,
    Customer.Customer_Segment,
    Customer.Product_Sub_Category,
    Returned.Status
FROM (
    SELECT 
        Order_ID,
        Customer_Segment,
        Product_Sub_Category,
        Customer_Name
    FROM [dbo].[KMS Sql Case Study]
) AS Customer
JOIN (
    SELECT 
        Order_ID,
        Status
    FROM [KMS_DB].[dbo].[Order_Status]
) AS Returned
ON Customer.Order_ID = Returned.Order_ID
ORDER BY Customer.Customer_Name ASC;

