## **PostgreSQL**

### **Beginner:**

1. **What is PostgreSQL, and how does it differ from other databases?**
   - PostgreSQL is an open-source, object-relational database management system (RDBMS) that is known for its reliability, extensibility, and SQL-compliance. It differs from other databases by offering advanced features such as support for complex queries, foreign keys, triggers, views, and more, while being highly scalable and capable of handling large amounts of data efficiently.

2. **How do you create a database and table in PostgreSQL?**
   - You can create a database using the command: `CREATE DATABASE mydatabase;`
   - To create a table, you can use: 
     ```sql
     CREATE TABLE mytable (
       id SERIAL PRIMARY KEY,
       name VARCHAR(100),
       age INT
     );
     ```

3. **What are the basic data types available in PostgreSQL?**
   - Basic data types include:
     - `INTEGER`, `BIGINT`, `FLOAT`, `BOOLEAN`
     - `CHAR`, `VARCHAR`, `TEXT`
     - `DATE`, `TIME`, `TIMESTAMP`
     - `BYTEA` (for binary data)
     - `JSON`, `JSONB`

4. **How do you insert, update, delete, and retrieve data in PostgreSQL?**
   - Insertion: 
     ```sql
     INSERT INTO mytable (name, age) VALUES ('Alice', 30);
     ```
   - Update:
     ```sql
     UPDATE mytable SET age = 31 WHERE name = 'Alice';
     ```
   - Delete:
     ```sql
     DELETE FROM mytable WHERE name = 'Alice';
     ```
   - Retrieve:
     ```sql
     SELECT * FROM mytable WHERE age > 20;
     ```

5. **What is a primary key, and why is it important?**
   - A primary key is a field or a combination of fields that uniquely identifies each row in a table. It is essential because it ensures data integrity and allows for efficient searching, indexing, and relationships with other tables.

6. **What is an index in PostgreSQL, and how does it improve performance?**
   - An index in PostgreSQL is a data structure that improves the speed of data retrieval operations on a database table by allowing quick lookups. It enhances performance for queries that use `WHERE`, `JOIN`, or `ORDER BY` clauses.

7. **What is the difference between `CHAR`, `VARCHAR`, and `TEXT` in PostgreSQL?**
   - `CHAR`: Fixed-length string, padded with spaces if the length is shorter than defined.
   - `VARCHAR`: Variable-length string with a defined limit.
   - `TEXT`: Variable-length string with no length limit.

8. **How do you use `JOIN` in PostgreSQL? Provide examples.**
   - `INNER JOIN`:
     ```sql
     SELECT users.name, orders.total
     FROM users
     INNER JOIN orders ON users.id = orders.user_id;
     ```
   - `LEFT JOIN`:
     ```sql
     SELECT users.name, orders.total
     FROM users
     LEFT JOIN orders ON users.id = orders.user_id;
     ```

9. **What is the purpose of `GROUP BY` and `HAVING` in SQL?**
   - `GROUP BY`: Groups rows that have the same values into summary rows, typically used with aggregate functions like `COUNT`, `SUM`, etc.
   - `HAVING`: Filters groups created by `GROUP BY` based on a condition.

10. **How do you filter data using `WHERE` and `ORDER BY`?**
    - `WHERE`: Used to filter records based on a condition.
      ```sql
      SELECT * FROM users WHERE age > 21;
      ```
    - `ORDER BY`: Used to sort results in ascending or descending order.
      ```sql
      SELECT * FROM users ORDER BY age DESC;
      ```

---

### **Mid-Level:**

1. **How does PostgreSQL handle ACID compliance?**
   - PostgreSQL ensures ACID (Atomicity, Consistency, Isolation, Durability) compliance through its transaction management system, ensuring data integrity and reliability. Each transaction is atomic and isolated, ensuring that operations are consistent and durable.

