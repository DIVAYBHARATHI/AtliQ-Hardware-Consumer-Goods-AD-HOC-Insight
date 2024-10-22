## Introduction
AtliQ Hardware is a significant player in India's computer hardware scene, with a global presence. They're leveraging data insights to refine their product sales strategy, emphasizing data-driven decisions to drive strategic business growth. 
Task:

1. Check ‘ad-hoc-requests.pdf’ - there are 10 ad hoc requests for which the business needs insights.
2. You need to run a SQL query to answer these requests.
3. The target audience of this dashboard is top-level management - hence you need to create a presentation to show the insights.

This file provides a comprehensive overview of the tables found in the 'gdb023' (atliq_hardware_db) database. It includes information for six main tables:
1. dim_customer: contains customer-related data
2. dim_product: contains product-related data
3. fact_gross_price: contains gross price information for each product
4. fact_manufacturing_cost: contains the cost incurred in the production of each product
5. fact_pre_invoice_deductions: contains pre-invoice deductions information for each product
6. fact_sales_monthly: contains monthly sales data for each product.

**Column Description for dim_customer table:**

1. customer_code: The 'customer_code' column features unique identification codes for every customer in the dataset. These codes can be used to track a customer's sales 		history, demographic information, and other relevant details. For example, the codes could look like '70002017', '90005160', and '80007195' respectively.

2. customer: The 'customer' column lists the names of customers, for example 'Atliq Exclusive', 'Flipkart', and 'Surface Stores' etc.

3. platform: The 'platform' column identifies the means by which a company's products or services are sold. "Brick & Mortar" represents the physical store/location, and 			"E-Commerce" represents online platforms.

4. channel: The 'channel' column reflects the distribution methods used to sell a product. These methods include "Retailers", "Direct", and "Distributors". Retailers 				refer to physical or online stores that sell products to consumers. Direct sales refer to sales made directly to consumers through a company's website or other direct means, and distributors refer to intermediaries or middlemen between the manufacturer and retailer or end consumers.

5. market: The 'market' column lists the countries in which the customer is located.

6. region: The 'region' column categorizes countries according to their geographic location, including "APAC" (Asia Pacific), "EU" (Europe), "NA" (North America), and 			    "LATAM" (Latin America).

7. sub_zone: "The 'sub_zone' column further breaks down the regions into sub-regions, such as "India", "ROA" (Rest of Asia), "ANZ" (Australia and New Zealand), "SE" 				  Southeast Asia), "NE" (Northeast Asia), "NA" (North America), and "LATAM" (Latin America)."


**Column Description for dim_product table:**

1. product_code: The 'product_code' column features unique identification codes for each product, serving as a means to track and distinguish individual products within a 		database or system.

2. division: The 'division' column categorizes products into groups such as "P & A" (Peripherals and Accessories), "N & S" (Network and Storage) and "PC" (Personal 				 Computer).

3. segment: The 'segment' column categorizes products further within the division, such as "Peripherals" (keyboard, mouse, monitor, etc.), "Accessories" (cases, cooling 			solutions, power supplies), "Notebook" (laptops), "Desktop" (desktops, all-in-one PCs, etc), "Storage" (hard disks, SSDs, external storage), and "Networking" (routers, switches, modems, etc.).

4. category: The 'category' column classifies products into specific subcategories within the segment.

5. product: The 'product' column lists the names of individual products, corresponding to the unique identification codes found in the 'product_code' column.

6. variant: The "variant" column classifies products according to their features, prices, and other characteristics. The column includes variants such as "Standard", 				"Plus", "Premium" that represent different versions of the same product.


**Column Description for fact_gross_price table:**

1. product_code: The 'product_code' column features unique identification codes for each product.

2. fiscal_year: The 'fiscal_year' column contains the fiscal period in which the product sale was recorded. A fiscal year is a 12-month period that is used for accounting 			purposes and often differs from the calendar year. For Atliq Hardware, the fiscal year starts in September. The data available in this column covers the 				fiscal years 2020 and 2021.

3. gross_price: The 'gross_price' column holds the initial price of a product, prior to any reductions or taxes. It is the original selling price of the product.

**Column Description for fact_manufacturing_cost:**

1. product_code: The 'product_code' column features unique identification codes for each product

2. cost_year: The "cost_year" column contains the fiscal year in which the product was manufactured.

3. manufacturing_cost: The "manufacturing_cost" column contains the total cost incurred for the production of a product. This cost includes direct costs like
raw materials, labor, and overhead expenses that are directly associated with the production process.

**Column Description for fact_pre_invoice_deductions:**

1. customer_code: The 'customer_code' column features unique identification codes for every customer in the dataset. These codes can be used to track a customer's sales 			history, demographic information, and other relevant details. For example, the codes could look like '70002017', '90005160', and '80007195' respectively.

2. fiscal_year: The "fiscal_year" column holds the fiscal period when the sale of a product occurred.

3. pre_invoice_discount_pct: The "pre_invoice_discount_pct" column contains the percentage of pre-invoice deductions for each product. Pre-invoice deductions are 
discounts that are applied to the gross price of a product before the invoice is generated, and typically applied to large orders or 							     long-term contracts.

