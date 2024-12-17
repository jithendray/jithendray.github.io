---

tags: sql

---
# SQL Joins

## What are Joins?

SQL **joins** are used to combine rows from two or more tables based on a related column between them. They allow querying data across multiple tables in a relational database.

# Types of Joins

## Inner Join

- Combines rows from two tables where there is a match in the specified columns.
- Unmatched rows are excluded.

### Syntax

```sql
SELECT a.column1, b.column2  
FROM table1 a  
INNER JOIN table2 b  
ON a.common_column = b.common_column;
```

### When to Use

- To retrieve records with data present in both tables.
- Common for finding relationships like orders belonging to customers.

### Important Notes
- Filters unmatched rows; make sure the match condition is correct.

---

## Left Join (Left Outer Join)
- Returns all rows from the left table and matching rows from the right table. Unmatched rows in the left table are filled with NULLs.

### Syntax

```sql
SELECT a.column1, b.column2  
FROM table1 a  
LEFT JOIN table2 b  
ON a.common_column = b.common_column;
```

### When to Use
- To include all records from one table regardless of matching data in the second table.
- Useful for checking missing relationships.

### Important Notes
- Can result in NULL values for unmatched rows from the right table.

---

## Right Join (Right Outer Join)

- Returns all rows from the right table and matching rows from the left table. Unmatched rows in the right table are filled with NULLs.

### Syntax

```sql
SELECT a.column1, b.column2  
FROM table1 a  
RIGHT JOIN table2 b  
ON a.common_column = b.common_column;
```

### When to Use

- To include all records from the second table regardless of matches in the first.

---

## Full Outer Join

- Returns all rows from both tables, with NULLs for unmatched rows in either table.

### Syntax

```sql
SELECT a.column1, b.column2  
FROM table1 a  
FULL OUTER JOIN table2 b  
ON a.common_column = b.common_column;
```

### When to Use

- To combine all data while identifying mismatches between two tables.

### Important Notes

- Rarely used in performance-critical queries due to the potential size of the output.

---

## Cross Join

- Produces a Cartesian product where each row from the first table is combined with every row from the second table.

### Syntax

```sql
SELECT a.column1, b.column2  
FROM table1 a  
CROSS JOIN table2 b;
```

### When to Use

- Used when every combination of rows is required.
- Typically paired with conditions to reduce row explosion.

---

## Self Join

- A table is joined with itself by treating it as two separate tables.

### Syntax

```sql
SELECT a.column1, b.column2  
FROM table1 a  
JOIN table1 b  
ON a.column1 = b.column2;
```

### When to Use

- To find hierarchical relationships, like parent-child relationships in the same table.

---

## Natural Join

- Automatically joins tables on columns with the same name and compatible data types.

### Syntax

```sql
SELECT *  
FROM table1  
NATURAL JOIN table2;
```

### When to Use

- When column names and data types match exactly between tables.

### Important Notes

- Can be error-prone if unintended columns are included in the join.

---

# Advanced Joins

## Hash Join

- Uses a hash table to quickly match rows between two tables.
- Common in large data processing and data warehouses.

### When to Use

- When both tables are large, and join conditions are on equality (e.g., `a.id = b.id`).

---

## Nested Loop Join

- For every row in one table, the database scans matching rows in another table.
- Inefficient for large datasets but useful for smaller tables.

### When to Use

- When one table is small and the other is large.

---

## Broadcast Join

- Copies (or "broadcasts") a small table to every node in a distributed system to join it with a large table.

### When to Use

- In distributed databases like Spark SQL or BigQuery.
- When the smaller table fits in memory.

---

## SMB (Sort-Merge-Broadcast) Join

- Combines sorting, merging, and broadcasting for distributed systems.
- Useful in data-intensive frameworks like Apache Spark.

---

# Key Considerations When Using Joins

## Performance

- Joining large datasets can be computationally expensive.
- Always ensure proper indexing on join columns for efficient lookups.

## Filtering Before Joins

- Always filter data using `WHERE` or `ON` conditions before joining to reduce the number of rows processed.

## Avoiding Cartesian Products

- Be cautious with `CROSS JOIN` or missing join conditions as they create large, unnecessary datasets.

---

# Common Gotchas and Edge Cases

## NULL Handling

- NULL values can cause unexpected results in joins.
- Use `IS NULL` or `IS NOT NULL` explicitly when dealing with outer joins.

## Duplicates in Joins

- Ensure no unintended duplicate rows by checking primary keys or using `DISTINCT`.

## Join Order

- Join order can impact performance. Always join smaller tables first if possible.

## Mismatched Data Types

- Columns in the `ON` clause must have compatible data types.

---

# When to Use Which Join?

| Join Type       | When to Use                                                                           |
| --------------- | ------------------------------------------------------------------------------------- |
| Inner Join      | When only matching rows are required.                                                 |
| Left Join       | When you want all rows from the left table, regardless of matches in the right table. |
| Right Join      | When you want all rows from the right table, regardless of matches in the left table. |
| Full Outer Join | When you need all rows from both tables, including non-matching ones.                 |
| Cross Join      | When all combinations of rows are required.                                           |
| Self Join       | When rows in the same table need to relate to each other.                             |
| Hash Join       | For equality-based joins in large datasets.                                           |
| Broadcast Join  | For distributed joins where one table is significantly smaller than the other.        |
