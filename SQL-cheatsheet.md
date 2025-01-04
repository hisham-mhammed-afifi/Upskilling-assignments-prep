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

#### **Subqueries**

- **Subquery in `WHERE`**: Query inside another query
  ```sql
  SELECT * FROM table WHERE column = (SELECT column FROM table WHERE condition);
  ```
- **Subquery in `FROM`**: Subquery used as a table
  ```sql
  SELECT * FROM (SELECT column FROM table WHERE condition) AS subquery;
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
- **`PRIMARY KEY`**: Unique identifier for a row
  ```sql
  CREATE TABLE table (id INT PRIMARY KEY);
  ```
- **`FOREIGN KEY`**: Link between tables
  ```sql
  CREATE TABLE table (id INT, foreign_id INT, FOREIGN KEY (foreign_id) REFERENCES other_table(id));
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

---
