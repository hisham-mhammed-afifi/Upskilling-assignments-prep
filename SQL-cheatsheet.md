### **SQL Cheat Sheet**

#### **Basic Structure**

- **`SELECT`**: Retrieve data
  ```sql
  SELECT column1, column2 FROM table;
  ```
- **`INSERT INTO`**: Add data
  ```sql
  INSERT INTO table (column1, column2) VALUES (value1, value2);
  ```
- **`UPDATE`**: Modify data
  ```sql
  UPDATE table SET column1 = value1 WHERE condition;
  ```
- **`DELETE FROM`**: Remove data
  ```sql
  DELETE FROM table WHERE condition;
  ```

#### **Database Management**

- **`CREATE DATABASE`**: Create a new database
  ```sql
  CREATE DATABASE database_name;
  ```
- **`USE`**: Select a database to work with
  ```sql
  USE database_name;
  ```
- **`SHOW DATABASES`**: List all databases
  ```sql
  SHOW DATABASES;
  ```
- **`DROP DATABASE`**: Delete a database
  ```sql
  DROP DATABASE database_name;
  ```

#### **Schemas**

- **`CREATE SCHEMA`**: Define a new schema
  ```sql
  CREATE SCHEMA schema_name;
  ```
- **`USE`**: Switch to a specific schema
  ```sql
  USE schema_name;
  ```
- **`DROP SCHEMA`**: Delete a schema
  ```sql
  DROP SCHEMA schema_name;
  ```
- **`SHOW SCHEMAS`**: List available schemas
  ```sql
  SHOW SCHEMAS;
  ```

#### **Filtering**

- **`WHERE`**: Filter rows
  ```sql
  SELECT * FROM table WHERE column = value;
  ```
- **`AND`, `OR`**: Combine conditions
  ```sql
  SELECT * FROM table WHERE column1 = value1 AND column2 = value2;
  ```
- **`BETWEEN`**: Range of values
  ```sql
  SELECT * FROM table WHERE column BETWEEN value1 AND value2;
  ```
- **`IN`**: Match multiple values
  ```sql
  SELECT * FROM table WHERE column IN (value1, value2, value3);
  ```
- **`LIKE`**: Pattern matching
  ```sql
  SELECT * FROM table WHERE column LIKE 'A%';
  ```
- **`IS NULL` / `IS NOT NULL`**: Handle null values
  ```sql
  SELECT * FROM table WHERE column IS NULL;
  ```

#### **Sorting**

- **`ORDER BY`**: Sort results
  ```sql
  SELECT * FROM table ORDER BY column ASC;
  ```
- **`DESC`**: Sort in descending order
  ```sql
  SELECT * FROM table ORDER BY column DESC;
  ```

#### **Aggregations**

- **`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`**: Aggregate functions
  ```sql
  SELECT COUNT(*), AVG(column) FROM table;
  ```
- **`GROUP BY`**: Group rows
  ```sql
  SELECT column, COUNT(*) FROM table GROUP BY column;
  ```
- **`HAVING`**: Filter groups
  ```sql
  SELECT column, COUNT(*) FROM table GROUP BY column HAVING COUNT(*) > 1;
  ```

#### **Joins**

- **`INNER JOIN`**: Match rows from both tables
  ```sql
  SELECT * FROM table1 INNER JOIN table2 ON table1.id = table2.id;
  ```
- **`LEFT JOIN`**: All rows from the left table, matched with right table rows
  ```sql
  SELECT * FROM table1 LEFT JOIN table2 ON table1.id = table2.id;
  ```
- **`RIGHT JOIN`**: All rows from the right table, matched with left table rows
  ```sql
  SELECT * FROM table1 RIGHT JOIN table2 ON table1.id = table2.id;
  ```
- **`FULL JOIN`**: All rows from both tables
  ```sql
  SELECT * FROM table1 FULL JOIN table2 ON table1.id = table2.id;
  ```
- **`CROSS JOIN`**: Cartesian product of two tables
  ```sql
  SELECT * FROM table1 CROSS JOIN table2;
  ```
- **Self-Join**: Join a table with itself
  ```sql
  SELECT A.column1, B.column2 FROM table A, table B WHERE A.common_column = B.common_column;
  ```

#### **Subqueries**

- **Subquery in `WHERE`**: Query inside another query
  ```sql
  SELECT * FROM table WHERE column = (SELECT column FROM table WHERE condition);
  ```
- **Subquery in `FROM`**: Subquery used as a table
  ```sql
  SELECT * FROM (SELECT column FROM table WHERE condition) AS subquery;
  ```
- **Correlated Subquery**: Dependent on the outer query
  ```sql
  SELECT column FROM table A WHERE EXISTS (SELECT 1 FROM table B WHERE B.column = A.column);
  ```

#### **Set Operations**

- **`UNION`**: Combine results from two queries, removing duplicates
  ```sql
  SELECT column FROM table1 UNION SELECT column FROM table2;
  ```
