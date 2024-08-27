## MySQL Basics

### 1. **Introduction to MySQL**

MySQL is a popular open-source relational database management system (RDBMS) that uses Structured Query Language (SQL) for managing and manipulating databases.

### 2. **MySQL Data Types**

MySQL supports various data types, categorized into several groups:

- **Numeric Types**:
    - `INT` (integer), `TINYINT`, `SMALLINT`, `MEDIUMINT`, `BIGINT`
    - `DECIMAL`(or `NUMERIC`), `FLOAT`, `DOUBLE`
    - `BIT`, `BOOLEAN`
- **String Types**:
    - `CHAR`, `VARCHAR`
    - `TEXT`, `TINYTEXT`, `MEDIUMTEXT`, `LONGTEXT`
    - `BLOB`, `TINYBLOB`, `MEDIUMBLOB`, `LONGBLOB`
    - `ENUM`, `SET`
- **Date and Time Types**:
    - `DATE`, `DATETIME`, `TIMESTAMP`
    - `TIME`, `YEAR`
- **Spatial Types**: For geographic data types such as `POINT`, `LINESTRING`, `POLYGON`.

### **DDL (Data Definition Language)**

- **Create**: Used to create tables, databases, etc.
- **Alter**: Modify the structure of an existing database object.
    - **Alter Table**:
        - Add or drop columns.
        - Add or drop constraints (e.g., foreign keys, unique, etc.).
        - Modify existing columns.
- **Drop**: Delete tables or databases.
- **Truncate**: Remove all records from a table, but not the table itself.
- **Rename**: Change the name of an existing database object.

### **DML (Data Manipulation Language)**

- **Insert**: Add new records to a table.
- **Update**: Modify existing records.
- **Delete**: Remove records from a table.

### **DQL (Data Query Language)**

- **Select**: Retrieve data from a database.
    - **From**: Specifies the table to query data from.
    - **Where**: Filters records based on specified conditions.

### **Keys in SQL**

Keys are fundamental elements in SQL databases that are used to identify records uniquely, establish relationships between tables, and ensure data integrity. Here’s a brief overview of the different types of keys commonly used in SQL:

1. **Primary Key**:
    - A primary key is a column or a set of columns in a table that uniquely identifies each row in that table.
    - **Characteristics**:
        - Must contain unique values.
        - Cannot contain `NULL` values.
        - Each table can have only one primary key.
    - **Syntax**:
        
        ```sql
        CREATE TABLE Employees (
            EmployeeID INT NOT NULL PRIMARY KEY,
            FirstName VARCHAR(50),
            LastName VARCHAR(50)
        );
        
        ```
        
2. **Foreign Key**:
    - A foreign key is a column or a set of columns in a table that establishes a link between the data in two tables.
    - It refers to the primary key in another table, ensuring referential integrity between the two tables.
    - **Characteristics**:
        - Can contain duplicate values.
        - Can contain `NULL` values (unless specified otherwise).
    - **Syntax**:
        
        ```sql
        CREATE TABLE Orders (
            OrderID INT NOT NULL PRIMARY KEY,
            EmployeeID INT,
            FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
        );
        
        ```
        
3. **Unique Key**:
    - A unique key is a column or a set of columns that ensures all values in the column(s) are distinct.
    - **Characteristics**:
        - Must contain unique values.
        - Can contain a single `NULL` value (unlike a primary key).
        - A table can have multiple unique keys.
    - **Syntax**:
        
        ```sql
        CREATE TABLE Customers (
            CustomerID INT NOT NULL,
            Email VARCHAR(100) UNIQUE
        );
        
        ```
        
4. **Composite Key**:
    - A composite key is a combination of two or more columns that uniquely identify a row in a table.
    - It is often used when a single column is not sufficient to ensure uniqueness.
    - **Syntax**:
        
        ```sql
        CREATE TABLE Enrollment (
            StudentID INT,
            CourseID INT,
            EnrollmentDate DATE,
            PRIMARY KEY (StudentID, CourseID)
        );
        
        ```
        

### **Summary**

- **Primary Key**: Uniquely identifies each record in a table; only one per table, no `NULL` values.
- **Foreign Key**: Establishes a relationship between tables; can have duplicate and `NULL` values.
- **Unique Key**: Ensures all values in a column are unique; allows one `NULL` value.
- **Composite Key**: A combination of columns used to uniquely identify a record.

