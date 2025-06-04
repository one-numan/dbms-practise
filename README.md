# dbms-practise
To use ChatGPT canvas and get this as a Markdown document, you'll need to log in to ChatGPT.

However, here's the extended cheat sheet in **Markdown format** with additional commands:

---

# 🐬 MySQL SQL Cheat Sheet (Markdown)

## 📚 Database Operations

```sql
-- Create a database
CREATE DATABASE dbname;

-- Show all databases
SHOW DATABASES;

-- Select a database to use
USE dbname;

-- Delete a database
DROP DATABASE dbname;

-- Rename a database (manual method)
ALTER DATABASE old_name MODIFY NAME = new_name; -- Note: not supported in all MySQL versions
```

---

## 🗃️ Table Operations

```sql
-- Create a table
CREATE TABLE table_name (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Show all tables
SHOW TABLES;

-- Describe table structure
DESCRIBE table_name;
EXPLAIN table_name;

-- Rename a table
RENAME TABLE old_table TO new_table;

-- Delete a table
DROP TABLE table_name;

-- Truncate table (delete all data but keep structure)
TRUNCATE TABLE table_name;

-- Alter table: add column
ALTER TABLE table_name ADD column_name DATATYPE;

-- Alter table: modify column
ALTER TABLE table_name MODIFY column_name NEW_DATATYPE;

-- Alter table: drop column
ALTER TABLE table_name DROP COLUMN column_name;

-- Add primary key
ALTER TABLE table_name ADD PRIMARY KEY (column_name);

-- Add foreign key
ALTER TABLE table_name ADD CONSTRAINT fk_name
FOREIGN KEY (column_name) REFERENCES other_table(column_name);
```

---

## ✍️ Data Operations (CRUD)

```sql
-- Insert data
INSERT INTO table_name (column1, column2) VALUES ('value1', 'value2');

-- Insert multiple rows
INSERT INTO table_name (column1, column2) VALUES
('val1', 'val2'),
('val3', 'val4');

-- Select all data
SELECT * FROM table_name;

-- Select specific columns
SELECT column1, column2 FROM table_name;

-- Update data
UPDATE table_name SET column1 = 'new_value' WHERE id = 1;

-- Delete data
DELETE FROM table_name WHERE id = 1;

-- Replace data (insert or update)
REPLACE INTO table_name (id, column1) VALUES (1, 'new_val');
```

---

## 🔍 Query Filtering

```sql
-- WHERE clause
SELECT * FROM table_name WHERE column = 'value';

-- Comparison operators
=, !=, <>, >, <, >=, <=

-- BETWEEN
SELECT * FROM table_name WHERE column BETWEEN 10 AND 20;

-- IN
SELECT * FROM table_name WHERE column IN ('val1', 'val2');

-- LIKE and wildcards
SELECT * FROM table_name WHERE column LIKE 'A%'; -- starts with A

-- IS NULL
SELECT * FROM table_name WHERE column IS NULL;

-- Logical operators
AND, OR, NOT
```

---

## 🧾 Sorting and Limiting

```sql
-- Order by column
SELECT * FROM table_name ORDER BY column ASC;
SELECT * FROM table_name ORDER BY column DESC;

-- Limit results
SELECT * FROM table_name LIMIT 10;

-- Pagination
SELECT * FROM table_name LIMIT 10 OFFSET 20;
```

---

## 🔁 Joins

```sql
-- INNER JOIN
SELECT a.*, b.*
FROM table1 a
JOIN table2 b ON a.id = b.a_id;

-- LEFT JOIN
SELECT a.*, b.*
FROM table1 a
LEFT JOIN table2 b ON a.id = b.a_id;

-- RIGHT JOIN
SELECT a.*, b.*
FROM table1 a
RIGHT JOIN table2 b ON a.id = b.a_id;

-- FULL OUTER JOIN (MySQL workaround using UNION)
SELECT * FROM table1
LEFT JOIN table2 ON table1.id = table2.id
UNION
SELECT * FROM table1
RIGHT JOIN table2 ON table1.id = table2.id;
```

---

## 📊 Aggregate Functions

```sql
-- Basic aggregates
SELECT COUNT(*), SUM(column), AVG(column), MIN(column), MAX(column) FROM table_name;

-- Group by
SELECT column, COUNT(*) FROM table_name GROUP BY column;

-- Having clause (after GROUP BY)
SELECT column, COUNT(*) FROM table_name
GROUP BY column
HAVING COUNT(*) > 1;
```

---

## 📌 Subqueries

```sql
-- Subquery in SELECT
SELECT name, (SELECT COUNT(*) FROM orders WHERE user_id = users.id) AS order_count FROM users;

-- Subquery in WHERE
SELECT * FROM products WHERE category_id IN (SELECT id FROM categories WHERE active = 1);
```

