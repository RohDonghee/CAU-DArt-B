# Syntex 
## SQL Syntax Order

SELECT<br>
FROM <br>
WHERE<br>
GROUP BY<br>
HAVING<br>
ORDER BY <br>



## SQL Parsing order 핵심 절(core clauses)
FROM : Identify source tables

ON : Apply join conditions
```SELECT u.*, o.*
FROM tb_user as A
INNER 
JOIN tb_office as B 
ON A.user_no = B.user_no;
```
### JOIN : Merge tables
#### What is a Join Key?
A **join key** is the column (or set of columns) used to combine rows from two or more tables.  
In relational databases, this is typically a **Primary Key ↔ Foreign Key** relationship.  
- <b>Primary Key (PK)</b>: uniquely identifies a row in a table. In a DBMS tool, we can verify whether a column is a primary key by the '🔑' icon.
- <b>Foreign Key (FK)</b>: references the primary key of another table, establishing a relationship.  
#### Example
```
SELECT *
FROM   USED_GOODS_BOARD AS A
INNER JOIN USED_GOODS_REPLY AS B
       ON A.BOARD_ID = B.BOARD_ID
WHERE  A.CREATED_DATE BETWEEN '2022-10-01' AND '2022-10-31'
ORDER BY B.CREATED_DATE ASC, A.TITLE ASC;
```
### WHERE : Condition
#### LIKE ```SELECT * FROM TABLE WHERE NAME LIKE '라면'```


### GROUP BY : Group rows by specific columns
- The `GROUP BY` clause groups rows that have the same values in specified columns into summary rows.  
- Often used together with aggregate functions like:
  - `COUNT()`
  - `SUM()`
  - `AVG()`
  - `MAX()`
  - `MIN()`

### HAVING : Filter groups 
- HAVING is generally used with GROUP BY <br>
- After using GROUP BY, set the condition <br>

SELECT : Select output columns

DISTINCT : Remove duplicates

### ORDER BY : Sort the result set (ASC, DESC)
- ASC : 오름차순 / DESC : 내림차순
- When using multiple columns in `ORDER BY`, <b>the leftmost column has the highest priority</b>
- SQL sorts the result set from left to right in the order specified.
- If two rows have the same value for the first column, the next column is used as a **tie-breaker**, and so on.
#### Example
```sql
SELECT name, LENGTH(name) AS len, id
FROM users
ORDER BY len DESC, id ASC;
