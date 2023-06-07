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
WHERE AnnualSalary >= 50000 AND (Department = 'Marketing' OR Department = 'Finance');

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


### REPLACE
REPLACE INTO Orders (OrderID, ClientID, ProductID, Quantity, Cost) <br>
VALUES (9, "Cl1", "P1", 10, 5000), (10, "Cl2", "P2", 5, 100); <br>

<br>

REPLACE INTO Orders <br>
SET OrderID = 9, ClientID = "Cl1", ProductID = "P1", Quantity = 10, Cost = 500;

<br>

## CHANGE TABLE STRUCTURE
### ALTER TABLE
ALTER TABLE Staff <br>
MODIFY StaffID INT PRIMARY KEY, <br>
MODIFY FullName VARCHAR(100) NOT NULL, <br>
MODIFY PhoneNumber INT NOT NULL;

<br>

ALTER TABLE Staff <br>
ADD COLUMN Role VARCHAR(50) NOT NULL;

<br>

ALTER TABLE Staff <br>
DROP COLUMN PhoneNumber;

<br>

## COPY TABLE

## SUBQUERIES
SELECT * <br>
FROM Bookings <br>
WHERE BookingSlot > <br>
(SELECT BookingSlot FROM Bookings WHERE GuestFirstName = 'Vanessa' AND GuestLastName = 'McCarthy');

<br>

SELECT * <br>
FROM MenuItems <br>
WHERE Price > <br>
ALL (SELECT Price FROM MenuItems WHERE Type IN ('Starters', 'Desserts'));

<br>

SELECT * <br>
FROM MenuItems WHERE Price = <br>
(SELECT Price FROM Menus, MenuItems WHERE Menus.ItemID = MenuItems.ItemID AND MenuItems.Type = 'Starters' AND Cuisine = 'Italian');

<br>

SELECT * <br>
FROM MenuItems <br>
WHERE NOT EXISTS <br>
(SELECT * FROM TableOrders, Menus WHERE TableOrders.MenuID = Menus.MenuID AND Menus.ItemID = MenuItems.ItemID);

<br>

## VIEWS
CREATE VIEW OrdersView AS <br>
SELECT OrderID, Quantity, Cost <br>
FROM Orders;

<br>

UPDATE OrdersView <br>
SET Cost = 200 <br>
WHERE OrderID = 2; 

<br>

RENAME TABLE OrdersView TO ClientsOrdersView; <br>

<br>

DROP VIEW ClientsOrdersView; 