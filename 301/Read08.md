# SQL

### Structured Query Language
it is a language designed to allow technical and non-technical users query, manipulate, and transform data from relational database, and SQL databases provide a safe scalable storage for millions of websites and mobile.
### relational database
It represents a collection of related tables, each table is with fixed numbeer of named columns and any number of rows.
 
### Using SQL
* Selecting
   When we choose the table we want, we can choose the columns we need using the (select) statements as follows:
        ```
        SELECT column, another_column, ...
        FROM table_name;
        ```
* Queries with constraints
    in some table there are millions of rows to use, so in that case choosing the column that will get all the rows is a bad choice, so in orderto filter the results we want we can use the WHERE clause in the query, it is used by selecting the column then writing the data we want to have as follows:
    ```
    SELECT column, another_column, ...
    FROM table_name
    WHERE condition
    AND/OR antoher_condition
    AND/OR...;
    ```
    we can use the following operators to make the conditions:
        ![](https://i.ibb.co/WB97Cqm/op1.png)

    and there are another operatorn for the comparison:
        ![](https://i.ibb.co/zZNDk52/op2.png)

* Ordering and limiting:
    We can use the ORDER BY clause to order the rows asccending or Descending, and we can use DISTINCT to remove duplicate rows, and LIMIT to reduce the number of rows and the OFFSET to specify where to begin as follows:
    ```
    Select query with limited rows
    SELECT column, another_column, …
    FROM mytable
    WHERE condition(s)
    ORDER BY column ASC/DESC
    LIMIT num_limit OFFSET num_offset;
    ```
* Inserting values to the table:
    we can insert values using INSERT INTO and specify the values as the default order and data-typea as follows:
    * Insert statement with values for all columns
        ```
        INSERT INTO mytable
        VALUES (value_or_expr, another_value_or_expr, …),
       (value_or_expr_2, another_value_or_expr_2, …),
       …;
       ```
    * Insert statement with specific columns
        ```
        INSERT INTO mytable
        (column, another_column, …)
        VALUES (value_or_expr, another_value_or_expr, …),
        (value_or_expr_2, another_value_or_expr_2, …),
        …;
        ```
* Updating data:
    we can update data using :
    ```
    UPDATE mytable
    SET column = value_or_expr, 
    other_column = another_value_or_expr, 
    …
    WHERE condition;
    ```

