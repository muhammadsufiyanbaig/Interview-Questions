## **9. MongoDB**

### **Beginner:**

1. **What is MongoDB, and how does it differ from SQL databases?**
   - **MongoDB** is a NoSQL, document-oriented database that stores data in flexible, JSON-like format called **BSON** (Binary JSON). Unlike SQL databases that store data in tables and rows, MongoDB stores data as documents within collections, making it schema-less and suitable for applications with evolving data models.

2. **What is a document in MongoDB?**
   - A **document** in MongoDB is a record, similar to a row in SQL, but it is stored in a flexible JSON-like format. It can contain nested structures (arrays, objects), making it suitable for complex and hierarchical data.

3. **What are collections in MongoDB?**
   - A **collection** in MongoDB is analogous to a table in a relational database. It holds multiple documents that are stored together. Collections are schema-less, meaning documents within a collection can have different structures.

4. **What are the advantages of using MongoDB?**
   - **Flexibility**: It allows schema-less data storage.
   - **Scalability**: It supports horizontal scaling through sharding.
   - **Performance**: Designed for high-performance read and write operations.
   - **Agility**: Easier to work with unstructured data and supports fast prototyping.

5. **How do you insert, update, and delete documents in MongoDB?**
   - **Insert**: `db.collection.insertOne(doc)` or `db.collection.insertMany([doc1, doc2])`
   - **Update**: `db.collection.updateOne({filter}, {update})` or `db.collection.updateMany({filter}, {update})`
   - **Delete**: `db.collection.deleteOne({filter})` or `db.collection.deleteMany({filter})`

6. **What is the difference between `findOne()` and `find()` in MongoDB?**
   - `findOne()` returns the **first document** that matches the query.
   - `find()` returns a **cursor** pointing to all documents that match the query, allowing for pagination and iteration.

7. **How do you filter documents using MongoDB queries?**
   - MongoDB queries use a JSON-like syntax. Example: `db.collection.find({field: value})` to find documents with a specific field value.

8. **What is an ObjectId in MongoDB?**
   - **ObjectId** is the default unique identifier for documents in MongoDB. It is a 12-byte identifier, automatically generated when a document is created.

9. **What is indexing in MongoDB, and how does it improve performance?**
   - **Indexing** in MongoDB is a mechanism that allows for fast lookups of documents. It speeds up queries by creating a data structure that maps the fields in the documents to their values, reducing the search time.

10. **How does MongoDB handle schema flexibility?**
    - MongoDB’s schema flexibility allows each document in a collection to have a different structure. This is advantageous for applications where the data model may evolve over time.

---

### **Mid-Level:**

1. **How does MongoDB handle transactions?**
   - MongoDB supports **ACID transactions** since version 4.0. It allows multiple operations (across multiple documents or collections) to be performed as a single transaction, ensuring consistency and isolation.

2. **What are MongoDB aggregations, and how do they work?**
   - **Aggregation** is the process of performing operations on data (such as filtering, grouping, and sorting) to produce aggregated results. MongoDB provides the `$aggregate` method, which uses a pipeline of stages (e.g., `$match`, `$group`, `$sort`) to process data.

3. **How does MongoDB handle sharding?**
   - **Sharding** in MongoDB is the process of distributing data across multiple servers. It enables horizontal scaling by splitting large datasets into smaller chunks and distributing them across different servers or clusters.

4. **What is the difference between a `lookup` and a `join` in MongoDB?**
   - A **`lookup`** is an aggregation operation in MongoDB that allows you to perform a **left outer join** to combine data from two collections based on a matching field. SQL **joins** are typically used to combine tables with foreign key relationships.

5. **How do you handle schema validation in MongoDB?**
   - MongoDB allows schema validation using the `validator` option in collection creation. It uses the JSON Schema specification to enforce rules such as required fields, field types, and ranges of values.