Keys are crucial for designing robust and efficient relational databases, ensuring data accuracy and relational integrity.

### **Aliases (AS)**

- Used to give temporary names to columns or tables.

```sql
SELECT CONCAT(first_name , last_name) AS full_name FROM customers;
```

### **Logical Operators**

- **AND, OR, NOT**: Used to combine multiple conditions.
- **IS, IS NOT**: Used for NULL checks.
- **BETWEEN, IN**: Range and set operations.
- **Wildcards**:
    - `%`: Represents zero or more characters.
    - `_`: Represents exactly one character.

### 3. **Creating and Managing Databases**

### **Create a Database**

```sql
CREATE DATABASE database_name;

```

### **Show Databases**

```sql
SHOW DATABASES;

```

### **Use a Database**

```sql
USE database_name;

```

### **Drop a Database**

```sql
DROP DATABASE database_name;

```

### 4. **Creating and Managing Tables**

### **Create a Table**

```sql
CREATE TABLE table_name (
    column1 datatype constraints,
    column2 datatype constraints,
    ...
);

```

- **Example**:
    
    ```sql
    CREATE TABLE Employees (
        EmployeeID INT PRIMARY KEY AUTO_INCREMENT,
        FirstName VARCHAR(50) NOT NULL,
        LastName VARCHAR(50) NOT NULL,
        BirthDate DATE,
        Salary DECIMAL(10, 2),
        DepartmentID INT
    );
    
    ```
    

### **Show Tables**

```sql
SHOW TABLES;

```

### **Describe a Table Structure**

```sql
DESCRIBE table_name;

```

or

```sql
SHOW COLUMNS FROM table_name;

```

### **Drop a Table**

```sql
DROP TABLE table_name;

```

### **Alter a Table**

- **Add a Column**:
    
    ```sql
    ALTER TABLE table_name ADD column_name datatype constraints;
    
    ```
    
- **Modify a Column**:
    
    ```sql
    ALTER TABLE table_name MODIFY column_name new_datatype constraints;
    
    ```
    
- **Drop a Column**:
    
    ```sql
    ALTER TABLE table_name DROP COLUMN column_name;
    
    ```
    

### 5. **Inserting, Updating, and Deleting Data**

### **Insert Data into a Table**

```sql
INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...);

```

- **Example**:
    
    ```sql
    INSERT INTO Employees (FirstName, LastName, BirthDate, Salary, DepartmentID)
    VALUES ('John', 'Doe', '1980-01-15', 50000.00, 1);
    
    ```
    

### **Insert Multiple Rows**

```sql
INSERT INTO table_name (column1, column2, ...) VALUES
(value1, value2, ...),
(value1, value2, ...),
...;

```

### **Update Data in a Table**

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;

```

- **Example**:
    
    ```sql
    UPDATE Employees
    SET Salary = 55000.00
    WHERE EmployeeID = 1;
    
    ```
    

### **Delete Data from a Table**

```sql
DELETE FROM table_name WHERE condition;

```

- **Example**:
    
    ```sql
    DELETE FROM Employees WHERE EmployeeID = 1;
    
    ```
    

### **Truncate a Table**

Removes all data from a table but keeps the table structure:

```sql
TRUNCATE TABLE table_name;

```

### 6. **Basic SQL Queries**

### **Select Data from a Table**

```sql
SELECT column1, column2, ... FROM table_name;

```

- **Select All Columns**:
    
    ```sql
    SELECT * FROM table_name;
    
    ```
    

### **Where Clause**

```sql
SELECT column1, column2, ... FROM table_name WHERE condition;

```

- **Example**:
    
    ```sql
    SELECT * FROM Employees WHERE Salary > 50000;
    
    ```
    

### **Order By Clause**

Sorts the result set in ascending (`ASC`) or descending (`DESC`) order:

```sql
SELECT column1, column2, ... FROM table_name ORDER BY column1 ASC|DESC;

```

- **Example**:
    
    ```sql
    SELECT * FROM Employees ORDER BY LastName ASC;
    
    ```
    

### **GROUP BY Clause**

```sql
SELECT DepartmentID, COUNT(*)
FROM Employees
GROUP BY DepartmentID
HAVING COUNT(*) > 5;

