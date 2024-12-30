2024-12-15 12:17

Status: [[complete]]

Tags: [[PostgreSQL]] [[CORE CS]]


# PostgreSQL Complete Notes

##### Why? 
1. Adheres to SQL Standards
2. Excels in concurrency
3. Superior at avoiding data corruption
4. Custom data types, operators and index types
5. Extensible, scalable and protects our data
---
#### Database?
Organized collection of structured information. basically they are computer servers where we can store, manipulate and retrieve the data.
Data is stored in form of rows and columns.
* Column : Attribute
* Row : Actual Data*
---
##### SQL : Structured query language

Postgres is actual database engine and SQL is used in it. SQL allow us to interact with database.
* Relational Database is relation between one or more tables.
---
##### PSQL is command line tool to interact with postgreSQL database

| psql command      | Use                |
| ----------------- | ------------------ |
| psql -U <db_name> | connect to databse |
| \l                | list all databases |

---
### 1.Create AND Insert Into Table
```sql
CREATE TABLE customer(
	id SERIAL PRIMARY KEY,
	first_name VARCHAR(30) NOT NULL,
	last_name VARCHAR(30) NOT NULL,
	email VARCHAR(30) NOT NULL,
	state CHAR(2) NOT NULL, 
	zip SMALLINT NOT NULL,
	birth_date DATE NULL,
	sex CHAR(1) NOT NULL,
	curr_date TIMESTAMP NOT NULL
);

INSERT INTO customer(first_name, last_name, email, state, zip, birth_date, 
					sex, curr_date) VALUES (
					'Shreyas', 
					'Shevale',
					'shreyas2003@gmail.com',
					'MH',
					416214,
					'2003-06-29',
					'M',
					current_timestamp);
-- current_timestamp --. It gives current timestamp for us
		
```
---
### 2.Data Types
##### 1. Character Types :
1. Char(5) - Stores up-to max 5 characters.
2. Varchar - store any length of characters (basically String). e.g. VARCHAR(20) stores 20 chars
3. Text - store any length of characters.
##### 2. Numeric Types :
1. Serial - Whole numbers that auto increment. (generally used for primary key)
	- Smallserial : 1 to 32,767
	- Serial : 1 to 2147482647
	- Bigserial : 1 to alot...upto 19 digit number
2. Integer - Whole numbers
	- smallint : -32,768 to 32,767
	- Integer : -2,147,583,648 to 2,147,583,647
	- Bigint : alot big
3. Floats - Numbers with decimals
	- Decimal 131072 whole digits and 16383 after decimal. (How many we can store)
	- Numeric : 131072 whole digits and 16383 after decimal
	- Real : 1E-37 to 1E37 (6 places of precision)
	- Double Precision : 1E-307 to 1E308 (15 places of precision) used when decimal doesn't have to be very precise
	- Float : same as double
##### 3. Boolean :
- True, False or Null.
	- True, 1, t, y, yes, on
	- False, 0, f, n, no, off
	- null
##### 4. DATE/TIME - 
- Date : No matter what format we enter we get *YYYY-MM-DD* format.
- Time : 
	- '1:30:30':: TIME WITHOUT TIMEZONE -> 13:30:30
	- 01:30 AM EST -> 01:30-5:00 (UTC format)
	- 01:30 PM PST -> 01:30-8:00
	- 01:30 PM UTC -> 01:30+00:00
	- 1:30:30 PM EST':: TIME WITHOUT TIMEZONE -> 13:30:30-5:00
- Timestamp : these contains date and time both info
	- 'DEC-21-1974 1:30 PM EST':: TIMESTAMP WITH TIME ZONE
		-> 1972-21-21 13:30-5:00
- Interval : Represent duration of time
	- '1 day' :: `INTERVAL` -> 01:00
	- '1D 1H 1M 1S'::`INTERVAL` -> 01:01:01:01 (DD:HH:MM:SS) 
	- We can add and subtract intervals
##### 6. Other Data Types :
1. Currency
2. Binary
3. JSON
4. Range
5. Geometric
6. Arrays
7. XML
8. UUID
7. Custom Data Types -  we can create our own data type in postgres.
	e.g.
```sql
-- create Enumerated custom type
CREATE TYPE sex_type as enum ('M', 'F');
```
##### 7. Type Casting : 
It is used to convert one data type to another.
 - `::` is used for type casting in postgresql.
```sql
SELECT CURRENT_DATE::text;  -- Converts the current date to a text representation
SELECT '123'::int;   -- convert string to int
```

### 3.Primary Key and Foreign Key
Primary key is a column or a set of columns that uniquely identifies a row in a table. It enforces uniqueness and **not-null** constraints automatically.
```sql
CREATE TABLE table_name ( 
	column1 datatype PRIMARY KEY, 
	column2 datatype, 
	column3 datatype 
);

-- Composite primary key
CREATE TABLE table_name ( 
	column1 datatype, 
	column2 datatype, 
	column3 datatype, 
	PRIMARY KEY (column1, column2) 
);
```

- A table can have only one primary key, but it can consist of multiple columns (composite key).
- PostgreSQL automatically creates an **index** on the primary key for fast lookups.
- Composite primary key - 

| student_id | course_id |
| ---------- | --------- |
| 1          | 101       |
| 1          | 102       |
| 2          | 101       |
- The same `student_id` can appear multiple times if they enroll in different courses.
- The same `course_id` can appear multiple times if it has different students.
- But **the combination of `student_id` and `course_id` is unique**, fulfilling the primary key requirement.

A foreign key is a column (or a group of columns) in a table that establishes a relationship between the data in two tables. It ensures referential integrity, meaning the values in the foreign key column(s) must match values in the referenced table's primary key (or a unique key).
e.g.
```sql
CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers (customer_id)
);

-- or
CREATE TABLE product(
	type_id INTEGER REFERENCES product_type(id),
	name VARCHAR(30) NOT NULL,
	supplier VARCHAR(30) NOT NULL,
	description TEXT NOT NULL,
	id SERIAL PRIMARY KEY);
```


### 4.Conditional Operators
1. Equal : =
2. Less than : <
3. greater than : >
4. less than or equal : <=
5. greater than or equal : >=
6. Not equal : <> or !=
It is generally use to filter data based on some condition
e.g.
```sql
SELECT * FROM customer WHERE age > 20;
```

### 5.Logical Operators
used to stack conditional operators.
1. AND
2. OR
3. NOT
e.g.
```sql
SELECT first_name 
FROM customer 
WHERE 
age > 20 AND birth_date > '2003-06-29';
```

### 6.ORDER BY
It is used to sort the data based on some column value.
e.g. 
```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column_name [ASC | DESC], column_name2 [ASC | DESC], ...;

-- increasing order by default
SELECT * FROM sales 
WHERE discount > 10
ORDER BY discount;

-- 
SELECT first_name, last_name, salary
FROM employees
ORDER BY 3 DESC; -- sort by 3rd column which is salary here

-- 
SELECT * 
FROM employees
ORDER BY salary DESC NULLS [LAST/FIRST];


```

### 7.LIMIT and OFFSET
used to constrain number of rows returned by query.
e.g.
```sql
SELECT column1, column2, ...
FROM table_name
LIMIT number_of_rows
[OFFSET start_position];


--
SELECT * 
FROM employees
ORDER BY employee_id
LIMIT 10 OFFSET 20;  -- get employees from 21 to 30 based on employee_id

```
### 8.CONCAT
used to concatenate multiple strings.
If value is NULL then it is treated as empty string
```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM employees;

--
SELECT first_name || ' ' || last_name AS full_name  
FROM employees;
--  || is act as concat

--
SELECT CONCAT_WS('-', '2024', '12', '15') AS formatted_date; 
-- Use CONCAT_WS (Concatenate with Separator) for concatenating with a specific delimiter:
```