6. **What is a capped collection in MongoDB?**
   - A **capped collection** is a fixed-size collection that automatically overwrites its oldest documents when it reaches its size limit. It is used for scenarios like logging where only the most recent records are important.

7. **How do you implement authentication and authorization in MongoDB?**
   - MongoDB supports **authentication** via username/password, LDAP, or x.509 certificates. **Authorization** can be implemented using **role-based access control (RBAC)** to define what actions a user can perform on specific resources.

8. **How does MongoDB handle replication and high availability?**
   - MongoDB uses **replica sets** to provide high availability. A replica set is a group of MongoDB instances that maintain the same data set. One node is the primary (writes and reads), while the others are secondary (read-only, backup).

9. **What are GridFS and its use cases?**
   - **GridFS** is a specification for storing and retrieving files that exceed the BSON document size limit (16MB). It divides large files into smaller chunks and stores them in two collections (`chunks` and `files`).

10. **How do you optimize queries in MongoDB for performance?**
    - Use **indexes** to speed up query execution.
    - Limit the number of documents returned with `.limit()`.
    - Use **projection** to only retrieve required fields.
    - Analyze query performance with `explain()`.

---

### **Senior-Level:**

1. **How does MongoDB compare with PostgreSQL for large-scale applications?**
   - MongoDB is better suited for **unstructured or semi-structured data** with high write throughput requirements, horizontal scalability, and flexible schema. **PostgreSQL**, on the other hand, excels with **structured data** requiring complex queries, strong ACID compliance, and complex joins.

2. **What are MongoDB change streams, and how do they work?**
   - **Change streams** allow applications to listen to real-time changes in the database (inserts, updates, deletes) without polling. They provide a feed of changes as events that can trigger actions in response to data changes.

3. **How do you implement multi-document ACID transactions in MongoDB?**
   - Since MongoDB version 4.0, you can implement multi-document ACID transactions using the `session` API. Transactions can span multiple documents and collections within a replica set or sharded cluster.

4. **How would you design a scalable MongoDB architecture?**
   - A scalable architecture would involve:
     - **Sharding** for horizontal scaling of large datasets.
     - **Replication** for high availability and fault tolerance.
     - **Load balancing** to distribute traffic evenly.
     - **Backup and monitoring** tools for disaster recovery and health checks.

5. **How does MongoDB Atlas improve database management?**
   - **MongoDB Atlas** is a fully-managed cloud database service that simplifies database management by providing automated backups, scaling, monitoring, security, and performance tuning. It integrates with popular cloud platforms like AWS, GCP, and Azure.

6. **How would you handle database migrations in MongoDB?**
   - Database migrations in MongoDB can be handled using tools like **Mongoose migration scripts** or manual updates to schema validation rules. MongoDB supports rolling updates to handle migrations without downtime.

7. **What are the advantages and disadvantages of using MongoDB for an e-commerce application?**
   - **Advantages**:
     - Flexible schema for evolving product data.
     - High write throughput and performance for dynamic inventory updates.
   - **Disadvantages**:
     - Lack of relational features like JOINs may complicate complex queries.
     - Potential challenges with transaction consistency across multiple documents.

8. **How does MongoDB handle concurrency and locking?**
   - MongoDB uses **document-level locking** in replica sets and sharded clusters. It allows for high concurrency with minimal locking contention. However, complex operations can still result in locking delays.

9. **How would you implement role-based access control (RBAC) in MongoDB?**
   - Implement **RBAC** in MongoDB by creating **custom roles** and assigning them specific permissions (e.g., read, write, admin) for different resources like databases or collections. Roles can be assigned to users based on their responsibilities.

10. **How do you integrate MongoDB with a GraphQL API?**
    - You can integrate MongoDB with a **GraphQL API** by using **Apollo Server** and a MongoDB driver like **Mongoose**. GraphQL resolvers fetch data from MongoDB and return it in the required format. You can leverage the flexibility of MongoDB’s schema-less nature to model GraphQL types.
