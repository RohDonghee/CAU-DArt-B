# 1. SQL Syntax Order

SELECT<br>
FROM <br>
WHERE<br>
GROUP BY<br>
HAVING<br>
ORDER BY <br>

# 2. SQL Parsing order core clauses

## 2-1 FROM : Identify source tables

### ■ JOIN : Merge tables
#### What is a Join Key?
A **join key** is the column (or set of columns) used to combine rows from two or more tables.  
In relational databases, this is typically a **Primary Key ↔ Foreign Key** relationship.  
- <b>Primary Key (PK)</b>: uniquely identifies a row in a table. In a DBMS tool, we can verify whether a column is a primary key by the '🔑' icon.
- <b>Foreign Key (FK)</b>: references the primary key of another table, establishing a relationship. <br>
  
Example <br>
```MySQL 
SELECT *
FROM   USED_GOODS_BOARD AS A
INNER JOIN USED_GOODS_REPLY AS B
       ON A.BOARD_ID = B.BOARD_ID
WHERE  A.CREATED_DATE BETWEEN '2022-10-01' AND '2022-10-31'
ORDER BY B.CREATED_DATE ASC, A.TITLE ASC;
```

### ■ ON : Apply JOIN conditions
Example <br>
```MySQL
SELECT u.*, o.*
FROM tb_user as A
INNER 
JOIN tb_office as B 
ON A.user_no = B.user_no;
```


## 2-2 WHERE : Condition

### ■ LIKE ```SELECT * FROM TABLE WHERE NAME LIKE '라면'```

## 2-3 GROUP BY : Group rows by specific columns
- The `GROUP BY` clause groups rows that have the same values in specified columns into summary rows.  
- Often used together with aggregate functions like:
  - `COUNT()`
  - `SUM()`
  - `AVG()`
  - `MAX()`
  - `MIN()`

## 2-4 HAVING : Filter groups 
- HAVING is generally used with GROUP BY <br>
- After using GROUP BY, set the condition <br>

## 2-5 SELECT : Select output columns
### ■ CASE WHEN 
- multiple conditon
- If columns correspond to plural condition, follow prior conditon 
```MySQL
SELECT
  CASE
  WHEN conditon1 THEN ['if conditon1 is True']
  WHEN condition2 THEN ['if condition2 is True']
  ELSE ['other condition']
END AS [new_column_name]
FROM [table_name]
```
### ■ IF
- one condition
```MySQL
SELECT
IF ([condition], ['True Val'], ['False Val']) AS [new_column_name] 
```


## 2-6 ORDER BY : Sort the result set (ASC, DESC)
- ASC : 오름차순 / DESC : 내림차순
- When using multiple columns in `ORDER BY`, <b>the leftmost column has the highest priority</b>
- SQL sorts the result set from left to right in the order specified.
- If two rows have the same value for the first column, the next column is used as a **tie-breaker**, and so on. <br>
Example
```sql
SELECT name, LENGTH(name) AS len, id
FROM users
ORDER BY len DESC, id ASC;
