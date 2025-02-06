# Chapter 2: Data Models and Query Languages

## Overview
This chapter examines the evolution of data models and query languages, comparing relational, document, and graph-based models. It emphasizes how different models address specific use cases and introduces **MapReduce** as a framework for large-scale data processing.

---

## Key Concepts

### 1. **Relational Model**
- **Structure**: Data organized into tables (rows and columns) with strict schemas.
- **Strengths**:
  - Powerful for complex queries and joins.
  - ACID transactions and normalization reduce redundancy.
- **Query Language**: SQL (declarative).
- **Use Case**: Structured data with well-defined relationships (e.g., financial systems).

---

### 2. **Document Model**
- **Structure**: Self-contained documents (JSON/XML) with nested data.
- **Strengths**:
  - Flexible schema (schema-on-read).
  - Efficient for hierarchical or one-to-many relationships.
- **Weaknesses**: Poor support for many-to-many relationships.
- **Examples**: MongoDB, CouchDB.
- **Use Case**: Content management systems, semi-structured data.

---

### 3. **Graph Model**
- **Structure**: Nodes (entities) and edges (relationships).
- **Strengths**:
  - Excels at interconnected data (e.g., social networks).
  - Supports expressive traversal queries.
- **Query Languages**: Cypher (Neo4j), SPARQL (RDF), Gremlin.
- **Use Case**: Fraud detection, recommendation engines.

---

### 4. **Query Languages**
- **Declarative (e.g., SQL)**: Specify *what* data to retrieve, not *how*. Enables optimization by the database engine.
- **Imperative**: Explicitly define steps to retrieve data (e.g., application code).
- **MapReduce**: A low-level programming model for batch processing (details below).

---

### 5. **MapReduce**
- **Purpose**: Process large datasets in parallel across distributed systems.
- **Phases**:
  1. **Map**:
    - Input: Key-value pairs (e.g., raw log files).
    - Output: Intermediate key-value pairs (e.g., `(user_id, 1)` for each action).
  2. **Reduce**:
    - Input: Grouped intermediate keys and their values (e.g., `(user_id, [1, 1, 1])`).
    - Output: Aggregated results (e.g., `(user_id, total_actions)`).
- **Example Use Case**:
  - Counting page views: Map extracts URLs, Reduce sums totals per URL.
- **Advantages**:
  - Scalable for petabytes of data.
  - Fault-tolerant (handles node failures).
- **Limitations**:
  - Requires writing custom code (not declarative).
  - High latency (not for real-time queries).
  - Complex multi-step workflows (e.g., chaining jobs).
- **Tools**: Hadoop, MongoDB (legacy), and cloud data pipelines.

---

### 6. **Trade-offs Between Models**
| **Model**       | **Strengths**                          | **Weaknesses**                     |
|------------------|----------------------------------------|------------------------------------|
| **Relational**   | Joins, ACID, complex queries           | Rigid schema, scaling complexity   |
| **Document**     | Flexibility, hierarchical data         | Poor for many-to-many relationships|
| **Graph**        | Traversal of relationships             | Overhead for simple queries        |

---

### 7. **Schema Flexibility**
- **Schema-on-Write** (Relational): Enforce structure upfront. Changes require migrations.
- **Schema-on-Read** (Document/Graph): Interpret data structure at query time. Flexible but risks inconsistency.

---

### 8. **Scalability**
- **Relational**: Vertical scaling (strong consistency) but struggles with horizontal scaling.
- **NoSQL (Document/Graph)**: Prioritize horizontal scaling and availability (eventual consistency).

---

## Key Takeaways
1. **Data Model Fit**: Choose based on data structure, relationships, and query patterns.
2. **Declarative > Imperative**: Declarative languages (SQL, Cypher) simplify optimization.
3. **MapReduce**: Powerful for batch analytics but lower-level than modern tools (e.g., Spark, SQL-on-Hadoop).
4. **Hybrid Systems**: Modern databases blend models (e.g., PostgreSQL with JSON and graph extensions).