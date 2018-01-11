# Challenge Set 9
## Part I: W3Schools SQL Lab

*Introductory level SQL*

--

This challenge uses the [W3Schools SQL playground](http://www.w3schools.com/sql/trysql.asp?filename=trysql_select_all). Please add solutions to this markdown file and submit.

1. Which customers are from the UK?

7
```sql
SELECT
  COUNT(CustomerID)
FROM
  Customers
WHERE
  Country = 'UK';
```

2. What is the name of the customer who has the most orders?

Ernst Handel (10)

```sql
SELECT
	MAX(CustomerName), COUNT(*)
FROM
	Customers
JOIN
	Orders
ON
	Customers.CustomerID =
	Orders.CustomerID
GROUP BY
	CustomerName
ORDER BY
	COUNT(*) DESC
LIMIT 1;
```

3. Which supplier has the highest average product price?

Aux joyeux ecclésiastiques ($140.75)

```sql
SELECT
	Suppliers.SupplierName,
	AVG(Products.Price)
FROM
	Products
JOIN
	Suppliers
ON
	Products.SupplierID =
  Suppliers.SupplierID
GROUP BY
	Products.SupplierID
ORDER BY
	AVG(Products.Price) DESC
LIMIT 1;
```

4. How many different countries are all the customers from? (*Hint:* consider [DISTINCT](http://www.w3schools.com/sql/sql_distinct.asp).)

21
```sql
SELECT
  COUNT(DISTINCT(Country))
AS
  [Number of Unique Countries]
FROM
  [Customers];
```

5. What category appears in the most orders?
Dairy Products (100)

```sql
SELECT
  Categories.CategoryName,
  COUNT(*)
FROM
  Categories
JOIN
  Products
ON
  Categories.CategoryID = Products.CategoryID
JOIN
  OrderDetails
ON
  OrderDetails.ProductID = Products.ProductID
GROUP BY
  Categories.CategoryID
ORDER BY
  COUNT(Categories.CategoryID) DESC
LIMIT 1;
```

6. What was the total cost for each order?

```sql
SELECT
	OrderDetails.OrderID,
  SUM(Products.Price)
FROM
	OrderDetails
JOIN
	Products
ON
	OrderDetails.ProductID =
  Products.ProductID
GROUP BY
	OrderID
```
7. Which employee made the most sales (by total price)?

Peacock, Margaret ($3887.22)

```sql
SELECT  
	Employees.LastName,
  Employees.FirstName,
  SUM(Products.Price)
FROM
	Employees
JOIN
	Orders
ON
	Employees.EmployeeID =
  Orders.EmployeeID
JOIN
	OrderDetails
ON
	Orders.OrderID =
  OrderDetails.OrderID
JOIN
	Products
ON
  OrderDetails.ProductID =
  Products.ProductID
GROUP BY
	Employees.EmployeeID
ORDER BY
	SUM(Products.Price) DESC
LIMIT 1;
```

8. Which employees have BS degrees? (*Hint:* look at the [LIKE](http://www.w3schools.com/sql/sql_like.asp) operator.)

Leverling,	Janet
Buchanan,	Steven

```sql
SELECT
	LastName,
  FirstName
FROM
	Employees
WHERE
	Notes
LIKE
	'%BS%';
```
9. Which supplier of three or more products has the highest average product price? (*Hint:* look at the [HAVING](http://www.w3schools.com/sql/sql_having.asp) operator.)