2. **What are `CTE` (Common Table Expressions) in PostgreSQL?**
   - A `CTE` is a temporary result set that you can reference within a `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement. It's defined using `WITH`:
     ```sql
     WITH cte AS (SELECT id, name FROM users WHERE age > 30)
     SELECT * FROM cte;
     ```

3. **What is a `VIEW`, and how is it used in PostgreSQL?**
   - A `VIEW` is a virtual table based on the result of a `SELECT` query. It allows you to encapsulate complex queries and simplify data access:
     ```sql
     CREATE VIEW active_users AS
     SELECT id, name FROM users WHERE active = true;
     ```

4. **What is a `TRIGGER`, and how do you implement one?**
   - A `TRIGGER` is a function that is automatically executed in response to certain events on a table or view (like `INSERT`, `UPDATE`, or `DELETE`). For example:
     ```sql
     CREATE TRIGGER update_timestamp
     BEFORE UPDATE ON users
     FOR EACH ROW
     EXECUTE FUNCTION update_timestamp_function();
     ```

5. **What is a `STORED PROCEDURE`, and how does it work?**
   - A `STORED PROCEDURE` is a set of SQL commands that can be stored in the database and executed as needed. They are typically used to encapsulate business logic and repetitive tasks:
     ```sql
     CREATE PROCEDURE update_user_age(IN user_id INT, IN new_age INT)
     LANGUAGE plpgsql
     AS $$
     BEGIN
       UPDATE users SET age = new_age WHERE id = user_id;
     END;
     $$;
     ```

6. **What is JSONB, and how does it differ from JSON?**
   - `JSONB` is a binary format for storing JSON data that allows for faster processing and more efficient storage compared to the standard `JSON` type, which stores data as plain text. `JSONB` supports indexing and is often preferred for performance.

7. **How do you perform full-text search in PostgreSQL?**
   - PostgreSQL provides a built-in full-text search capability using `tsvector` and `tsquery`. Example:
     ```sql
     SELECT * FROM articles WHERE to_tsvector('english', content) @@ to_tsquery('english', 'PostgreSQL');
     ```

8. **What is the difference between a materialized view and a regular view?**
   - A regular view is a dynamic query that retrieves data when accessed. A materialized view stores the result of the query physically, allowing for faster reads but requiring periodic refreshes to update the data.

9. **How do you optimize PostgreSQL queries for performance?**
   - Optimization techniques include:
     - Using proper indexes
     - Avoiding `SELECT *`
     - Writing efficient `JOIN` queries
     - Using `EXPLAIN ANALYZE` to analyze query performance
     - Normalizing data to avoid redundant queries

10. **How does PostgreSQL handle transactions and isolation levels?**
    - PostgreSQL supports transactions, which ensure that operations are atomic. It offers several isolation levels like `READ COMMITTED`, `REPEATABLE READ`, and `SERIALIZABLE`, which determine how transactions are isolated from each other.

---

### **Senior-Level:**

1. **How do you handle database replication in PostgreSQL?**
   - PostgreSQL supports synchronous and asynchronous replication using `streaming replication` to create replicas of the primary database. This ensures data redundancy and improves high availability.

2. **What are PostgreSQL’s partitioning strategies?**
   - Partitioning strategies include range partitioning, list partitioning, and hash partitioning. Each strategy divides a table into smaller, more manageable pieces based on the data.

3. **How do you perform database sharding in PostgreSQL?**
   - Sharding is the process of horizontally dividing data across multiple databases or servers. In PostgreSQL, you can achieve sharding using `Citus` or manually managing partitions across multiple servers.

4. **How do you manage database migrations in PostgreSQL?**
   - Migrations can be managed using tools like `Flyway` or `Liquibase`, or by writing SQL migration scripts to update the schema.

5. **What are the advantages of using `PL/pgSQL` for stored procedures?**
   - `PL/pgSQL` is PostgreSQL’s procedural language and is used for creating complex stored procedures. It allows for better control structures (like loops and conditions) and supports exception handling.

6. **How do you implement Row-Level Security (RLS) in PostgreSQL?**
   - RLS enables fine-grained access control by restricting access to rows in a table based on user roles or session variables:
     ```sql
     CREATE POLICY policy_name
     ON table_name
     FOR SELECT
     USING (user_id = current_user_id());
     ```

7. **How does PostgreSQL handle concurrency and locking?**
   - PostgreSQL uses MVCC (Multi-Version Concurrency Control) to allow for concurrent access to data without conflict. It provides several types of locks, including row-level locks and table-level locks, to manage concurrent access.

8. **What are the best practices for indexing in PostgreSQL?**
   - Best practices include:
     - Creating indexes on frequently queried columns
     - Avoiding unnecessary indexes
     - Using `GIN` or `GiST` indexes for full-text or spatial data

9. **How would you design a multi-tenant database using PostgreSQL?**
   - Multi-tenancy in PostgreSQL can be achieved by using separate schemas for each tenant, row-level security for isolating tenant data, or even database sharding.

10. **How do you integrate PostgreSQL with a GraphQL API?**
    - To integrate PostgreSQL with a GraphQL API, you can use tools like `PostGraphile`, `Hasura`, or implement your own resolvers that interact with PostgreSQL through `SQL` queries.