---

## 🛡️ User Management (MySQL-Specific)

```sql
-- Create new user
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';

-- Grant privileges
GRANT ALL PRIVILEGES ON dbname.* TO 'username'@'localhost';

-- Revoke privileges
REVOKE ALL PRIVILEGES ON dbname.* FROM 'username'@'localhost';

-- Drop user
DROP USER 'username'@'localhost';

-- Show current user
SELECT USER();

-- Show grants for a user
SHOW GRANTS FOR 'username'@'localhost';

-- Apply privilege changes
FLUSH PRIVILEGES;
```

---

## 🧪 Indexes

```sql
-- Create index
CREATE INDEX idx_column ON table_name(column);

-- Unique index
CREATE UNIQUE INDEX idx_unique ON table_name(column);

-- Drop index
DROP INDEX idx_column ON table_name;

-- Show indexes
SHOW INDEXES FROM table_name;
```

---

## 📈 Performance & Debugging

```sql
-- Explain query
EXPLAIN SELECT * FROM table_name WHERE column = 'value';

-- Show running processes
SHOW PROCESSLIST;

-- Kill process
KILL process_id;
```

---

| Command        | Description                                                        |
| -------------- | ------------------------------------------------------------------ |
| `\g`           | End and execute the current statement (same as `;`)                |
| `\G`           | End and execute the current statement, show results **vertically** |
| `\c`           | Cancel the current input/query buffer                              |
| `\e`           | Open default system editor to edit current input                   |
| `\p`           | Print the current query buffer without running it                  |
| `\s`           | Show current connection and status info                            |
| `\T filename`  | Output results to a file (`tee`)                                   |
| `\t`           | Disable writing output to file (stop tee)                          |
| `\!`           | Execute a system shell command                                     |
| `\P pager`     | Set the pager (e.g., `less`, `more`, or custom)                    |
| `\n`           | Enable/disable column names in result (toggle)                     |
| `\q` or `exit` | Quit MySQL client                                                  |



Got it! Since we've already covered common and advanced **basic SQL commands**, here’s a curated list of **lesser-known but powerful SQL features**, especially those **unique or advanced in MySQL** that are often overlooked.

---

## 🧮 1. **CASE Expressions**

```sql
SELECT name,
       CASE 
           WHEN age < 18 THEN 'Minor'
           WHEN age BETWEEN 18 AND 64 THEN 'Adult'
           ELSE 'Senior'
       END AS age_group
FROM people;
```

* Acts like `if-else` for SQL queries.
* Very useful for derived columns or conditional logic.

---

## ⛓️ 2. **Common Table Expressions (CTEs)** – MySQL 8.0+

```sql
WITH recent_orders AS (
    SELECT * FROM orders WHERE order_date > CURDATE() - INTERVAL 7 DAY
)
SELECT * FROM recent_orders WHERE total > 100;
```

* Cleaner queries, especially with **subqueries**, **recursive logic**, etc.

---

## 🔄 3. **Recursive CTEs** – For hierarchical data

```sql
WITH RECURSIVE category_path (id, name, parent_id) AS (
  SELECT id, name, parent_id FROM categories WHERE id = 5
  UNION ALL
  SELECT c.id, c.name, c.parent_id
  FROM categories c
  INNER JOIN category_path cp ON cp.parent_id = c.id
)
SELECT * FROM category_path;
```

* Useful for **tree structures**, such as categories, menus, organizational charts.

---

## 🧾 4. **JSON Functions in MySQL**

```sql
-- Store JSON
INSERT INTO products (info) VALUES ('{"color":"red","size":"L"}');

-- Query JSON
SELECT info->>'$.color' AS color FROM products;

-- Update JSON field
UPDATE products SET info = JSON_SET(info, '$.color', 'blue');
```

* MySQL has full **JSON** support including `JSON_EXTRACT`, `JSON_ARRAY`, `JSON_OBJECT`, etc.

---

## 🔎 5. **FULLTEXT Search**

```sql
-- Enable full-text index
ALTER TABLE articles ADD FULLTEXT(title, body);

-- Use MATCH AGAINST
SELECT * FROM articles
WHERE MATCH(title, body) AGAINST('MySQL fulltext' IN NATURAL LANGUAGE MODE);
```

* Useful for **basic text search** without external search engines.

---

## ⏱️ 6. **Generated (Virtual) Columns**

```sql
CREATE TABLE users (
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    full_name VARCHAR(100) GENERATED ALWAYS AS (CONCAT(first_name, ' ', last_name)) STORED
);
```

* Automatically computed values, **no need to update manually**.

---