```

- **Purpose**: The `GROUP BY` clause is used to group rows that have the same values in specified columns into summary rows, like "find the total salary of employees in each department."
- **Usage**: It is commonly used with aggregate functions to perform calculations on each group of data.
- **Syntax**:
    
    ```sql
    SELECT column1, aggregate_function(column2)
    FROM table_name
    GROUP BY column1;
    
    ```
    
- **Example**:
This query calculates the total salary for each department.
    
    ```sql
    SELECT Department, SUM(Salary) AS TotalSalary
    FROM Employees
    GROUP BY Department;
    
    ```
    

### **HAVING Clause**

- **Purpose**: The `HAVING` clause is used to filter groups created by the `GROUP BY` clause based on a condition.
- **Difference from WHERE**: While `WHERE` filters rows before grouping, `HAVING` filters groups after the grouping has been applied.
- **Usage**: Used with `GROUP BY` to apply conditions to groups.
- **Syntax**:
    
    ```sql
    SELECT column1, aggregate_function(column2)
    FROM table_name
    GROUP BY column1
    HAVING condition;
    
    ```
    
- **Example**:
This query returns departments with more than 10 employees.
    
    ```sql
    SELECT Department, COUNT(*)
    FROM Employees
    GROUP BY Department
    HAVING COUNT(*) > 10;
    
    ```
    

### **Summary**

- **GROUP BY**: Groups rows that share a value in specified columns for aggregation.
- **HAVING**: Filters these grouped results based on aggregate conditions.

### 7. **Joins**

### **Inner Join**

Returns records that have matching values in both tables:

```sql
SELECT table1.column1, table2.column2, ...
FROM table1
INNER JOIN table2 ON table1.common_column = table2.common_column;

```

- **Example**:
    
    ```sql
    SELECT Employees.FirstName, Departments.DepartmentName
    FROM Employees
    INNER JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
    
    ```
    

### **Left Join (Left Outer Join)**

Returns all records from the left table, and the matched records from the right table:

```sql
SELECT table1.column1, table2.column2, ...
FROM table1
LEFT JOIN table2 ON table1.common_column = table2.common_column;

```

### **Right Join (Right Outer Join)**

Returns all records from the right table, and the matched records from the left table:

```sql
SELECT table1.column1, table2.column2, ...
FROM table1
RIGHT JOIN table2 ON table1.common_column = table2.common_column;

```

### **Full Join (Full Outer Join)**

Returns all records when there is a match in either left or right table. *Note: MySQL does not support FULL JOIN directly, but you can achieve it using a combination of LEFT JOIN and RIGHT JOIN.*

### 8. **Subqueries**

A subquery is a query within another SQL query:

```sql
SELECT column1, column2, ...
FROM table_name
WHERE column_name IN (SELECT column_name FROM another_table WHERE condition);

```

### 9. **Indexes**

Indexes are used to speed up the retrieval of data from a database table:

### **Create an Index**

```sql
CREATE INDEX index_name ON table_name (column1, column2, ...);

```

### **Drop an Index**

```sql
DROP INDEX index_name ON table_name;

```

### 10. **Views**

A view is a virtual table based on the result-set of an SQL statement:

### **Create a View**

```sql
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;

```

### **Drop a View**

```sql
DROP VIEW view_name;

```

### 12. **Stored Procedures**

```sql
DELIMITER //

CREATE FUNCTION GetEmployeeCount(dept_id INT) RETURNS INT
BEGIN
    DECLARE emp_count INT;
    SELECT COUNT(*) INTO emp_count
    FROM Employees
    WHERE DepartmentID = dept_id;
    RETURN emp_count;
END //

DELIMITER ;

```

### **What is a Stored Procedure?**

A stored procedure is a set of SQL statements that can be stored and executed on the database server. Stored procedures are used to encapsulate repetitive tasks and logic that you want to execute multiple times without rewriting the code.

### **Creating a Stored Procedure**

**Syntax:**

```sql
DELIMITER //

CREATE PROCEDURE procedure_name (IN parameter1 datatype, OUT parameter2 datatype, ...)
BEGIN
    -- SQL statements
    -- You can use SELECT, INSERT, UPDATE, DELETE, etc.
