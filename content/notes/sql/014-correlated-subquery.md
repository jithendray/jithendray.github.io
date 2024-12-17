---

tags: sql

---
# Correlated Sub-query in SQL

### What is a Correlated Sub-query?

A **correlated subquery** is a subquery that depends on values from the outer query for its execution. It is evaluated once for each row in the outer query, making it row-specific.

Unlike regular (non-correlated) subqueries, a correlated subquery cannot be executed independently because it references columns from the outer query.

### General Syntax

```sql
SELECT column1, column2
FROM table1 t1
WHERE (
    SELECT aggregate_function(column3)
    FROM table2 t2
    WHERE t2.columnX = t1.columnX
) = some_value;

```

### Example: Finding a User's 3rd Transaction Without a Window Function

#### Query using SELF-JOIN:

```sql
SELECT t1.user_id, t1.spend, t1.transaction_date
FROM transactions t1
JOIN transactions t2
ON t1.user_id = t2.user_id
WHERE t2.transaction_date <= t1.transaction_date
GROUP BY t1.user_id, t1.spend, t1.transaction_date
HAVING COUNT(*) = 3;
```

#### Query using Correlated Subquery:

```sql
SELECT t1.user_id, t1.spend, t1.transaction_date
FROM transactions t1
WHERE (
	SELECT COUNT(*)
	FROM transactions t2
	WHERE t2.user_id = t1.user_id
	AND t2.transaction_date <= t1.transaction_date
) = 3;
```

Explanation:
- Outer Query (t1): Iterated through each row in the transactions table
- Correlated Subquery (t2): for every row in outer query, counts how many transactions for the same user occurred on or before the transaction date of the current transaction (t1.transaction_date)
- Outer query filters the rows where the subquery count is 3. This indicates the row corresponds to the user's 3rd transaction

### When to Use Correlated Subqueries

1. **Row-Specific Logic**:
    
    - When the logic for a row in the outer query requires calculating a value dynamically based on other rows in the same or a related table.
2. **Complex Filtering**:
    
    - To filter rows based on aggregates or comparisons that are not directly available in the table, such as finding rows based on a sequential count or range.
3. **Replacing Window Functions**:
    
    - In cases where window functions (like `ROW_NUMBER()`, `RANK()`, etc.) are unavailable or not allowed, correlated subqueries can provide similar functionality.
4. **Avoiding Explicit Joins**:
    
    - When you don’t want to explicitly write self-joins but still need to compare rows within the same table.

### Advantages

- **Simplicity**:
    - Can sometimes be easier to understand or write compared to explicit joins or derived tables.
- **Flexibility**:
    - Handles row-specific logic that might otherwise require multiple joins or additional tables.
- **Reduced Code Overhead**:
    - No need to materialize intermediate results or write extensive groupings.

### Disadvantages

- **Performance**:
    - Correlated subqueries are evaluated for each row in the outer query, leading to potentially poor performance for large datasets.
    - May not leverage indexes as effectively as joins or window functions.
- **Complexity with Scaling**:
    - Becomes inefficient when datasets grow, as the subquery runs multiple times.


### When _Not_ to Use Correlated Subqueries

1. **Large Datasets**:
    - They can lead to performance bottlenecks due to repeated evaluation for each row in the outer query.
2. **When Window Functions are Available**:
    - Window functions are generally more efficient and easier to optimize.
3. **Readability Concerns**:
    - If the logic becomes too complex, using explicit joins or Common Table Expressions (CTEs) can make the query easier to understand.


### Key Takeaways

- Correlated subqueries are powerful but should be used judiciously due to potential performance costs.
- They're ideal for row-specific logic and dynamic filtering when joins or window functions aren't feasible.
- For performance-critical queries, always evaluate alternative approaches like window functions or joins.