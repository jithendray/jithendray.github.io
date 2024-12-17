---
tags: sql
---

# JOIN on TRUE

In [[notes/sql/015-sql-joins|015-sql-joins]] - sometimes tables should be joined just to give results from multiple tables in the same output without any joining key.

```sql
FROM hire_gaps
FULL OUTER JOIN fire_gaps ON TRUE;
```

### Explanation:

1. `FULL OUTER JOIN`:
    - Combines all rows from both `hire_gaps` and `fire_gaps`.
    - If a row from `hire_gaps` has no matching row in `fire_gaps`, the result will include the row from `hire_gaps` with `NULL` values for the `fire_gaps` columns, and vice versa.
    - Ensures all data from both `hire_gaps` and `fire_gaps` is considered, even if one of the CTEs (Common Table Expressions) is empty (e.g., no hires or no terminations).

2. `ON TRUE`:
    - A join condition that is always true. This means every row from `hire_gaps` is paired with every row from `fire_gaps` (a Cartesian product), but since we're only aggregating (`MAX()`), no duplication occurs.
    - This approach avoids filtering or matching specific rows because the gaps are independent metrics.

3. Why Use `FULL OUTER JOIN ON TRUE`?:
    - To ensure that both `hire_gaps` and `fire_gaps` contribute to the final result, even if one of them is empty.
    - For example:
        - If no employees were fired (`fire_gaps` is empty), we still want to return the maximum hiring gap (`hire_gaps`).
        - If no employees were hired (`hire_gaps` is empty), we still want to return the maximum firing gap (`fire_gaps`).

4. Effect in the Query:
    - The `FULL OUTER JOIN ON TRUE` effectively combines both `hire_gaps` and `fire_gaps`, ensuring we compute `MAX()` for both gaps even if one CTE has no rows.