END //

DELIMITER ;

```

**Explanation:**

- `DELIMITER //` is used to change the default statement delimiter from `;` to `//` (or any other delimiter you choose) to allow for creating a procedure with multiple statements. It is reverted back to `;` after the procedure definition.
- `CREATE PROCEDURE procedure_name` is the command to create a stored procedure.
- `(IN|OUT|INOUT parameter_name datatype)` specifies the parameters of the procedure.
    - **IN**: Input parameter (default). The procedure can read the input value, but it cannot modify the parameter.
    - **OUT**: Output parameter. The procedure can modify the parameter to pass back a value.
    - **INOUT**: Input and output parameter. The procedure can both read and modify the parameter.
- `BEGIN` and `END` keywords define the body of the procedure.

**Example:**

```sql
DELIMITER //

CREATE PROCEDURE AddEmployee (
    IN p_first_name VARCHAR(50),
    IN p_last_name VARCHAR(50),
    IN p_birth_date DATE,
    IN p_salary DECIMAL(10,2),
    IN p_department_id INT,
    OUT p_employee_id INT
)
BEGIN
    INSERT INTO Employees (FirstName, LastName, BirthDate, Salary, DepartmentID)
    VALUES (p_first_name, p_last_name, p_birth_date, p_salary, p_department_id);

    SET p_employee_id = LAST_INSERT_ID();
END //

DELIMITER ;

```

In this example, the `AddEmployee` procedure inserts a new employee into the `Employees` table and returns the new `EmployeeID` using an `OUT` parameter.

### **Calling a Stored Procedure**

**Syntax:**

```sql
CALL procedure_name(parameter1, parameter2, ...);

```

**Example:**

```sql
CALL AddEmployee('John', 'Doe', '1980-01-15', 50000.00, 1, @new_employee_id);
SELECT @new_employee_id;

```

In this example, the `CALL` statement executes the `AddEmployee` procedure with specific parameters. The `@new_employee_id` variable is used to capture the output parameter.

### **Modifying a Stored Procedure**

To modify an existing stored procedure, you must drop it and then recreate it.

**Drop a Procedure:**

```sql
DROP PROCEDURE IF EXISTS procedure_name;

```

**Recreate the Procedure:**
Use the `CREATE PROCEDURE` syntax as before to recreate the stored procedure with the desired changes.

### **Dropping a Stored Procedure**

**Syntax:**

```sql
DROP PROCEDURE procedure_name;

```

**Example:**

```sql
DROP PROCEDURE AddEmployee;

```

## 13. **Stored Functions**

### **What is a Stored Function?**

A stored function is similar to a stored procedure, but it returns a single value. Functions can be used in SQL statements wherever an expression is allowed, such as in SELECT lists or WHERE clauses.

### **Creating a Stored Function**

**Syntax:**

```sql
DELIMITER //

CREATE FUNCTION function_name (parameter_name datatype, ...)
RETURNS datatype
DETERMINISTIC -- or NOT DETERMINISTIC
BEGIN
    -- Variable declarations
    -- SQL statements
    RETURN value;
END //

DELIMITER ;

```

**Explanation:**

- `CREATE FUNCTION function_name` is the command to create a stored function.
- `(parameter_name datatype, ...)` specifies the parameters of the function. Functions can only have `IN` parameters.
- `RETURNS datatype` specifies the data type of the value that the function returns.
- `DETERMINISTIC` or `NOT DETERMINISTIC` indicates whether the function returns the same result for the same input parameters.
- `BEGIN` and `END` keywords define the body of the function.
- `RETURN` specifies the value to return.

**Example:**

```sql
DELIMITER //

CREATE FUNCTION GetEmployeeSalary (p_employee_id INT)
RETURNS DECIMAL(10, 2)
DETERMINISTIC
BEGIN
    DECLARE v_salary DECIMAL(10, 2);

    SELECT Salary INTO v_salary
    FROM Employees
    WHERE EmployeeID = p_employee_id;

    RETURN v_salary;
END //

DELIMITER ;

```

In this example, the `GetEmployeeSalary` function returns the salary of a specific employee.

### **Calling a Stored Function**

Stored functions can be called as part of SQL statements.

