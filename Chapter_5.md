# Chapter 5 of *Designing Data-Intensive Applications* focuses on the topic of replication. It discusses various replication strategies, consistency models, and trade-offs involved in building distributed systems.
## **Replication**
### **1. Replication Strategies**
- **Replication** is the process of storing copies of data on multiple machines to ensure fault tolerance and high availability.
- **Leader-Followers replication** involves one node (Leader) handling writes and replicating data to other nodes (Followers) for read operations.
- **Multi-Leader replication** allows multiple nodes to accept writes, providing better write scalability and fault tolerance.
- **Leaderless replication** involves all nodes accepting writes, providing better read scalability and fault tolerance.
### **2. Sync vs. Async Replication**
- **Synchronous replication** ensures that writes are committed to multiple nodes before acknowledging the write operation.
- **Asynchronous replication** acknowledges writes before committing them to other nodes, providing better write performance but risking data loss.
- **Semi-synchronous replication** is a compromise between synchronous and asynchronous replication, providing better durability and performance.
- **Chain replication** is a form of replication where writes are passed through a chain of nodes before being committed.
### **3. Setting Up New Followers**
## The steps like this:
- **Take a consistent snapshot** of the Leader's state.
- **Copy the snapshot** to the new Follower node.
- **Start the Follower** node and connect it to the Leader for replication.
### **4. Handling Node Outages**
- **Follower Failure: catch-up recovery** involves re-syncing a failed Follower node with the Leader's state by copying missing data from logs of data changes.
- **Leader Failure: failover** involves promoting a Follower node to become the new Leader and reconfiguring the system to redirect writes to the new Leader.
#### **5. Failover problems**
- **Data Loss** occurs when the new Leader has not replicated all writes from the old Leader.
- **Split Brain** occurs when multiple nodes believe they are the Leader, leading to conflicts and data inconsistency.
- **Preventing Split Brain** involves using fencing mechanisms to ensure only one node becomes the Leader.
### **6. Implementing of Replication Logs**
- **Statement-based replication** involves replicating SQL statements from the Leader to Followers.
  - **Problems**: non-deterministic statements, schema changes, and performance issues.
  - **Solutions**: logical (row-based) replication, and trigger-based replication.
  - **Used in**: MySQL 5.1 and voltDB (But make it safe by requiring deterministic statements).
- **Write-Ahead Log (WAL)** is a log of changes written before the data is updated, providing durability and replication support.
  - **Problems**: disk I/O, log compaction, and log shipping.
  - **Used in**: PostgreSQL, and Oracle.
- **Logical Log** is a log of data changes in a structured format, providing a way to replicate data changes.
  - **Problems**: data consistency (eventual consistent), and performance overhead with write intensive workloads.
  - **Used in**: Apache Kafka, and Amazon Kinesis.
- **Trigger-based replication** involves using triggers to capture data changes and replicate them to other nodes.
  - **Problems**: more prone to bugs, and limitations than the database's built-in replication.
  - **Used in**: Oracle GoldenGate.
### **7. Problems with Replication Lag**
- **Replication Lag** refers to the delay between writes on the Leader and their replication to Followers.
- **Causes**: network latency, disk I/O, and processing delays.
- **Solutions**:
  - **Read Your Writes**: ensure that reads are consistent with writes.
  - **Monotonic Reads**: ensure that reads are consistent with the order of writes.
  - **Consistent Prefix Reads**: ensure that reads are consistent with a prefix of writes.
  - **Read-after-Write Consistency**: ensure that reads are consistent with writes after a write operation.
