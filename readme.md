/* joins: select all the computers from the products table: using the products table and the categories table, return the product name and the category name */

SELECT products.name, categories.name 
FROM products
INNER JOIN categories
ON products.CategoryID = categories.CategoryID
WHERE categories.Name = 'Computers';

/* joins: find all product names, product prices, and products ratings that have a rating of 5 */

SELECT products.name AS 'Charles', products.price, reviews.rating 
FROM products
INNER JOIN reviews
ON products.ProductID = reviews.ProductID 
WHERE reviews.rating = 5;

/* joins: find the employee with the most total quantity sold.  use the sum() function and group by */

SELECT employees.employeeID, FirstName, LastName, Sum(Quantity)
FROM employees
INNER JOIN sales
ON employees.EmployeeID = sales.EmployeeID
GROUP BY employees.employeeID
HAVING SUM(Quantity) = (
	SELECT SUM(Quantity)
    FROM employees
    INNER JOIN sales
    ON employees.EmployeeID = sales.EmployeeID
    GROUP BY employees.EmployeeID
    ORDER BY SUM(Quantity) DESC
    LIMIT 1
    ); 

/* joins: find the name of the department, and the name of the category for Appliances and Games */

SELECT categories.Name, departments.Name
FROM categories
INNER JOIN departments
ON categories.DepartmentID = departments.DepartmentID
WHERE categories.name IN('appliances', 'Games');

/* joins: find the product name, total # sold, and total price sold, for Eagles: Hotel California --You may need to use SUM() */

SELECT name, SUM(sales.quantity), SUM(products.price * quantity)
FROM products
INNER JOIN sales
ON products.ProductID = sales.ProductID
Where products.name = 'eagles: hotel california';

/* joins: find Product name, reviewer name, rating, and comment on the Visio TV. (only return for the lowest rating!) */

SELECT name, reviewer, rating, comment
FROM products
INNER JOIN reviews
ON products.ProductID = reviews.ProductID
Where name LIKE '%Visio%TV%' AND Rating = 1;




-- ------------------------------------------ Extra - May be difficult

/* Your goal is to write a query that serves as an employee sales report.

This query should return the employeeID, the employee's first and last name, the name of each product, how many of that product they sold */

Select name AS 'Product Name', employees.employeeId, firstName, lastName, sales.productID, Sum(Quantity)
FROM employees
INNER JOIN sales
ON sales.EmployeeID = employees.EmployeeID
INNER JOIN products
ON products.ProductID = sales.ProductID
GROUP BY employees.employeeID, sales.productId;