**Syntax:**

```sql
SELECT function_name(parameter1, parameter2, ...);

```

**Example:**

```sql
SELECT GetEmployeeSalary(1) AS Salary;

```

In this example, the `GetEmployeeSalary` function is called to retrieve the salary of the employee with `EmployeeID` 1.

### **Modifying a Stored Function**

To modify an existing stored function, you must drop it and then recreate it.

**Drop a Function:**

```sql
DROP FUNCTION IF EXISTS function_name;

```

**Recreate the Function:**
Use the `CREATE FUNCTION` syntax as before to recreate the stored function with the desired changes.

### **Dropping a Stored Function**

**Syntax:**

```sql
DROP FUNCTION function_name;

```

**Example:**

```sql
DROP FUNCTION GetEmployeeSalary;

```

## 3. **Key Differences Between Stored Procedures and Functions**

| Feature | Stored Procedure | Stored Function |
| --- | --- | --- |
| **Purpose** | Executes a set of SQL statements | Performs a calculation and returns a single value |
| **Return Value** | Can return multiple values using `OUT` parameters | Returns a single value using the `RETURN` keyword |
| **Usage in SQL Statements** | Cannot be used directly in SQL statements | Can be used directly in SQL statements (e.g., SELECT) |
| **Parameter Types** | `IN`, `OUT`, `INOUT` | Only `IN` parameters |
| **Transaction Handling** | Can contain transaction statements like COMMIT, ROLLBACK | Limited, as they should not have transaction control statements |
| **Effect on Data** | Can modify database data | Typically does not modify database data |

Stored procedures and functions are powerful tools in MySQL for managing complex logic and calculations directly in the database. Using these appropriately can help optimize database performance and maintainability.

### **13. Transactions in SQL (TCL)**

A **transaction** in SQL is a sequence of one or more SQL statements that are executed as a single unit of work. Transactions ensure data integrity and consistency by following the ACID properties:

1. **Atomicity**: Ensures that all parts of a transaction are completed; if any part fails, the entire transaction is rolled back.
2. **Consistency**: Ensures the database transitions from one valid state to another, maintaining data integrity.
3. **Isolation**: Ensures that transactions are executed independently without interference, even if they are occurring simultaneously.
4. **Durability**: Ensures that once a transaction is committed, the changes are permanently stored in the database.

### **Basic Transaction Commands**

- **START TRANSACTION** or **BEGIN**: Begins a new transaction.
- **COMMIT**: Saves all changes made during the transaction permanently to the database.
- **ROLLBACK**: Reverts all changes made during the transaction, restoring the database to its previous state.

### **Start a Transaction**

```sql
START TRANSACTION;

```

### **Commit a Transaction**

```sql
COMMIT;

```

### **Rollback a Transaction**

```sql
ROLLBACK;

```

### 14. **Common SQL Functions**

- **Aggregate Functions**: `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`
- **String Functions**: `CONCAT()`, `SUBSTRING()`, `LENGTH()`, `REPLACE()`
- **Date Functions**: `NOW()`, `CURDATE()`, `DATEDIFF()`, `DATE_FORMAT()`
- **Mathematical Functions**: `ABS()`, `ROUND()`, `CEILING()`, `FLOOR()`

### CURSOR

A **cursor** in MySQL is a database object used to retrieve and manipulate data row by row from a result set. Cursors are useful when you need to process query results one row at a time rather than all at once.

### **Key Points about Cursors:**

1. **Declaration**: Cursors must be declared before they are used and after any variable declarations in the same block.
2. **Opening**: After declaring, a cursor must be opened to establish the result set.
3. **Fetching**: Once the cursor is open, rows can be fetched one at a time into variables.
4. **Closing**: After processing the rows, the cursor should be closed to release the resources.

### **Basic Cursor Syntax:**

1. **Declare a Cursor**:
    
    ```sql
    DECLARE cursor_name CURSOR FOR
    SELECT column1, column2 FROM table_name WHERE condition;
    
    ```
    
2. **Open a Cursor**:
    
    ```sql
    OPEN cursor_name;
    
    ```
    
3. **Fetch Data from a Cursor**:
    
    ```sql
    FETCH cursor_name INTO variable1, variable2;
    
    ```
    
