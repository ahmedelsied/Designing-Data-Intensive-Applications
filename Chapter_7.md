# Chapter 7 of *Designing Data-Intensive Applications* focuses on the transactions
## 1. The Slippery Concept of a Transaction
- A transaction is an abstraction layer that allows an application to pretend certain concurrency problems and failures don’t exist.
- Not all databases need transactions, but they simplify error handling by bundling operations into an "all-or-nothing" unit.
- Definitions vary: Some databases (e.g., MySQL, PostgreSQL) offer traditional ACID transactions, while others (e.g., many NoSQL systems) explicitly avoid them for scalability.
- The scope (e.g., single-operation vs. multi-object) and guarantees differ across systems.
- Transactions are a trade-off: They simplify programming but limit scalability and performance (e.g., distributed transactions are expensive).
## 2.The Meaning of ACID
### A: Atomicity
- Definition: "All-or-nothing" guarantee. If a transaction aborts, partial changes are undone.
- Atomicity is about recovery, not concurrency. It ensures the system is left in a clean state after crashes.
- Example: A transaction transferring money between two accounts won’t leave one account debited and the other not credited.
