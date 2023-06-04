# SQL

## Filtering Data
### AND
SELECT * <br>
FROM employees <br>
WHERE AnnualSalary >= 50000 AND Department = 'Marketing';

<br>

### OR
SELECT * <br>
FROM employees <br>
WHERE AnnualSalary >= 50000 AND (Department = 'Marketing' OR 'Finance');

<br>

### NOT
SELECT * <br>
FROM employees <br>
WHERE NOT AnnualSalary >= 50000;

<br>

### IN
SELECT * <br>
FROM employees <br>
WHERE AnnualSalary < 50000 AND Department IN('Marketing', 'Finance', 'Legal');

<br>

### BETWEEN 
SELECT * <br>
FROM employees <br>
WHERE AnnualSalary BETWEEN 10000 AND 50000;

<br>

### LIKE

<br><br>

## Joins
### ALIAS 
### INNER 
SELECT Customers.FullName, Customers.PhoneNumber, Bookings.BookingDate, Bookings.NumberOfGuests <br>
FROM Customers INNER JOIN Bookings <br>
ON Customers.CustomerID = Bookings.CustomerID;

<br>

### LEFT
SELECT Customers.CustomerID, Bookings.BookingID <br>
FROM Customers LEFT JOIN Bookings <br>
ON Customers.CustomerID = Bookings.CustomerID;

<br>

### RIGHT
SELECT Customers.CustomerID, Bookings.BookingID <br>
FROM Customers RIGHT JOIN Bookings <br>
ON Customers.CustomerID = Bookings.CustomerID;

<br>

### SELF

<br>

### UNION

<br><br>

## Grouping Data
### GROUP BY
SELECT EmployeeID, HandlingCost   <br>
FROM employee_orders   <br>
WHERE HandlingCost > ALL(SELECT ROUND(OrderTotal/100 * 20) FROM orders) GROUP BY EmployeeID,HandlingCost;

<br>

### HAVING
SELECT EmployeeID, HandlingCost <br>
FROM employee_orders  <br>
WHERE HandlingCost > ALL(SELECT ROUND(OrderTotal/100 * 20) AS twentyPercent FROM orders  GROUP BY OrderTotal  <br>
HAVING twentyPercent > 100)  GROUP BY EmployeeID,HandlingCost;  

<br>

### ANY
SELECT EmployeeId, EmployeeName <br> 
FROM employees <br>
WHERE EmployeeID = ANY (SELECT EmployeeID FROM employee_orders WHERE Status='Completed'); 

<br>

### ALL
SELECT EmployeeID,HandlingCost <br>
FROM employee_orders <br>
WHERE HandlingCost > ALL(SELECT ROUND(OrderTotal/100 * 20) FROM orders);

<br>