4. **Close a Cursor**:
    
    ```sql
    CLOSE cursor_name;
    
    ```
    

### **Example Usage:**

```sql
DELIMITER //

CREATE PROCEDURE ProcessEmployees()
BEGIN
    DECLARE done INT DEFAULT 0;
    DECLARE emp_name VARCHAR(50);
    DECLARE emp_salary DECIMAL(10,2);

    DECLARE emp_cursor CURSOR FOR
    SELECT name, salary FROM Employees;

    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = 1;

    OPEN emp_cursor;

    read_loop: LOOP
        FETCH emp_cursor INTO emp_name, emp_salary;
        IF done THEN
            LEAVE read_loop;
        END IF;
        -- Process each row here
        -- For example, we can print the name and salary
        SELECT emp_name, emp_salary;
    END LOOP;

    CLOSE emp_cursor;
END //

DELIMITER ;

```

In this example:

- A cursor named `emp_cursor` is declared to select employee names and salaries.
- The cursor is opened, and rows are fetched one by one inside a loop.
- The loop continues until all rows are processed, after which the cursor is closed.

### **When to Use Cursors**

- **Row-by-Row Processing**: Cursors are used when you need to perform row-by-row processing, such as complex calculations or operations that cannot be easily done with a standard SQL query.
- **Procedural Logic**: They are often used in stored procedures where procedural logic is needed.

###

### **Triggers in MySQL**

A **trigger** is a set of SQL statements that automatically executes or "fires" in response to certain events on a particular table in a database. Triggers are used to enforce business rules, validate data, maintain audit trails, and synchronize tables.

### **Key Points about Triggers:**

1. **Automatic Execution**: Triggers execute automatically when a specified event occurs (e.g., `INSERT`, `UPDATE`, or `DELETE` operations on a table).
   
2. **Event-Based**: Triggers are defined to fire before or after a specific event:
   - **BEFORE Trigger**: Executes before the triggering event is processed. Commonly used to validate or modify data before it's written to the database.
   - **AFTER Trigger**: Executes after the triggering event is processed. Often used for logging changes, auditing, or updating related tables.

3. **Attached to a Table**: Triggers are associated with a specific table and defined for specific events on that table.

4. **Cannot be Manually Invoked**: Unlike stored procedures or functions, triggers cannot be called or executed manually. They are automatically executed by the database system in response to the specified events.

5. **Scope of Use**: Typically used for:
   - **Data Integrity**: Ensuring data consistency and enforcing business rules.
   - **Auditing**: Tracking changes to data for audit purposes.
   - **Automation**: Automating repetitive tasks, such as updating related records.

### **Syntax of Triggers in MySQL:**

```sql
CREATE TRIGGER trigger_name
{BEFORE | AFTER} {INSERT | UPDATE | DELETE}
ON table_name
FOR EACH ROW
BEGIN
    -- SQL statements
END;
```

### **Example Usage of Triggers:**

1. **Example of an AFTER INSERT Trigger**:
   
   ```sql
   CREATE TRIGGER after_employee_insert
   AFTER INSERT ON employees
   FOR EACH ROW
   BEGIN
       -- Automatically insert a record into an audit table whenever a new employee is added
       INSERT INTO audit_log (action, employee_id, action_time)
       VALUES ('INSERT', NEW.employeeNumber, NOW());
   END;
   ```
   
   - **Trigger Name**: `after_employee_insert`.
   - **Trigger Event**: Fires after an `INSERT` operation on the `employees` table.
   - **Purpose**: Logs the action to an `audit_log` table whenever a new employee is inserted.

2. **Example of a BEFORE UPDATE Trigger**:
   
   ```sql
   CREATE TRIGGER before_employee_update
   BEFORE UPDATE ON employees
   FOR EACH ROW
   BEGIN
       -- Ensure the salary is not decreased
       IF NEW.salary < OLD.salary THEN
           SIGNAL SQLSTATE '45000'
           SET MESSAGE_TEXT = 'Salary cannot be decreased';
       END IF;
   END;
   ```
   
   - **Trigger Name**: `before_employee_update`.
   - **Trigger Event**: Fires before an `UPDATE` operation on the `employees` table.
   - **Purpose**: Prevents the salary from being decreased by raising an error.


