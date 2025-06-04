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

