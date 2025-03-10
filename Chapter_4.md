# Chapter 4 of *Designing Data-Intensive Applications* focuses on the topic of encoding and evolution. It discusses various encoding formats, schema evolution, and compatibility issues that arise when dealing with data storage and retrieval.
## **Encoding and Evolution**
### **1. Data Encoding Formats**
- Data encoding is the process of converting data into a specific format for storage or transmission.
- Common encoding formats include **JSON**, **XML**, **Protocol Buffers**, **Thrift** and **Avro**.
- **JSON** and **XML** are human-readable but less space-efficient compared to binary formats like **Protocol Buffers** and **Avro**.
- **Protocol Buffers** and **Avro** provide schema support and are more efficient for serialization and deserialization.
- **Thrift** is similar to **Protocol Buffers** but has some differences in schema definition and language support.
- **Avro** is a self-describing format that includes schema information with the data.
### **2. Schema Evolution**
- **Schema evolution** refers to the process of changing the structure of data over time while maintaining compatibility with existing data.
- **Schema evolution strategies** include **backward compatibility**, **forward compatibility**, and **full compatibility**.
- **Forward compatibility** ensures that new code can read old data, while **backward compatibility** ensures that old code can read new data.
- **Backward compatibility** allows new schema versions to read data written in the old schema.
- **Full compatibility** ensures that both old and new code can read data written in any schema version.
### **3. Formats for Encoding Data**
- **in-memory data structures** are often serialized to disk or transmitted over the network using encoding formats.
- **Binary encoding formats** are more space-efficient and faster to serialize/deserialize compared to text-based formats.
- translation from in-memory representation to a byte sequence is called **serialization**, and the reverse process is called **deserialization**.
### **4. Language-Specific Formats**
- Some languages have built-in support for specific encoding formats (e.g., **JSON** in JavaScript, **Protocol Buffers** in Java).
- for example:
  - Java has java.io.Serializable for object serialization.
  - Python has pickle and marshal for serialization.
  - Ruby has Marshal for serialization.
- the deep problem with language-specific formats:
  - that they are tightly coupled to the programming language
  - may not be compatible with other languages.
  - can be difficult to evolve schemas over time. 
### **5. Modes Of Dataflow**
- **Dataflow** refers to the movement of data between systems or components.
- **Async MSG-passing** is a form of dataflow where messages are sent between components asynchronously Like (Kafka, RabbitMQ, and Amazon SQS).
- **Databases** Like Espresso is a form of dataflow where data is pushed to clients in real-time.
- **Service calls** are another form of dataflow where services communicate with each other over a network Like (Rest, SOAP and RPC).