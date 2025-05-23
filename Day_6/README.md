# 📊 SQL Sales Trend Analysis – Auto Sales Data

## 🧾 Overview
This project focuses on analyzing sales trends using SQL queries. The dataset contains Auto sales data including order dates, customer information, product details, and sales amounts. The analysis is done using **MySQL**, with insights drawn through aggregation and filtering techniques.

---

## 📁 Dataset
**Filename:** `auto_sales_data.csv`  
The dataset contains the following columns:
- `ORDERNUMBER`
- `QUANTITYORDERED`
- `PRICEEACH`
- `ORDERLINENUMBER`
- `SALES`
- `ORDERDATAE` (Format: `DD/MM/YYYY`)
- `DAYS_SINCE_LASTORDER`
- `STATUS`
- `PRODUCTLINE`
- `MSRP`
- `PRODUCTCODE`
- `CUSTOMERNAME`
- `PHONE`
- `ADDRESSLINE1`
- `CITY`
- `POSTALCODE`
- `COUNTRY`
- `CONTACTLASTNAME`
- `CONTACTFIRSTNAME`
- `DEALSIZE`

---

## 🔍 SQL Queries & Insights

#1. TOTAL SALES BY COUNTRY --

`SELECT COUNTRY, SUM(SALES) AS TOTAL_SALES FROM `auto sales data` GROUP BY COUNTRY ORDER BY TOTAL_SALES DESC;`



#2.  TOP 5 CUSTOMERS BY REVENUE
`SELECT  CUSTOMERNAME, ROUND(SUM(SALES),2) AS TOTAL_SPENT FROM  `auto sales data` GROUP BY CUSTOMERNAME ORDER BY TOTAL_SPENT DESC LIMIT 5;`


#3 AVERAGE ORDER VALUES 
`SELECT ROUND(AVG(SALES),0) AS AOV FROM `auto sales data` ;`


#4. PRODUCT PERFORMANCE BY PRODUCTLINE
`SELECT 
ROUND(AVG(SALES),2) AS AVG_SALES,
ROUND(SUM(SALES),2) AS TOTAL_SALES,
COUNT(*) AS TOTAL_ORDERS 
FROM 
`auto sales data` GROUP BY PRODUCTLINE
ORDER BY TOTAL_SALES DESC;`



#5. YEARLY REVENUE AND ORDER VOLUME
`SELECT 
  EXTRACT(YEAR FROM STR_TO_DATE(ORDERDATE, '%d/%m/%Y')) AS ORDER_YEAR,
  SUM(SALES) AS TOTAL_REVENUE,
  COUNT(DISTINCT ORDERNUMBER) AS TOTAL_ORDERS
FROM `auto sales data`
WHERE ORDERDATE IS NOT NULL
GROUP BY ORDER_YEAR
ORDER BY ORDER_YEAR;`



#6. REVENUE DIFF BETWEEN DEALSIZES
`SELECT DEALSIZE, 
COUNT(*) AS TOTAL_ORDERS, ROUND(SUM(SALES),1) AS TOTAL_SALE
FROM `auto sales data`
GROUP BY DEALSIZE 
ORDER BY TOTAL_SALE DESC;`



#7. FIND DUPLICATE CUSTOMER NAME
`SELECT CUSTOMERNAME, COUNT(*) AS COUNT FROM `auto sales data` GROUP BY CUSTOMERNAME HAVING COUNT(*) > 1;`



#8. LIST OF PRODUCTS WITH BELOW AVERAGE MSRP
`SELECT PRODUCTLINE, PRODUCTCODE, MSRP FROM `auto sales data` WHERE MSRP > (SELECT AVG(MSRP)
 FROM `auto sales data`);`



 #9. COUNT OF ORDERS BY STATUS
`SELECT STATUS, COUNT(*) AS TOTAL_ORDER FROM `auto sales data` GROUP BY STATUS ORDER BY TOTAL_ORDER;`



#10. TOP 3 MONTHS BY SALES
`SELECT 
 EXTRACT(YEAR FROM STR_TO_DATE(ORDERDATE, '%d/%m/%Y')) AS ORDER_YEAR,
 EXTRACT(MONTH FROM STR_TO_DATE(ORDERDATE, '%d/%m/%y')) AS ORDER_MONTH,
 ROUND(SUM(SALES),2) AS TOTAL_REVENUE
 FROM `auto sales data` GROUP BY ORDER_YEAR, ORDER_MONTH ORDER BY TOTAL_REVENUE DESC
 LIMIT 3;`



#11. DEAL WITH MISSING VALUE
`SELECT ROUND(SUM(COALESCE(SALES, 0)),2) AS TOTAL_SALES FROM `auto sales data` ;`


---
📷 Screenshots
Screenshots of query results are included in the folder for visual reference.


---
🛠 Tools Used
MySQL Workbench

Excel / CSV files

GitHub



---
🙋‍♂️ Author
Anmol Chandra
Passionate about data, learning SQL, and diving into real-world business analysis.


