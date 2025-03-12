# Retail-Sales-Analysis-SQL
SQL project analysing retail sales data with queries for revenue, customer trends, and product performance.
# Retail Sales Data Analysis (SQL Project)  

## 📌 Project Overview  
This project analyzes **retail sales data** using **SQL queries**. The goal is to extract insights such as **total revenue, best-selling products, regional sales trends, and customer spending habits**.  

## 🗂 Database Schema  
The dataset consists of three tables:  

1. **Customers** (customer information)  
2. **Products** (product details)  
3. **Sales** (sales transactions)  

### **Customers Table**  
| Column Name  | Data Type   | Description            |
|-------------|------------|------------------------|
| customer_id | INT (PK)   | Unique ID for customers |
| customer_name | VARCHAR  | Customer full name  |
| region      | VARCHAR    | Customer's region |

### **Products Table**  
| Column Name  | Data Type   | Description          |
|-------------|------------|----------------------|
| product_id  | INT (PK)   | Unique ID for products |
| product_name | VARCHAR  | Product name        |
| category    | VARCHAR    | Product category   |
| price       | DECIMAL    | Product price      |

### **Sales Table**  
| Column Name  | Data Type   | Description              |
|-------------|------------|--------------------------|
| sales_id    | INT (PK)   | Unique ID for sales      |
| order_date  | DATE       | Date of purchase         |
| customer_id | INT (FK)   | References Customers     |
| product_id  | INT (FK)   | References Products      |
| quantity    | INT        | Quantity sold           |
| total_price | DECIMAL    | Total sale amount       |

---

## 🔍 **SQL Queries & Insights**  

### 1️⃣ **Total Sales Revenue & Transactions**  
```sql
SELECT SUM(total_price) AS Total_Revenue, COUNT(*) AS Total_Transactions FROM Sales;
SELECT p.product_name, SUM(s.total_price) AS Total_Sales
FROM Sales s
JOIN Products p ON s.product_id = p.product_id
GROUP BY p.product_name
ORDER BY Total_Sales DESC
LIMIT 5;
SELECT c.region, SUM(s.total_price) AS Total_Sales
FROM Sales s
JOIN Customers c ON s.customer_id = c.customer_id
GROUP BY c.region
ORDER BY Total_Sales DESC;
SELECT c.customer_name, SUM(s.total_price) AS Total_Spent
FROM Sales s
JOIN Customers c ON s.customer_id = c.customer_id
GROUP BY c.customer_name
ORDER BY Total_Spent DESC
LIMIT 3;
SELECT DATE_FORMAT(order_date, '%Y-%m') AS Month, SUM(total_price) AS Monthly_Sales
FROM Sales
GROUP BY Month
ORDER BY Month;