- **`UNION ALL`**: Combine results including duplicates
  ```sql
  SELECT column FROM table1 UNION ALL SELECT column FROM table2;
  ```
- **`INTERSECT`**: Return only rows that appear in both queries
  ```sql
  SELECT column FROM table1 INTERSECT SELECT column FROM table2;
  ```
- **`EXCEPT`**: Return rows from the first query that are not in the second
  ```sql
  SELECT column FROM table1 EXCEPT SELECT column FROM table2;
  ```

#### **Advanced Functions**

- **`CASE`**: Conditional logic in queries
  ```sql
  SELECT column,
         CASE
           WHEN condition1 THEN result1
           WHEN condition2 THEN result2
           ELSE result3
         END AS alias
  FROM table;
  ```
- **`COALESCE`**: Return the first non-null value
  ```sql
  SELECT COALESCE(column1, column2, 'default') FROM table;
  ```
- **Window Functions**: Perform calculations across a set of rows
  ```sql
  SELECT column, RANK() OVER (PARTITION BY column ORDER BY column DESC) AS rank FROM table;
  ```

#### **Working with Strings**

- **`CONCAT`**: Combine strings
  ```sql
  SELECT CONCAT(column1, ' ', column2) FROM table;
  ```
- **`LENGTH`**: Get the length of a string
  ```sql
  SELECT LENGTH(column) FROM table;
  ```
- **`SUBSTRING`**: Extract part of a string
  ```sql
  SELECT SUBSTRING(column FROM 1 FOR 5) FROM table;
  ```
- **`TRIM`**: Remove spaces from both ends
  ```sql
  SELECT TRIM(column) FROM table;
  ```
- **`UPPER` / `LOWER`**: Change case
  ```sql
  SELECT UPPER(column), LOWER(column) FROM table;
  ```

#### **Working with Dates**

- **`CURRENT_DATE`**: Current date
  ```sql
  SELECT CURRENT_DATE;
  ```
- **`DATE_ADD` / `DATE_SUB`**: Add or subtract time
  ```sql
  SELECT DATE_ADD(CURRENT_DATE, INTERVAL 1 DAY);
  ```
- **`DATEDIFF`**: Difference between dates
  ```sql
  SELECT DATEDIFF(end_date, start_date);
  ```
- **`EXTRACT`**: Extract parts of a date
  ```sql
  SELECT EXTRACT(YEAR FROM date_column) FROM table;
  ```

#### **Creating Tables & Constraints**

- **`CREATE TABLE`**: Define a new table
  ```sql
  CREATE TABLE table_name (column1 datatype, column2 datatype);
  ```
- **`ALTER TABLE`**: Modify table structure
  ```sql
  ALTER TABLE table ADD column datatype;
  ALTER TABLE table DROP COLUMN column;
  ```
- **`DROP TABLE`**: Delete a table
  ```sql
  DROP TABLE table_name;
  ```
- **Constraints**:
  - **`PRIMARY KEY`**: Unique identifier for a row
    ```sql
    CREATE TABLE table (id INT PRIMARY KEY);
    ```
  - **`FOREIGN KEY`**: Link between tables
    ```sql
    CREATE TABLE table (id INT, foreign_id INT, FOREIGN KEY (foreign_id) REFERENCES other_table(id));
    ```
  - **`CHECK`**: Ensure column values meet a condition
    ```sql
    CREATE TABLE table (id INT, column INT CHECK (column > 0));
    ```
  - **`DEFAULT`**: Set default values
    ```sql
    CREATE TABLE table (id INT, column INT DEFAULT 0);
    ```

#### **Indexes and Views**

- **`CREATE INDEX`**: Create an index for faster searching
  ```sql
  CREATE INDEX idx_column ON table (column);
  ```
- **`DROP INDEX`**: Remove an index
  ```sql
  DROP INDEX idx_column;
  ```
- **`CREATE VIEW`**: Create a virtual table
  ```sql
  CREATE VIEW view_name AS SELECT column1, column2 FROM table;
  ```
- **`DROP VIEW`**: Delete a view
  ```sql
  DROP VIEW view_name;
  ```

#### **Transactions**

- **`START TRANSACTION`**: Begin a transaction
  ```sql
  START TRANSACTION;
  ```
- **`COMMIT`**: Commit the transaction
  ```sql
  COMMIT;
  ```
- **`ROLLBACK`**: Rollback the transaction
  ```sql
  ROLLBACK;
  ```

#### **Performance Tips**

- **Use Indexes**: Optimize frequently queried columns.
- **Avoid `SELECT *`**: Specify only necessary columns.
- **Limit Rows for Testing**: Use `LIMIT` for sample data.
- **Normalize Data**: Break data into related tables.
- **Analyze Queries**: Use `EXPLAIN` to optimize query execution.
- **Batch Updates**: Process large updates in chunks.
- **Caching**: Use query result caching for repeated queries.

---