**Column Description for fact_sales_monthly:**

1. date: The "date" column contains the date when the sale of a product was made, in a monthly format for 2020 and 2021 fiscal years. This information can be used
to understand the sales performance of products over time.

2. product_code: The "product_code" column contains a unique identification code for each product. This code is used to track and differentiate individual 
products within a database or system.

3. customer_code: The 'customer_code' column features unique identification codes for every customer in the dataset. These codes can be used to track a customer's sales 			history, demographic information, and other relevant details. For example, the codes could look like '70002017', '90005160', and '80007195' respectively.

4. sold_quantity: The "sold_quantity" column contains the number of units of a product that were sold. This information can be used to understand the sales volume ofproducts and to compare the sales volume of different products or variants.

5. fiscal_year: The "fiscal_year" column holds the fiscal period when the sale of a product occurred.


## Ad-Hoc Requests and Solutions
> **1. Provide the list of markets in which customer "Atliq Exclusive" operates its business in the APAC region.**
```
SELECT 
	DISTINCT c.market AS Market,
	ROUND((SUM(g.gross_price * s.sold_quantity))) AS Gross_sales_Amount
FROM dim_customer c
INNER JOIN fact_sales_monthly s ON c.customer_code = s.customer_code
INNER JOIN fact_gross_price g ON g.product_code = s.product_code
WHERE customer = 'Atliq Exclusive' AND region = 'APAC'
GROUP BY 1
ORDER BY 2 DESC;
```
#### Answer 1
![Q1 P1](https://github.com/user-attachments/assets/e84b02e3-795f-42bf-9420-abfae056d274)
![Q1P2](https://github.com/user-attachments/assets/52d687f3-dfbf-4ce2-a7ac-3a4a7637f8bc)



#### Report
![BI 1](https://github.com/user-attachments/assets/d738333d-de54-45c1-b9db-ac7633db9017)




> **2. What is the percentage of unique product increase in 2021 vs. 2020? **
```
SELECT 
	a.p20 as unique_products_2020,
    	b.p21 as unique_products_2021,
	round((p21-p20)*100/p20,2) as percentage_chg
from 
	(
	(SELECT COUNT(DISTINCT product_code) as p20
		FROM fact_manufacturing_cost
		WHERE cost_year = 2020) a,
	(SELECT COUNT(DISTINCT product_code) as p21
		FROM fact_manufacturing_cost
		WHERE cost_year = 2021) b
	 );
```
#### Answer 2
![Q2P1](https://github.com/user-attachments/assets/e77548c1-6c34-44c9-b9a1-8c2543ec2335)


#### Report
![BI 2](https://github.com/user-attachments/assets/3bbbe7ca-4873-40a8-8de0-f7edfa199d71)


 

> **3. Provide a report with all the unique product counts for each segment and sort them in descending order of product counts.**
```
SELECT 
	segment,
    	COUNT(DISTINCT product_code) as product_count
FROM dim_product
GROUP BY segment
ORDER BY 2 DESC;
```
#### Answer 3
![Q3P1](https://github.com/user-attachments/assets/2eda5ab5-ff39-4f8b-8169-743a78f65c59)


#### Report
![BI 3](https://github.com/user-attachments/assets/558dbe5e-a44f-4492-bc6b-16afcc9a8c64)




> **4. Which segment had the most increase in unique products in 2021 vs 2020?**
```
WITH CTE1 AS(
SELECT 
	DISTINCT d.segment, 
    	COUNT(DISTINCT m.product_code) as pc20
FROM dim_product d 
INNER JOIN fact_manufacturing_cost m USING(product_code)
WHERE cost_year = 2020
GROUP BY d.segment
),
CTE2 AS(
SELECT 
	DISTINCT d.segment, 
    	COUNT(DISTINCT m.product_code) as pc21
FROM dim_product d 
INNER JOIN fact_manufacturing_cost m USING(product_code)
WHERE cost_year = 2021
GROUP BY d.segment
)
SELECT 
	CTE1.segment,
	CTE1.pc20 as product_count_2020, 
    	CTE2.pc21 as product_count_2021,
    	(CTE2.pc21-CTE1.pc20) AS difference 
from CTE1,CTE2
WHERE CTE1.segment=CTE2.segment
ORDER BY 4 DESC
LIMIT 1;
```
#### Answer 4
![Q4P1](https://github.com/user-attachments/assets/ea0ff811-38ed-4310-863c-c7ccd7c1792b)


#### Report
![BI 4](https://github.com/user-attachments/assets/390c9f41-b3a1-486e-85ae-81c13dbbac40)


 

> **5. Get the products that have the highest and lowest manufacturing costs.**
```
SELECT 
	m.product_code,
    	p.product,
    	m.manufacturing_cost
FROM dim_product p
INNER JOIN fact_manufacturing_cost m USING(product_code)
WHERE manufacturing_cost = (SELECT MAX(manufacturing_cost) from fact_manufacturing_cost) 
	  OR
      manufacturing_cost = (SELECT MIN(manufacturing_cost) from fact_manufacturing_cost)
ORDER BY 3 DESC;
```
#### Answer 5
![Q5P1](https://github.com/user-attachments/assets/93e488c6-fcde-4184-879e-5396b21e2b48)


#### Report
![BI 5](https://github.com/user-attachments/assets/884214b5-b7e1-42d2-98a2-6a3269493eff)


 

> **6. Generate a report which contains the top 5 customers who received an 
average high pre_invoice_discount_pct for the fiscal year 2021 and in the Indian market.**
```
SELECT 
	i.customer_code,
	c.customer,
    	ROUND(AVG(i.pre_invoice_discount_pct)*100,2) as average_discount_percentage
FROM fact_pre_invoice_deductions i
INNER JOIN  dim_customer c USING(customer_code)
WHERE fiscal_year = 2021 AND market = 'India'
GROUP BY 1,2
ORDER BY 3 DESC
LIMIT 5;
```
#### Answer 6
![Q6P1](https://github.com/user-attachments/assets/655108ca-5231-4094-ac18-afbb7f0a1db6)


#### Report
![BI 6](https://github.com/user-attachments/assets/d3b405f4-0e0b-475b-9b5f-e78e99db9f97)



 
> **7. Get the complete report of the Gross sales amount for the customer “Atliq Exclusive” for each month . 
This analysis helps to get an idea of low and high-performing months and take strategic decisions.**
```
SELECT  
	MONTHNAME(s.date) as `month`,
    	YEAR(s.date) as `year`,
    	CONCAT('$',(ROUND((SUM(g.gross_price * s.sold_quantity))/1000000,2))) AS Gross_sales_Amount
FROM dim_customer c
INNER JOIN fact_sales_monthly s ON c.customer_code = s.customer_code
INNER JOIN fact_gross_price g ON g.product_code = s.product_code
WHERE c.customer='Atliq Exclusive'
GROUP BY s.date
ORDER BY s.date,3;

```
#### Answer 7
![Q7P1](https://github.com/user-attachments/assets/43cdf659-5e48-40d0-aec2-7ff48e9abc7f)





#### Report
![BI 7](https://github.com/user-attachments/assets/394abcb2-0346-4866-8e4b-c2591c590c92)




 > **8. In which quarter of 2020, got the maximum total_sold_quantity?**
```
SELECT 
	CASE
		WHEN MONTH(date) IN (9,10,11) then 'Q1'
		WHEN MONTH(date) IN (12,1,2) then 'Q2'
		WHEN MONTH(date) IN (3,4,5) then 'Q3'
		ELSE 'Q4'
    	END AS Quarters,
    	SUM(sold_quantity) AS total_sold_quantity
FROM fact_sales_monthly
WHERE fiscal_year = 2020
GROUP BY 1
ORDER BY 2 DESC;
```
#### Answer 8
![Q8P1](https://github.com/user-attachments/assets/8d2e6c76-a99e-4991-b8b6-e5b17a320fc1)


#### Report
![BI 8](https://github.com/user-attachments/assets/82c10d9f-72d5-41fa-b9ba-1bcff92b24cf)



> **9. Which channel helped to bring more gross sales in the fiscal year 2021 and the percentage of contribution?**
```
WITH CTE AS (
SELECT 
	c.channel,
	ROUND((SUM(g.gross_price * s.sold_quantity))/1000000,2) AS gross_sales_mln
FROM dim_customer c
INNER JOIN fact_sales_monthly s ON c.customer_code = s.customer_code
INNER JOIN fact_gross_price g ON g.product_code = s.product_code
WHERE s.fiscal_year = 2021
GROUP BY 1
ORDER BY 2 DESC
)
SELECT 
	channel,
	gross_sales_mln,
	round(gross_sales_mln*100/sum(gross_sales_mln) over(),2) AS percentage
FROM cte
GROUP BY 1,2;
```
#### Answer 9
![Q9P1](https://github.com/user-attachments/assets/3ae3da09-3749-42b4-ac94-f183699af797)


#### Report
![BI 9](https://github.com/user-attachments/assets/e01bd50c-17e8-42a1-9f89-a0819a99b49b)




 
> **10. Get the Top 3 products in each division that have a high total_sold_quantity in the fiscal_year 2021?**
```
WITH CTE AS(
SELECT 
	p.division,
    	s.product_code,
    	p.product,
    	SUM(s.sold_quantity) AS total_sold_quantity,
    	DENSE_RANK() OVER(PARTITION BY division ORDER BY SUM(s.sold_quantity) DESC) AS rank_order 
FROM dim_product p
INNER JOIN fact_sales_monthly s USING(product_code)
WHERE fiscal_year = 2021 
GROUP BY 1,2,3 
ORDER BY 4 DESC
)
SELECT 
    	division,
    	product_code,
    	product,
    	total_sold_quantity,
	rank_order 
FROM CTE
WHERE rank_order IN (1,2,3);
```
#### Answer 10
![SQL 10](https://github.com/user-attachments/assets/3f48863e-510b-459a-b354-adc18a473836)


#### Report
![BI 10](https://github.com/user-attachments/assets/a56d9540-aaba-4a16-a349-ff198faa9243)











   