### 9. AS
It is used to store result of operation into variable.
`AS` keyword is used to assign an **alias** to a column or table, making it easier to reference them in the query. Aliases are particularly useful for renaming columns in the result set or simplifying table names in complex queries.
When using aliases with spaces or special characters, enclose them in double quotes

### 10. GROUP BY
`GROUP BY` clause is used to **group rows that have the same values in specified columns** into summary rows, often used with aggregate functions like `COUNT`, `SUM`, `AVG`, `MIN`, or `MAX`. It helps to organize data into groups for performing calculations on each group.
```sql
SELECT column1, column2, aggregate_function(column3)
FROM table_name
GROUP BY column1, column2;
```
Columns in the `SELECT` clause must either:
- Appear in the `GROUP BY` clause, or
- Be used in an aggregate function.

### 11. HAVING
`HAVING` clause is used in conjunction with the `GROUP BY` clause to filter the results of aggregated data. While the `WHERE` clause filters rows before grouping, the `HAVING` clause filters after the grouping has occurred, specifically based on aggregate functions like `COUNT()`, `SUM()`, `AVG()`, etc.
- can't not be used without `GROUP BY`
```sql
SELECT column1, aggregate_function(column2)
FROM table_name
WHERE condition
GROUP BY column1
HAVING condition

-- 
SELECT salesperson_id, COUNT(*) AS total_sales
FROM sales
GROUP BY salesperson_id
HAVING COUNT(*) > 5;
-- This query groups the data by `salesperson_id`, counts the number of 
-- sales for each salesperson, and filters the results to include only 
-- those salespeople who made more than 5 sales.
```
### 12. DISTINCT
`DISTINCT` keyword is used to **remove duplicate rows** from the result set of a query. It ensures that only unique rows are returned based on the columns specified in the `SELECT` clause.
- can be used with aggregate functions.
```sql
SELECT DISTINCT column1, column2, ...
FROM table_name;

--
SELECT COUNT(DISTINCT department_id) AS unique_departments
FROM employees;

```
### 13. IN and NOT IN
`IN` operator is used to filter rows where a column’s value matches any value in a specified list or subquery. It is a shorthand for multiple `OR` conditions.
The `NOT IN` operator excludes rows with the specified values.
For the sub query NULL values might need to be handled.  
```sql
SELECT column1, column2
FROM table_name
WHERE column1 IN (value1, value2, ...);

SELECT column1, column2
FROM table_name
WHERE column1 IN (SELECT column1 FROM another_table);

---
SELECT first_name, last_name
FROM employees
WHERE department_id NOT IN (10, 20, 30);

```

### 14. Arithmetic Operators
1. Addition : +
2. Subtraction : -
3. Division : /
4. Integer Division : DIV
5. Modules : %



### 15. JOINS
**joins** are used to combine rows from two or more tables based on a related column between them. Joins enable you to query and analyze data spread across multiple tables.
![[Joins In Postgres.png]]

1. INNER JOIN :
	- Combines rows from both tables where there is a match in the specified condition.
	- Rows that do not meet the condition are excluded from the result.
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;

