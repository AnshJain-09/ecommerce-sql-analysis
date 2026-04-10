# ecommerce-sql-analysis
"SQL-based sales and customer data analysis project showcasing advanced queries, revenue insights, and business intelligence using relational databases."
#  E-Commerce SQL Analysis

A collection of SQL queries for analyzing an e-commerce database (based on the Northwind-style schema). Covers customer behavior, product performance, employee sales, and shipping insights.

---

##  File

| File | Description |
|------|-------------|
| `ecommerce-sql-analysis.sql` | All analysis queries |

---

##  Database Schema

The queries assume the following core tables:

- **customers** — customer info (ID, company name, city)
- **orders** — order headers (order ID, customer ID, employee ID, shipper ID, freight, order date)
- **order_details** — line items (order ID, product ID, quantity, unit price, discount)
- **products** — product catalog (product ID, name, category ID, discontinued flag)
- **categories** — product categories
- **employees** — employee records
- **shippers** — shipping companies

---

##  Queries Overview

### 1. Orders with Customer Details
Lists all orders along with the corresponding customer name and city.

### 2. Total Quantity Ordered per Product
Aggregates quantity sold for each product, sorted by highest volume.

### 3. Percentage of Total Revenue by Product
Calculates each product's share of overall revenue using a subquery for the total.

### 4. Top 5 Customers by Spending
Ranks customers by their total order spend (after discounts).

### 5. Zero Out Discounts on Discontinued Products *(DML)*
Updates `order_details` to set discount = 0 for any discontinued product.

### 6. Above-Average Freight Cost by Shipper
Finds shippers whose average freight cost exceeds the overall average, using a `HAVING` clause.

### 7. Monthly Sales Revenue by Employee
Breaks down revenue by year, month, and employee — useful for trend and performance analysis.

### 8. Shipper Handling Most High-Value Orders (>$500)
Uses a CTE to first isolate orders over $500, then counts how many each shipper handled.

### 9. Top-Selling Employee per Product Category
Uses a CTE with a subquery to find the employee with the highest revenue in each category.

---

##  Usage

Run these queries against any MySQL-compatible database loaded with the Northwind dataset.

```sql
-- Example: Top 5 customers by spend
SELECT o.customerID, SUM(od.quantity * od.unitPrice * (1 - od.discount)) AS customer_spend
FROM orders o
JOIN order_details od ON o.orderID = od.orderID
GROUP BY o.customerID
ORDER BY customer_spend DESC
LIMIT 5;
```

---

##  Concepts Demonstrated

- `JOIN` (multi-table)
- Aggregate functions (`SUM`, `AVG`, `COUNT`)
- Subqueries & correlated subqueries
- Common Table Expressions (`WITH ... AS`)
- `HAVING` for post-aggregation filtering
- `UPDATE` with a subquery
- Date functions (`YEAR`, `MONTH`)
- Window-style ranking via CTE + max matching

##  Use Cases
- Sales analysis
- Customer behavior insights
- Product performance tracking
- Employee performance evaluation
- Logistics & shipping optimization
