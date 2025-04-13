# Task-3--Data-Analytics
## SELECT, WHERE, ORDER BY
SELECT CustomerID, CustomerName, City, Country
FROM customers
WHERE Country = 'Germany'
ORDER BY CustomerName;
## Subquery
SELECT CustomerName, Country
FROM customers
WHERE Country IN (
    SELECT Country
    FROM customers
    GROUP BY Country
    HAVING COUNT(*) > 3
);
## Aggregation
SELECT 
    MONTH(OrderDate) AS OrderMonth,
    COUNT(*) AS TotalOrders
FROM 
    orders
GROUP BY 
    OrderMonth
ORDER BY 
    OrderMonth;
## View
CREATE VIEW OrdersPerEmployee AS
SELECT 
    e.EmployeeID,
    CONCAT(e.FirstName, ' ', e.LastName) AS FullName,
    COUNT(o.OrderID) AS TotalOrders
FROM 
    employees e
LEFT JOIN 
    orders o ON e.EmployeeID = o.EmployeeID
GROUP BY 
    e.EmployeeID;
SELECT * FROM OrdersPerEmployee ORDER BY TotalOrders DESC;
## Index
CREATE INDEX idx_orderdate ON orders(OrderDate);