--
SELECT e.employee_id, e.first_name, d.department_name
FROM employees e
INNER JOIN departments d
ON e.department_id = d.department_id;
-- This query retrieves the employee ID, first name, and department name 
-- by joining the employees table with the departments table based on 
-- matching department IDs
-- If there are employees whose department_id does not match any department_id in the departments table, those employees will not appear in the result (because it's an INNER JOIN)
```

2. LEFT JOIN (LEFT OUTER JOIN):
	- Returns all rows from the left table and the matching rows from the right table.
	- If no match is found, `NULL` values are returned for the right table’s columns.
```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;

--
SELECT e.employee_id, e.first_name, d.department_name
FROM employees e
LEFT JOIN departments d
ON e.department_id = d.department_id;
-- Returns all employees, even if they are not assigned to a department.
```

3. RIGHT JOIN (RIGHT OUTER JOIN) :
	- Returns all rows from the right table and the matching rows from the left table.
	- If no match is found, `NULL` values are returned for the left table’s columns.
```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;

--
SELECT e.employee_id, e.first_name, d.department_name
FROM employees e
RIGHT JOIN departments d
ON e.department_id = d.department_id;
-- Returns all departments, even if no employees are assigned to them.
```


4. FULL JOIN :
	- Combines results of both `LEFT JOIN` and `RIGHT JOIN`.
	- Returns all rows from both tables, with `NULL` values for unmatched rows.
```sql
SELECT columns
FROM table1
FULL JOIN table2
ON table1.column = table2.column;

--
SELECT e.employee_id, e.first_name, d.department_name
FROM employees e
FULL JOIN departments d
ON e.department_id = d.department_id;
-- Returns all employees and all departments, even if there are no matches.
```

5. CROSS JOIN :
	- Produces the Cartesian product of two tables (every row from the first table is combined with every row from the second table).
```sql
SELECT columns
FROM table1
CROSS JOIN table2;

--
SELECT e.first_name, d.department_name
FROM employees e
CROSS JOIN departments d;
-- Every employee is paired with every department.

```

6. SELF JOIN :
	- A table is joined with itself, often used for hierarchical data or comparisons within the same table.

```sql
SELECT a.column1, b.column2
FROM table_name a
INNER JOIN table_name b
ON a.column = b.column;

--
SELECT e1.first_name AS Employee, e2.first_name AS Manager
FROM employees e1
INNER JOIN employees e2
ON e1.manager_id = e2.employee_id;
-- Finds employees and their managers from the same table.
```

7. NATURAL JOIN :
	- Automatically joins tables based on columns with the same name and compatible data types in both tables
```sql
SELECT columns
FROM table1
NATURAL JOIN table2;

--
SELECT *
FROM employees
NATURAL JOIN departments;
-- Joins `employees` and `departments` where column names are identical.
```

8. JOIN using `USING` Clause :
	- A JOIN with a USING clause is similar to a `NATURAL JOIN` but allows you to specify explicitly the columns to be used for the join. It joins the tables based on the specified columns and returns all rows where the values in those columns are equal.
	- It can be also used for `ON` clause.
```sql
SELECT columns
FROM table1
JOIN table2
USING (common_column);

--
SELECT * FROM 
employees e
INNER JOIN departments d 
USING (department_id);

SELECT * FROM
employees e 
INNER JOIN departments d 
ON e.department_id = d.id;
```

10. ANTI JOIN :
- An **ANTI JOIN** is used to retrieve rows from the left table that **do not have a corresponding match** in the right table. PostgreSQL does not have a direct `ANTI JOIN` syntax, but it can be achieved using a combination of a `LEFT JOIN` and a `WHERE` clause with `IS NULL` to filter out rows that do not match.
```sql
SELECT a.column1, a.column2
FROM table1 a
LEFT JOIN table2 b
ON a.column = b.column
WHERE b.column IS NULL;
-- In this query, we retrieve all rows from `table1` (left table) where 
-- there is no matching row in `table2` (right table).

--

SELECT e.first_name, e.last_name
FROM employees e
LEFT JOIN departments d
ON e.department_id = d.department_id
WHERE d.department_id IS NULL;
-- This query returns employees who are **not assigned to any department.
```

11. JOINS with Clause :

```sql
-- WHERE
SELECT e.first_name, d.department_name
FROM employees e
INNER JOIN departments d
ON e.department_id = d.department_id
WHERE d.location_id = 100;

-- GROUP BY
SELECT d.department_name, COUNT(e.employee_id) AS employee_count
FROM employees e
INNER JOIN departments d
ON e.department_id = d.department_id
GROUP BY d.department_name;

-- ORDER BY
SELECT e.first_name, d.department_name
FROM employees e
INNER JOIN departments d
ON e.department_id = d.department_id
ORDER BY d.department_name;
```

12. Performance Considerations :
	- 1. **Indexes**: Create indexes on columns used in `ON` conditions to speed up joins.
	- **Use Explicit Joins**: Avoid implicit joins (e.g., `SELECT * FROM table1, table2 WHERE ...`) for better clarity and performance.
	- **Analyze Query Plan**: Use `EXPLAIN` to analyze how PostgreSQL executes the query and optimize it
	 -
```sql
EXPLAIN SELECT e.first_name, d.department_name
FROM employees e
INNER JOIN departments d
ON e.department_id = d.department_id;
```

### 16. UNION and UNION ALL
The UNION operator is used to combine the results of two or more SELECT queries into a single result set. The UNION operator removes duplicates by default, while the UNION ALL operator keeps all the rows, including duplicates.
- All `SELECT` queries involved must have the **same number of columns** and the columns must have compatible data types.
```sql
SELECT columns
FROM table1
UNION
SELECT columns
FROM table2;

--
SELECT first_name FROM employees
UNION
SELECT first_name FROM contractors;
```
- `UNION` is useful when you want to combine all the rows from the queries without filtering out any duplicates.
```sql
SELECT columns
FROM table1
UNION ALL
SELECT columns
FROM table2;

--
SELECT first_name FROM employees
UNION ALL
SELECT first_name FROM contractors;
```

### 17. EXTRACT
`EXTRACT` function is used to retrieve a specific part of a date or time value, such as the year, month, day, hour, minute, etc.
```sql
EXTRACT(field FROM source)
```

- `field`: The part of the date or time to be extracted. Common fields include `YEAR`, `MONTH`, `DAY`, `HOUR`, `MINUTE`, `SECOND`, etc.
- `source`: The date or time value (a `DATE`, `TIME`, `TIMESTAMP`, or `INTERVAL`).
- Common `field` Values in `EXTRACT`

	- `YEAR`: Extracts the year part.
	- `MONTH`: Extracts the month part (1 to 12).
	- `DAY`: Extracts the day part (1 to 31).
	- `HOUR`: Extracts the hour part (0 to 23).
	- `MINUTE`: Extracts the minute part (0 to 59).
	- `SECOND`: Extracts the second part (0 to 59).
	- `DOW` (Day of Week): Extracts the day of the week (0 for Sunday, 6 for Saturday).
	- `DOY` (Day of Year): Extracts the day of the year (1 to 366).
	- `WEEK`: Extracts the week number of the year.
```sql
SELECT EXTRACT(YEAR FROM TIMESTAMP '2024-12-15');
SELECT EXTRACT(MONTH FROM TIMESTAMP '2024-12-15');
SELECT EXTRACT(DAY FROM TIMESTAMP '2024-12-15');
SELECT EXTRACT(HOUR FROM TIME '14:35:22');
SELECT EXTRACT(MINUTE FROM TIME '14:35:22');
SELECT EXTRACT(DOW FROM TIMESTAMP '2024-12-15');
SELECT EXTRACT(DOY FROM TIMESTAMP '2024-12-15');
SELECT EXTRACT(WEEK FROM TIMESTAMP '2024-12-15');

--
SELECT EXTRACT(YEAR FROM AGE('1990-06-15'::DATE));
```


### 18. IS NULL
We can not compare null with = we need to use `IS NULL` or `IS NOT NULL`
e.g.
```sql
SELECT * FROM customer
WHERE email IS NOT NULL;
```

### 19. SIMILAR AND LIKE (used as regex)
`SIMILAR TO` operator is used to perform pattern matching, similar to `LIKE`, but with more advanced regular expressions. It allows you to match strings using a regular expression-like syntax, giving you more flexibility than `LIKE` for complex patterns.
1. SIMILAR :
```sql
string SIMILAR TO pattern
```
- `string`: The string value to be matched.
- `pattern`: The pattern you're trying to match, which follows a regular expression syntax.
 `SIMILAR TO` uses a pattern that is similar to a regular expression, but with some differences:
- `.` matches any single character.
- `%` (similar to `LIKE`) matches any sequence of characters.
- `_` (similar to `LIKE`) matches a single character.
- `[]` is used to define a character class, like `[a-z]`.
- `|` is used for alternation (OR), e.g., `A|B` matches either `A` or `B`
- `*` can be used to match zero or more occurrences of a character, e.g., `A*` matches zero or more `A`s.
```sql
SELECT 'apple' SIMILAR TO '[a-z]+ple';  -- Matches "apple"
-- The pattern `'[a-z]+ple'` matches any string that ends with "ple", where -- the part before "ple" consists of one or more lowercase letters.
```
2. LIKE : 
	we have `LIKE` AND `NOT LIKE`
```sql
string LIKE pattern
```
- `string`: The string value to be matched.
- `pattern`: The pattern you're trying to match. It supports the use of two wildcard characters:
    - `%`: Matches any sequence of characters (including zero characters).
    - `_`: Matches a single character.
	e.g.
```sql
SELECT 'apple' LIKE 'a____';  -- Matches "apple"
-- The pattern `'a____'` matches any string that starts with "a" and is 
-- followed by exactly four characters.

SELECT 'apple' NOT LIKE 'a%';  -- Does not match "apple"
```

- To match % or _ we need to use `ESCAPE`
```sql 
string SIMILAR TO pattern ESCAPE escape_char;
string LIKE pattern ESCAPE escape_char;

SELECT 'a|b' SIMILAR TO 'a\|b' ESCAPE '\';
-- The vertical bar (`|`) is a special character for alternation in regular expressions, so it is escaped with the backslash (`\`).

SELECT '100% match' LIKE '100\% match' ESCAPE '\';
-- Here, the backslash (`\`) is used as the escape character, allowing `%` to be treated as a literal character rather than a wildcard.
```

### 20. Views
1. View - 
	- A _view_ is a _virtual table_ that is defined by a `SELECT` query. It doesn't store data itself, but rather provides a way to query data from one or more tables. Views can be used to simplify complex queries, improve security by exposing only specific columns or rows, and provide an abstraction layer over underlying tables. 
	- They are computed every time they are called, they do not store result data.
```sql
CREATE [ OR REPLACE ] [ TEMP | TEMPORARY ] [ RECURSIVE ] VIEW name [ ( column_name [, ...] ) ]
    [ WITH ( view_option_name [= view_option_value] [, ... ] ) ]
    AS query
    [ WITH [ CASCADED | LOCAL ] CHECK OPTION ]
```

```sql
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```
- `view_name`: The name you want to assign to the view.
- `SELECT` query: The query that defines the view. It can reference one or more tables and include joins, filtering, and aggregation.
	e.g.
```sql
CREATE VIEW department_view AS
SELECT department, COUNT(*) AS total_employees
FROM employees
GROUP BY department;
```
- Once a view is created, you can query it like a regular table:
```sql
SELECT * FROM view_name;
```
- To remove the view
```sql
DROP VIEW view_name;
```
- We can also replace view if it already exist
```sql
CREATE OR REPLACE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```
- Create a temporary view which is dropped after current session
```sql
CREATE TEMP VIEW temp_view AS SELECT * FROM employees;

```
- A `RECURSIVE` view s a view that can refer to itself within the query. This is especially useful for hierarchical or tree-structured data, like organizational charts or file systems. The recursive query typically uses a `Common Table Expression (CTE)` to define how the view should recurse.
```sql
CREATE RECURSIVE VIEW hierarchy AS
WITH RECURSIVE org_chart AS (
  SELECT employee_id, manager_id
  FROM employees
  WHERE manager_id IS NULL
  UNION ALL
  SELECT e.employee_id, e.manager_id
  FROM employees e
  JOIN org_chart o ON e.manager_id = o.employee_id
)
SELECT * FROM org_chart;
```
- `WITH` This clause allows you to define **options** for the view. These options influence the behavior of the view.
	- **`view_option_name`**: The name of the option.
	- **`view_option_value`**: The value for the option.
	A common option is `security_barrier`, Which ensures that the query in the view cannot be optimized in ways that would break security For example:
	There are other types of options too.
```sql
CREATE VIEW secure_view WITH (security_barrier=true) AS
SELECT * FROM sensitive_data;
```
- `[ WITH [ CASCADED | LOCAL ] CHECK OPTION` option specifies whether to enforce a **check** on data modification for views (such as `INSERT`, `UPDATE`, or `DELETE` operations).
	- **`CASCADED`** (default): The check option is applied recursively, meaning if a view is modified, the base tables behind it are also checked.
	- **`LOCAL`**: The check option applies only to the immediate view and does not propagate to the base tables.
	- **`CHECK OPTION`**: Ensures that any modification to the data that is done through the view must satisfy the conditions defined in the view's query. If the data doesn't match the `WHERE` clause of the view, the modification will fail.
```sql
CREATE VIEW active_employees AS
SELECT * FROM employees WHERE is_active = true
WITH CHECK OPTION;
-- In this case, any attempt to insert or update data through the 
-- active_employees view will be rejected if the row's is_active column 
-- is not true.
```
- Functions called in the view are treated the same as if they had been called directly from the query using the view. Therefore, the user of a view must have permissions to call all functions used by the view. Functions in the view are executed with the privileges of the user executing the query or the function owner, depending on whether the functions are defined as `SECURITY INVOKER` or `SECURITY DEFINER`
2. Materialized View -
	A **materialized view** is a type of view that stores the result of the query, unlike regular views which are calculated every time they are queried. Materialized views can be refreshed to keep the data up-to-date.
```sql
CREATE MATERIALIZED VIEW department_sales AS
SELECT department, SUM(sales) AS total_sales
FROM sales
GROUP BY department;

-- refresh 
REFRESH MATERIALIZED VIEW department_sales;

-- drop
DROP MATERIALIZED VIEW department_sales;
```
3. Advantages of views :
	- **Abstraction**: They can hide the complexity of queries and table structures from end users.
	- **Security**: You can grant access to views instead of base tables, controlling which data users can access.
	- **Reusability**: Complex queries can be encapsulated in views, allowing reuse without repeating the query logic.
4. Some rules for views
	- The view must have exactly one entry in its `FROM` list, which must be a table or another updatable view.
	- The view definition must not contain `WITH`, `DISTINCT`, `GROUP BY`, `HAVING`, `LIMIT`, or `OFFSET` clauses at the top level.
	- The view definition must not contain set operations (`UNION`, `INTERSECT` or `EXCEPT`) at the top level.
	- The view's select list must not contain any aggregates, window functions or set-returning functions. because 

### 21. SQL Functions
- Functions are set of SQL statements which performs the action and return the result.
- They can be used to encapsulate logic and simplify complex queries. PostgreSQL allows you to create both **built-in** functions (like `COUNT`, `AVG`, etc.) and **user-defined functions**.
- User defined functions can be created by users to perform custom operations, which can be written in SQL, PL/pgSQL (PostgreSQL's procedural language), or other languages like Python or C.
##### 1. Aggregate Functions :
**Aggregate functions** in SQL are used to perform calculations on multiple rows of a table and return a single result. These functions are commonly used with `GROUP BY` to aggregate data into summary results, such as totals, averages, counts, and more.
- **`COUNT()`** - Returns the number of rows.
- **`SUM()`** - Returns the sum of a numeric column.
- **`AVG()`** - Returns the average value of a numeric column.
- **`MIN()`** - Returns the smallest value in a column.
- **`MAX()`** - Returns the largest value in a column.
- **`STRING_AGG()`** - Concatenates values from multiple rows into a single string.
- **`ARRAY_AGG()`** - Collects the values of a column into an array.
- **`BOOL_AND()`** - Returns `TRUE` if all values in a group are `TRUE`.
- **`BOOL_OR()`** - Returns `TRUE` if at least one value in a group is `TRUE`
- **`MEDIAN()`** - Returns the median value from a set of values (available via extensions).
- **`VAR_POP()`** - Returns the population variance of a set of values.
- **`VAR_SAMP()`** - Returns the sample variance of a set of values.
- **`STDDEV_POP()`** - Returns the population standard deviation of a set of values.
- **`STDDEV_SAMP()`** - Returns the sample standard deviation of a set of values.
- **`JSON_AGG()`** - Aggregates values into a JSON array.
- **`JSONB_AGG()`** - Aggregates values into a JSONB array.
- **`XMLAGG()`** - Aggregates values into an XML document.
- **`REGR_SLOPE()`** - Computes the slope of the regression line.
- **`REGR_INTERCEPT()`** - Computes the intercept of the regression line.
- **`REGR_R2()`** - Computes the coefficient of determination for linear regression.
- **`REGR_AVGX()`** - Computes the average of the X values in a linear regression.
- **`REGR_AVGY()`** - Computes the average of the Y values in a linear regression.
- **`REGR_COUNT()`** - Counts the number of points used in a linear regression.
- `bit_length()` : Returns the number of bits in the binary representation of the value
```sql
SELECT 
    department,
    COUNT(*) AS total_employees,                    
     -- Count of employees in each department
    SUM(salary) AS total_salary,                     
    -- Sum of salaries in each department
    AVG(salary) AS avg_salary,                       
    -- Average salary in each department
    MIN(salary) AS lowest_salary,                    
    -- Minimum salary in each department
    MAX(salary) AS highest_salary,                   
    -- Maximum salary in each department
    STRING_AGG(employee_name, ', ') AS employee_names 
    -- Concatenate employee names in each department
FROM 
    employees
GROUP BY 
    department;
```
##### 2. String functions :
- `LENGTH()`: Returns the length of a string.
- `UPPER()`: Converts a string to uppercase.
- `LOWER()`: Converts a string to lowercase.
- `CONCAT()`: Concatenates two or more strings.
- `SUBSTRING()`: Extracts a substring from a string.
- `TRIM()`: Removes leading and trailing spaces from a string.
- `char_length(column_length` : Gives number of characters in string.
- `octet_length()` : Returns the number of bytes used to store the string (important for multibyte characters).

##### 3. Math's functions :
- `ABS()`: Returns the absolute value.
- `ROUND(val, decimal_places)`: Rounds a number to the nearest integer or specified decimal places.
- `CEIL()` / `FLOOR()`: Returns the smallest integer greater than or equal to the number / the largest integer less than or equal to the number.
- `POWER()`: Returns a number raised to the power of another number.
##### 4. Conditional Functions :
- `COALESCE()`: Returns the first non-NULL value in a list of arguments.
- `NULLIF()`: Returns NULL if two expressions are equal.
- `CASE`: Conditional expression that works like an `IF` statement.
```sql
SELECT CASE 
           WHEN salary > 50000 THEN 'High' 
           WHEN salary > 30000 THEN 'Medium' 
           ELSE 'Low' 
       END AS salary_range
FROM employees;
```
##### 5. JSON Functions :
used while working with JSON type
- `JSONB_ARRAY_LENGTH()`: Returns the number of elements in a JSON array.
- `JSONB_OBJECT_KEYS()`: Returns the keys of a JSON object.
- `JSONB_AGG()`: Aggregates JSON values into a JSON array.

##### 6. Window Function :
Window functions perform calculations across a set of table rows related to the current row, without collapsing the rows into a single result.

- `ROW_NUMBER()`: Assigns a unique number to each row in a result set.
- `RANK()`: Returns the rank of a row within a partition of a result set. Assigns a rank to rows within a partition, but rows with equal values receive the same rank, skipping subsequent ranks.
```sql
SELECT employee_name, department,
       ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS rank
FROM employees;
```

##### 7. Set Functions :
These functions operate on multiple sets of data.
- `UNION`: Combines results from multiple `SELECT` queries, removing duplicates.
- `INTERSECT`: Returns rows that appear in both result sets.
- `EXCEPT`: Returns rows from the first `SELECT` query that do not appear in the second query.
```sql
SELECT employee_name FROM employees WHERE department = 'HR'
INTERSECT
SELECT employee_name FROM employees WHERE salary > 70000;

--

SELECT employee_name FROM employees WHERE department = 'HR'
EXCEPT
SELECT employee_name FROM employees WHERE salary < 70000;
```

##### 8. User Defined :
Synopsis - 
```sql
CREATE [ OR REPLACE ] FUNCTION
    _`name`_ ( [ [ _`argmode`_ ] [ _`argname`_ ] _`argtype`_ [ { DEFAULT | = } _`default_expr`_ ] [, ...] ] )
    [ RETURNS _`rettype`_
      | RETURNS TABLE ( _`column_name`_ _`column_type`_ [, ...] ) ]
  { LANGUAGE _`lang_name`_
    | TRANSFORM { FOR TYPE _`type_name`_ } [, ... ]
    | WINDOW
    | { IMMUTABLE | STABLE | VOLATILE }
    | [ NOT ] LEAKPROOF
    | { CALLED ON NULL INPUT | RETURNS NULL ON NULL INPUT | STRICT }
    | { [ EXTERNAL ] SECURITY INVOKER | [ EXTERNAL ] SECURITY DEFINER }
    | PARALLEL { UNSAFE | RESTRICTED | SAFE }
    | COST _`execution_cost`_
    | ROWS _`result_rows`_
    | SUPPORT _`support_function`_
    | SET _`configuration_parameter`_ { TO _`value`_ | = _`value`_ | FROM CURRENT }
    | AS '_`definition`_'
    | AS '_`obj_file`_', '_`link_symbol`_'
    | _`sql_body`_
  } ...
```
e.g.
```sql
CREATE OR REPLACE FUNCTION fn_add_ints(int, int)
RETURNS int AS
'SELECT $1 + $2;'
LANGUAGE SQL;
-- with $ sign we can access passed parameters to function.
-- use above function
SELECT fn_add_ints(4,5);
DROP fn_add_ints
--

-- sometimes we need to use '' inside our sql so to define body of function we can use $body$
CREATE OR REPLACE FUNCTION fn_add_ints(int, int)
RETURNS int AS
$body$
SELECT $1 + $2;
$body$
LANGUAGE SQL;  -- for SQL we dont have BEGIN and END
```

```sql
-- we can use $$ instead of $body$
CREATE FUNCTION get_full_name(first_name text, last_name text)
RETURNS text AS 
$$
BEGIN
  RETURN first_name || ' ' || last_name; 
  -- can not use SELECT, instead RETURN for plpgsql
END;   -- ; is not complusory
$$ 
LANGUAGE plpgsql;  -- PL/pgSQL
-- use 
SELECT get_full_name('John', 'Doe');
```
- Return Type :
	- **Returning a scalar value**: The function can return a single value, like text, integer, etc.
		e.g. `void`, `int`, `text`, `numeric`, `varchar`, `SETOF <>`
	- **Returning a set of rows**: The function can return a set of rows, like a table.
```sql
CREATE FUNCTION get_employees_by_department(dept_id INT)
RETURNS TABLE(employee_id INT, employee_name TEXT) AS 
$$
BEGIN
  RETURN QUERY
  SELECT id, name FROM employees WHERE department_id = dept_id;
  -- SELECT can be used with RETURN QUERY
END;
$$ 
LANGUAGE plpgsql;
--
CREATE FUNCTION get_employees_by_department(dept_id INT)
RETURNS SETOF employees AS 
$$
BEGIN
  RETURN QUERY
  SELECT * FROM employees WHERE department_id = dept_id;
  -- SELECT can be used with RETURN QUERY
END;
$$ 
LANGUAGE plpgsql;

-- use
SELECT * FROM get_employees_by_department(1));
```
- Creating function in other language :
```sql
CREATE FUNCTION double_integer(n INT)
RETURNS INT AS 
$$
    return n * 2
$$ 
LANGUAGE plpythonu; -- plpythonu means python
```
- `(function_name).*` gives result of function in table format, if a table is return type of function.
- `(function_name).column_name` gives result of column of returned table.
```sql
CREATE FUNCTION get_employees_by_department(dept_id INT)
RETURNS employees AS 
$$
BEGIN
  RETURN QUERY
  SELECT * FROM employees WHERE department_id = dept_id;
END;
$$ 
LANGUAGE plpgsql;

-- use
SELECT * FROM (get_employees_by_department(1)).*;
SELECT * FROM (get_employees_by_department(1)).employee_name;
```
- Variables in function can be declared using `DECLARE`
```sql
CREATE OR REPLACE FUNCTION fn_add_ints(a int, b int)
RETURNS int AS
$$
DECLARE  -- only for plpgsql not for SQL
	ans int;
BEGIN
	ans := a + b;
	 -- Assign the sum of the parameters to the variable RETURN ans;
	RETURN ans;
END;
$$
LANGUAGE plpgsql

--

CREATE OR REPLACE FUNCTION get_random_value(min_val int, max_val int)
RETURNS int AS
$$
DECLARE
	rand int;
BEGIN
	SELECT random()*(max_val-min_val) + min_val INTO rand;
	-- INTO used to store result of query into declared variable
	RETURN rand;
END
$$
LANGUAGE plpgsql

SELECT get_random_value(1, 50);
```
- Store rows in variables using `RECORD` type
```sql
CREATE OR REPLACE get_random_employee()
RETURN varchar AS
$$
DECLARE
	rand int,
	emp RECORD;
BEGIN
	SELECT random()*(5-1) + 1 INTO rand;
	SELECT * FROM employee INTO emp WHERE id = rand;
	RETURN CONCAT(emp.first_name + ' ' + emp.last_name);
END
$$
LANGUAGE plpgsql

SELECT get_random_employee();
```
- `IN`, `INOUT`, and `OUT` in functions
	- `IN` is the default mode. It allows input data to be passed to the function but doesn't allow the function to modify the value.
	- `OUT` parameters are used to return values. You don't explicitly return anything with `RETURN` when using `OUT`.
	- `INOUT` parameters work both as input and output. They are passed into the function with initial values and can be modified inside the function to provide output.
	
```sql
CREATE OR REPLACE FUNCTION get_sum_and_difference(IN a INT, IN b INT, OUT sum_result INT, OUT diff_result INT)
AS $$
BEGIN
    sum_result := a + b;
    diff_result := a - b;
END;
$$ 
LANGUAGE plpgsql;

-- Call the function
SELECT * FROM get_sum_and_difference(10, 5);

CREATE OR REPLACE FUNCTION demo_parameters( IN a INT, INOUT b INT, OUT c INT ) AS 
$$ 
BEGIN 
	b := b * 2; -- Modify the INOUT parameter 
	c := a + b; -- Set the OUT parameter 
END; 
$$ 
LANGUAGE plpgsql;
```
- `IF`-`ELSE` in functions, `CASE` can also be used.
```sql
CREATE OR REPLACE FUNCTION check_num(num int)
RETURN varchar AS
$$
BEGIN
	IF num > 0 THEN
		RETURN '+ve';
	ELSEIF num < 0 THEN
		RETURN '-ve';
	ELSE 
		RETURN 'zero';
	END IF;
END;
$$
LANGUAGE plpgsql
--
CREATE OR REPLACE FUNCTION check_num(num int)
RETURN varchar AS
$$
BEGIN
	CASE
		WHEN num > 0 THEN
			RETURN '+ve';
		WHEN num < 0 THEN
			RETURN '-ve';
		ELSE 
			RETURN 'zero';
	END CASE;
END;
$$
LANGUAGE plpgsql
```
- Loops in functions can be used to iterate over rows, numbers, or custom logic
```sql
-- Loop with Exit Condition
CREATE OR REPLACE FUNCTION fn_loop_with_exit_condition(max_num int)
RETURN int AS
$$
DECLARE
	j int DEFAULT 1;
	total_sum int DEFAULT 0;
BEGIN
	LOOP
		total_sum := total_sum + j;
		j := j + 1;
		EXIT WHEN j > max_num
	END LOOP;
	RETURN total_sum
END;
$$
LANGUAGE plpgsql
```

```sql
-- FOR LOOP SYNTAX
FOR counter_name IN start_value .. end_value BY stepping
LOOP
	-- statements
END LOOP;

-- example
CREATE OR REPLACE FUNCTION fn_for_loop(max_num int)
RETURNS int AS
$$
DECLARE
	total_sum int DEFAULT 0;
BEGIN
	FOR i IN 1 .. max_num BY 1     -- increment i by 1
	LOOP
		total_sum := total_sum + i;
	END LOOP;
	RETURN total_sum;
END;
$$
LANGUAGE plpgsql

--

CREATE OR REPLACE FUNCTION fn_for_loop(max_num int)
AS
$$
BEGIN
	FOR i IN REVERSE max_num .. 1 BY 1     -- decrement i by 1
	LOOP
		RAISE NOTICE 'Number: %', i;
	END LOOP;
END;
$$
LANGUAGE plpgsql

--
-- loop over rows returned by a query using the `FOR` loop.
CREATE OR REPLACE FUNCTION loop_employees()
RETURNS VOID 
LANGUAGE plpgsql
AS $$
DECLARE
    emp RECORD;
BEGIN
    FOR emp IN SELECT id, name FROM employees 
    LOOP
        RAISE NOTICE 'Employee: ID = %, Name = %', emp.id, emp.name;
    END LOOP;
END;
$$;
```

- `RAISE NOTICE` is acting as print statement.
- `DO` Block allow us to write procedural language (pl/pgSQL) without using functions.
```sql
DO
$$
DECLARE
	-- variables
BEGIN
	-- statements
END;
$$ LANGUAGE plpgsql
```
- Arrays in postgreSQL 
```sql
SELECT ARRAY[1, 2, 3, 4];  -- Creates a one-dimensional array
SELECT ARRAY[]::INT[];  -- Creates an empty array of integers
```

```sql
-- FOREACH Loop
DO
$$
DECLARE
	arr int[] := ARRAY[1,2,3];
	i int;
BEGIN
	FOREACH i IN ARRAY arr
	LOOP
		RAISE NOTICE '%', i;
	END LOOP;
END;
$$ LANGUAGE plpgsql
```

```sql
-- WHILE LOOP
DO
$$
DECLARE
	counter int DEFAULT 1;
	sum int DEFAULT 0;
BEGIN
	WHILE j <= 10
	LOOP
		sum := sum + j;
		j := j + 1;
	END LOOP;
	RAISE NOTICE 'Sum = %', sum;
END;
$$ LANGUAGE plpgsql
```

```sql
-- CONTINUE and EXIT
DO
$$
DECLARE
	i INT DEFAULT 1;
BEGIN
	LOOP
		i := i+1;
		EXIT WHEN i > 10;
		CONTINUE WHEN MOD(i, 2) = 0;
		RAISE NOTICE '%', i;
	END LOOP;
END;
$$ LANGUAGE plpgsql

--
DO
$$ 
DECLARE 
	counter INT := 1; 
BEGIN 
	LOOP 
		RAISE NOTICE 'Counter: %', counter; 
		counter := counter + 1; 
		-- Exit condition 
		IF counter > 5 THEN 
			EXIT; 
		END IF; 
	END LOOP; 
END; 
$$ LANGUAGE plpgsql;
```
- Function overloading means you can define multiple functions with the same name but different argument types. PostgreSQL distinguishes them based on the number or types of arguments.
```sql
CREATE FUNCTION multiply(a INT, b INT)
RETURNS INT AS $$
BEGIN
  RETURN a * b;
END;
$$ LANGUAGE plpgsql;

CREATE FUNCTION multiply(a FLOAT, b FLOAT)
RETURNS FLOAT AS $$
BEGIN
  RETURN a * b;
END;
$$ LANGUAGE plpgsql;
```
- `DROP FUNCTION` to delete
	**If multiple overloads exist**: You must specify the parameter types to delete the specific version of the function.
```sql
DROP FUNCTION function_name;  -- if no parameters
DROP FUNCTION IF EXISTS function_name(TEXT, TEXT, TEXT);
```

### 22. Stored Procedures 
A **stored procedure** in PostgreSQL is a precompiled set of SQL and procedural logic that is stored in the database and can be executed by name. It allows expanding the capabilities of functions by allowing transaction control (e.g., `COMMIT` or `ROLLBACK`).
- Key Features :
	1. They can be executed by the application, which has access to database.
	2. Procedures can execute transactions(`COMMIT` and `ROLLBACK`) within the procedure body.
	3. Procedures can't be called by `SELECT`.
	4. They do not return any value, but there is workaround. But we can use `return;` in procedure to exit it. 
	1. Reusability - Procedures are stored in the database and can be reused to avoid repetitive code.
	2. Procedures can accept input, output, or input-output parameters.
	3. Procedures can be executed with the privileges of the owner or caller.
	4. Procedure without any parameters is called _static_ procedure and with parameters is called _dynamic_ procedure.
- Synopsis :
```sql
CREATE [ OR REPLACE ] PROCEDURE
    _`name`_ ( [ [ _`argmode`_ ] [ _`argname`_ ] _`argtype`_ [ { DEFAULT | = } _`default_expr`_ ] [, ...] ] )
  { LANGUAGE _`lang_name`_
    | TRANSFORM { FOR TYPE _`type_name`_ } [, ... ]
    | [ EXTERNAL ] SECURITY INVOKER | [ EXTERNAL ] SECURITY DEFINER
    | SET _`configuration_parameter`_ { TO _`value`_ | = _`value`_ | FROM CURRENT }
    | AS '_`definition`_'
    | AS '_`obj_file`_', '_`link_symbol`_'
    | _`sql_body`_
  } ...

-- 

CREATE [ OR REPLACE ] PROCEDURE procedure_name ( [ argument_name data_type [ IN | OUT | INOUT ] [, ...] ] )
LANGUAGE language_name
AS $$
DECLARE
	-- variables 
BEGIN
    -- Procedure Body
END;
$$;
```

e.g.
```sql
CREATE OR REPLACE PROCEDURE add_employee(emp_name TEXT, emp_salary NUMERIC)
LANGUAGE plpgsql   -- the language sec. can be added in last like function
AS $$
BEGIN
    INSERT INTO employees (name, salary)
    VALUES (emp_name, emp_salary);
    COMMIT;  -- not complusory 
END;
$$;

--
CALL add_employee('John Doe', 50000);   -- execution 
```

- Using transaction control in procedure :
```sql
CREATE OR REPLACE PROCEDURE update_employee_salary(emp_id INT, new_salary NUMERIC)
LANGUAGE plpgsql
AS $$
BEGIN
    BEGIN
        UPDATE employees
        SET salary = new_salary
        WHERE id = emp_id;
        -- Commit the transaction if the update succeeds
        COMMIT;
    EXCEPTION WHEN OTHERS THEN
        -- Rollback the transaction if an error occurs
        ROLLBACK;
        RAISE NOTICE 'Error occurred during update.';
    END;
END;
$$;
```

- `IN`, `INOUT`, `OUT` in procedure example :
```sql
CREATE OR REPLACE PROCEDURE manage_employee_salary(
    emp_id INT,                  
     -- IN parameter (employee ID)
    INOUT salary_adjustment NUMERIC, 
    -- INOUT parameter (adjustment to salary)
    OUT total_count INT           
    -- OUT parameter (total number of employees)
)
LANGUAGE plpgsql
AS $$
BEGIN
    -- Update the employee salary based on the INOUT parameter
    UPDATE employees
    SET salary = salary + salary_adjustment
    WHERE id = emp_id;

    -- Return the new salary via the INOUT parameter
    SELECT salary INTO salary_adjustment
    FROM employees
    WHERE id = emp_id;

    -- Calculate the total number of employees and return it via the OUT parameter
    SELECT COUNT(*) INTO total_count
    FROM employees;
END;
$$;

-- calling procedure
CALL manage_employee_salary(1, 2000, total_count);
```

- Calling procedure :
```sql
CALL procedure_name(parameter1, parameter2, ...);
```

- Note :
	To replace the current definition of an existing procedure, use `CREATE OR REPLACE PROCEDURE`. It is not possible to change the name or argument types of a procedure this way (if you tried, you would actually be creating a new, distinct procedure).

	When `CREATE OR REPLACE PROCEDURE` is used to replace an existing procedure, the ownership and permissions of the procedure do not change. All other procedure properties are assigned the values specified or implied in the command. You must own the procedure to replace it (this includes being a member of the owning role).
	
- Difference Between procedure and functions :

| **Aspect**          | **Function**                                        | **Procedure**                                |
| ------------------- | --------------------------------------------------- | -------------------------------------------- |
| Transaction Control | Cannot include `COMMIT` or `ROLLBACK`.              | Supports `COMMIT` and `ROLLBACK`.            |
| Returns Values      | Returns a single value or table using `RETURN`.     | Uses `OUT` or `INOUT` parameters for output. |
| Invocation          | Called in a `SELECT`, `FROM`, or other SQL context. | Called with `CALL`.                          |
| Use Case            | Best for computations and transformations.          | Best for performing database operations.     |

### 23. Triggers
 - A **trigger** in PostgreSQL is a special kind of stored procedure that is automatically executed (or "fired") in response to specific events on a table, foreign table or view. Triggers allow you to define custom actions that are executed when certain changes occur in the database, such as inserting, updating, or deleting data.
 - They can be executed _before_, _after_ and _instead_ of an event.
 - We can have multiple triggers and they will be executed on alphabetical order for that table, foreign table or view.
 - Can't be triggered manually by user.
 - Do not accept any parameters.
![[Triggers in postgres.png]]

- `ROW`: The trigger is fired for each row affected by the operation.
- `STATEMENT`: The trigger is fired once for the entire SQL statement, regardless of how many rows are affected.

- Synopsis :
```sql
CREATE [ OR REPLACE ] [ CONSTRAINT ] TRIGGER _`name`_ { BEFORE | AFTER | INSTEAD OF } { _`event`_ [ OR ... ] }
    ON _`table_name`_
    [ FROM _`referenced_table_name`_ ]
    [ NOT DEFERRABLE | [ DEFERRABLE ] [ INITIALLY IMMEDIATE | INITIALLY DEFERRED ] ]
    [ REFERENCING { { OLD | NEW } TABLE [ AS ] _`transition_relation_name`_ } [ ... ] ]
    [ FOR [ EACH ] { ROW | STATEMENT } ]
    [ WHEN ( _`condition`_ ) ]
    EXECUTE { FUNCTION | PROCEDURE } _`function_name`_ ( _`arguments`_ )

where _`event`_ can be one of:

    INSERT
    UPDATE [ OF _`column_name`_ [, ... ] ]
    DELETE
    TRUNCATE

--

CREATE TRIGGER trigger_name
	{BEFORE | AFTER} {event}  -- Event : insert, update, delete, truncate
ON table_name
	[FOR [EACH] {ROW | STATEMENT}]
		EXECUTE {PROCEDURE | FUNCTION}  
```

e.g.
```sql
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,  
    name VARCHAR(100),        
    salary NUMERIC NOT NULL,
    department VARCHAR(50),
    hired_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE employee_log (
    log_id SERIAL PRIMARY KEY,
    emp_id INT,
    old_salary NUMERIC,
    new_salary NUMERIC,
    changed_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
--
CREATE OR REPLACE FUNCTION log_salary_update()
RETURNS TRIGGER AS 
$$
BEGIN
    INSERT INTO employee_log (emp_id, old_salary, new_salary)
    VALUES (NEW.id, OLD.salary, NEW.salary);
    RAISE NOTICE "Trigger name : %", TG_NAME;
    RETURN NEW;  -- Required to continue the UPDATE operation
END;
$$ LANGUAGE plpgsql;
-- `NEW`: Refers to the new row (after the update).
-- `OLD`: Refers to the old row (before the update).
--
CREATE TRIGGER salary_update_trigger
AFTER UPDATE OF salary
ON employees
FOR EACH ROW
EXECUTE FUNCTION log_salary_update();
-- trigger will be fired after the `salary` field of any row in the 
-- `employees` table is updated. It will insert a record into the 
-- `employee_log` table with the employee ID, old salary, new salary, and  
-- timestamp
```

- `TG_NAME` is used to get the name of trigger inside trigger body.
- `TG_TABLE_NAME` gives table name on which we are working
- `TG_OP` gives operation we are performing
- `TG_WHEN` gives when it is executed
- `TG_LEVEL` gives is it for row or statement
- `TG_TABLE_SCHEMA` gives table schema we are working on
- PostgreSQL temporarily retains the **before-update values** (`OLD`) alongside the **after-update values** (`NEW`) in memory for the trigger to access.
- View all trigger's in database
```sql
SELECT tgname, tgrelid::regclass, tgtype, tgenabled
FROM pg_trigger;
```
- Delete trigger
```sql
DROP TRIGGER trigger_name ON table_name;
```
 
 - Important Considerations :
	1. **Performance Impact**: Triggers, especially `AFTER` triggers and `FOR EACH ROW` triggers, can impact performance because they add additional operations to each data modification.
	2. **Error Handling**: If a trigger function raises an exception, the operation (INSERT, UPDATE, DELETE) will be aborted unless you specifically handle the error in the trigger function.
	3. **Recursion**: Be cautious of recursive triggers, where a trigger causes another trigger to fire. This can lead to infinite loops.
e.g.
Let say we want that people should not be abled to update record on weekend.
```sql
CREATE OR REPLACE FUNCTION fn_block_weekend_change()
RETURN TRIGGER
LANGUAGE plpgsql
AS
$$
BEGIN
	RAISE NOTICE 'NO database changes allowed on the weekend'
	RETURN NULL;    -- Required for statement-level triggers
END
$$;

CREATE TRIGGER tr_block_weekend_changes
	BEFORE UPDATE OR INSERT OR DELETE OR TRUNCATE
	ON employees
	FOR EACH STATEMENT
	WHEN(
		EXTRACT('DOW' FROM CURRENT_TIMESTAMP) BETWEEN 6 AND 7
	)
EXECUTE FUNCTION fn_block_weekend_change();

```


### 24. Cursors
- Cursors are used to step forward or backward through rows of data. 
- cursors are used to retrieve query results row by row rather than all at once. This is especially useful for handling large datasets where fetching all rows at once could consume too much memory.
- How they work ? 
1. **Declare**: Define the cursor with a SQL query.
```sql
DECLARE cursor_name [{ FOR | NO SCROLL }] CURSOR(arguments) [{WITH HOLD}] FOR query;
```
- `FOR`: Specifies the SQL query whose results the cursor will process.
- `NO SCROLL`: Prevents backward navigation in the cursor.
- `WITH HOLD` : Persist after a transaction ends
- `arguments` are used in cursor query.

2. **Open**: Make the cursor ready for use.
```sql
OPEN cursor_name;
```

3. **Fetch**: Retrieve rows one at a time or in batches.
```sql
FETCH [ direction { FROM | IN } ] cursor_name;
```
- `direction`:
	- `NEXT` (default): Fetches the next row.
	- `PRIOR`: Fetches the previous row.
	- `FIRST`: Fetches the first row.
	- `LAST`: Fetches the last row.
	- `ABSOLUTE n`: Fetches the `n`'th row.
	- `RELATIVE n`: Fetches `n` rows forward/backward from the current position.
4. **`MOVE`** command in PostgreSQL is used with cursors to change the cursor's position within the result set without fetching any rows. It is helpful when you want to reposition the cursor for later operations, like `FETCH`, without retrieving data immediately.
```sql
MOVE [ direction ] [ FROM | IN ] cursor_name;
```
5. **Close**: Close the cursor to release resources.
```sql
CLOSE cursor_name;
```

- Bound Cursor :
	- A **bound cursor** is tied to a specific query when it is declared.
	- The query is fixed, and you cannot dynamically change it later.
- Unbounded Cursor :
	- An **unbound cursor** does not have a query assigned at the time of declaration.
	- Instead, you assign a query dynamically using the `OPEN` statement.
```sql
-- bounded
DECLARE bound_cursor SCROLL CURSOR FOR SELECT * FROM employee;

-- unbounded
DECLARE cursor_name CURSOR WITHOUT QUERY;
OPEN cursor_name FOR query;
```
6. `EXECUTE` over cursor :
```sql
OPEN _`unbound_cursorvar`_ [ [ NO ] SCROLL ] FOR EXECUTE _`query_string`_
                                     [ USING _`expression`_ [, ... ] ];

--
-- e.g.
PREPARE dynamic_query AS
SELECT id, name, salary
FROM employees
WHERE salary > $1;

DECLARE emp_cursor CURSOR FOR EXECUTE dynamic_query(55000);
```
e.g.
```sql
DO
$body$
	DECLARE
		msg text DEFAULT '';
		rec_customer record;
		-- Declare cursor with customer data
		cur_customers CURSOR
		FOR
			SELECT * FROM customer;
	BEGIN
		-- Open cursor
		OPEN cur_customers;
		LOOP
			-- Fetch records from cursor
			FETCH cur_customers INTO rec_customer;
			-- Loop until nothing more is found
			EXIT WHEN NOT FOUND;
			-- Concatenates all customer names together
			msg := msg || rec_customer.first_name || ' ' || rec_customer.last_name || ', ';
		END LOOP;
	RAISE NOTICE 'Customers : %', msg;
	END;
$body$
```

- UPDATE and DELETE using cursor :
	When a cursor is positioned on a table row, that row can be updated or deleted using the cursor to identify the row. There are restrictions on what the cursor's query can be (in particular, no grouping) and it's best to use `FOR UPDATE` in the cursor
```sql
UPDATE table_name
SET column_name = value
WHERE CURRENT OF cursor_name;
--
DELETE FROM table_name
WHERE CURRENT OF cursor_name;
```


### 25. More Constraints

1. CHECK constraints :
	A check constraint is the most generic constraint type. It allows you to specify that the value in a certain column must satisfy a Boolean (truth-value) expression. For instance, to require positive product prices, you could use:
```sql
CREATE TABLE products (
    product_no integer,
    name text,
    price numeric CHECK (price > 0)
);

-- You can also give the constraint a separate name.
CREATE TABLE products (
    product_no integer,
    name text,
    price numeric CONSTRAINT positive_price CHECK (price > 0)
);
-- The third one uses a new syntax. It is not attached to a particular 
-- column, instead it appears as a separate item in the comma-separated 
-- column list.
CREATE TABLE products (
    product_no integer,
    name text,
    price numeric CHECK (price > 0),
    discounted_price numeric CHECK (discounted_price > 0),
    CHECK (price > discounted_price)
);
```

2. UNIQUE constraints :
	Unique constraints ensure that the data contained in a column, or a group of columns, is unique among all the rows in the table. The syntax is:
```sql
CREATE TABLE products (
    product_no integer UNIQUE,
    name text,
    price numeric
);

CREATE TABLE products (
    product_no integer,
    name text,
    price numeric,
    UNIQUE (product_no)
);

CREATE TABLE example (
    a integer,
    b integer,
    c integer,
    UNIQUE (a, c)
);

-- NULL values are not considered unique, to consider them 
-- use NULLS NOT DISTINCT
CREATE TABLE products (
    product_no integer UNIQUE NULLS NOT DISTINCT,
    name text,
    price numeric
);
```

3. Exclusion constraint :
	Exclusion constraints ensure that if any two rows are compared on the specified columns or expressions using the specified operators, at least one of these operator comparisons will return false or null. Adding an exclusion constraint will automatically create an index of the type specified in the constraint declaration. The syntax is:
```sql
EXCLUDE [ USING _`index_method`_ ] ( _`exclude_element`_ WITH _`operator`_ [, ... ] ) _`index_parameters`_ [ WHERE ( _`predicate`_ ) ]``

CREATE TABLE circles (
    c circle,
    EXCLUDE USING gist (c WITH &&)
);
```








### 26. Miscellaneous
1. ALTER Queries - 
```sql
ALTER TABLE customer
ALTER COLUMN sex TYPE sex_type USING sex::sex_type;
-- here I am changing column sex to type sex_type and also specifying specific type
ALTER TABLE table_name ALTER COLUMN column_nam TYPE new_type;

-- add column
ALTER TABLE table_name ADD column_name data_type;

-- add constraint e.g. make it not null
ALTER TABLE table_name ALTER COLUMN column_name SET NOT NULL;

-- change column name
ALTER TABLE table_name RENAME COLUMN old_name TO new_name;

-- drop column
ALTER TABLE table_name DROP COLUMN column_name;

--rename table
ALTER TABLE table_name RENAME TO new_name;

```
2. DEFAULT - used to set the default type when none is provided
```sql
CREATE TABLE temp(
name VARCHAR(50) NOT NULL
state CHAR(2) NOT NULL DEFAULT='MH'
)
```
3. Custom data type :
```sql
CREATE TYPE sex_type as enum ('M', 'F');
```
4. Create Index :
```sql
-- we are creating index called index_name on table table_name for column column_name of the table.
CREATE INDEX index_name ON table_name(column_name);

-- creating index for multiple tables
CREATE INDEX index_name ON table_name(column_1, column_2);

```
5. Delete data from table : 
```sql
TRUNCATE TABLE table_name;  -- delete all data
```
6. Delete table :
```sql
DROP TABLE table_name;
```

# References
1. [PostgreSQL official docs](https://www.postgresql.org/docs/ )
2. [Postgres Tutorial YT](https://youtu.be/85pG_pDkITY?si=0mFdTUjI2Fro3ze1)