## 🔁 7. **Stored Procedures**

```sql
DELIMITER //

CREATE PROCEDURE GetUsersByAge(IN min_age INT)
BEGIN
  SELECT * FROM users WHERE age >= min_age;
END //

DELIMITER ;

CALL GetUsersByAge(25);
```

* Useful for reusable logic on the **database server** side.

---

## 🚦 8. **Triggers**

```sql
CREATE TRIGGER before_insert_user
BEFORE INSERT ON users
FOR EACH ROW
SET NEW.created_at = NOW();
```

* Automate actions **before/after** insert, update, or delete.

---

## 🔒 9. **Views**

```sql
CREATE VIEW active_users AS
SELECT id, name FROM users WHERE is_active = 1;

-- Use like a table
SELECT * FROM active_users;
```

* Acts like a **virtual table**, great for abstraction and reuse.

---

## 🔗 10. **Index Hints**

```sql
SELECT * FROM users USE INDEX (idx_name) WHERE age > 30;
```

* Control **which index** MySQL should use, for performance tuning.

---
Perfect — let’s take this further with concise examples and explanations for:

* ✅ **Window Functions**
* ✅ **Event Scheduler**
* ✅ **Optimizer Hints**

These are **powerful tools** in MySQL 8.0+ that can drastically improve how you write and optimize SQL.

---

## 🪟 1. **Window Functions** (MySQL 8.0+)

Window functions perform **calculations across rows related to the current row**, without collapsing them (unlike `GROUP BY`).

### 🔹 Example: Running Total

```sql
SELECT 
  employee_id,
  department,
  salary,
  SUM(salary) OVER (PARTITION BY department ORDER BY salary) AS running_total
FROM employees;
```

### 🔹 Useful Window Functions

| Function                         | Description                           |
| -------------------------------- | ------------------------------------- |
| `ROW_NUMBER()`                   | Row number in partition               |
| `RANK()` / `DENSE_RANK()`        | Ranking (with/without gaps)           |
| `LAG()` / `LEAD()`               | Previous or next row's value          |
| `FIRST_VALUE()` / `LAST_VALUE()` | Value from the start/end of partition |
| `NTILE(n)`                       | Divides rows into n buckets           |

---

These are powerful tools in MySQL 8.0+ that can drastically improve how you write and optimize SQL.

🪟 1. Window Functions (MySQL 8.0+)
Window functions perform calculations across rows related to the current row, without collapsing them (unlike GROUP BY).

🔹 Example: Running Total
sql
Copy
Edit
SELECT 
  employee_id,
  department,
  salary,
  SUM(salary) OVER (PARTITION BY department ORDER BY salary) AS running_total
FROM employees;
🔹 Useful Window Functions
Function	Description
ROW_NUMBER()	Row number in partition
RANK() / DENSE_RANK()	Ranking (with/without gaps)
LAG() / LEAD()	Previous or next row's value
FIRST_VALUE() / LAST_VALUE()	Value from the start/end of partition
NTILE(n)	Divides rows into n buckets



## ⏱️ 2. **Event Scheduler** (MySQL's built-in job scheduler)

Like a lightweight cron job **inside MySQL**.

### 🔹 Enable Event Scheduler

```sql
SET GLOBAL event_scheduler = ON;
```

### 🔹 Create a Recurring Event

```sql
CREATE EVENT archive_old_orders
ON SCHEDULE EVERY 1 DAY
DO
  DELETE FROM orders WHERE order_date < CURDATE() - INTERVAL 30 DAY;
```

### 🔹 One-Time Event Example

```sql
CREATE EVENT send_reminder_email
ON SCHEDULE AT CURRENT_TIMESTAMP + INTERVAL 10 MINUTE
DO
  CALL send_email_reminders();
```

---

## ⚙️ 3. **Optimizer Hints** (Control MySQL execution plan)

Optimizer hints help guide the query planner for performance.

### 🔹 Example: Force Index Usage

```sql
SELECT /*+ INDEX(users idx_age) */ * FROM users WHERE age > 30;
```

### 🔹 Other Hints

| Hint                         | Example                                                        |
| ---------------------------- | -------------------------------------------------------------- |
| `STRAIGHT_JOIN`              | `SELECT /*+ STRAIGHT_JOIN */ ...` – Use joins in written order |
| `JOIN_ORDER`                 | `/*+ JOIN_ORDER(t1, t2, t3) */` – Control join sequence        |
| `NO_ICP(t)`                  | `/*+ NO_ICP(t1) */` – Disable index condition pushdown         |
| `QB_NAME(qb)`                | Label query blocks for other hints                             |
| `DERIVED_CONDITION_PUSHDOWN` | Push WHERE into derived tables manually                        |

---


