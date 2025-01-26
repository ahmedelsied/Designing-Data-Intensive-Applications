# Summary
## Data Intensive Application is typically:
- Store data to retreive it later (Database)
- Remember result of expensive operation to speed up reads (Cache)
- Allow user to search data by keyword or filter it in various ways (Search indexes)
- Preiodically crunch a large amount of accumlated data (batch processing)
## Data Systems Example
<p align="center">
    <img src="assets/fig1.1.png"  width="400" height="350">
</p>

## Some questions to ask when designing a data system:
- How do you ensure that the data will remains correct and complete, even when things go wrong internally?
- How do you provide consistently good performance to clients, even when parts of your system are degraded?
- How do you scale your system to handle an increase in load?
- What does the good API for the system look like?
## Things that influence the design of a data system:
- The skills and experience of the people involved
- The time constraints
- Legacy systems dependencies
- The organization's tolerance for risk
## The most points that the book will cover:
- Reliability
  - The system should continue to work correctly (performing the correct function at the desired level of performance) even in the face of adversity (hardware or software faults, and human error).
- Scalability
    - As the system grows (in data volume, traffic volume, or complexity), there should be reasonable ways of dealing with that growth.
- Maintainability
    - Over time, many different people will work on the system, and they should all be able to work on it productively.
## Reliability
### Reliable system expectations:
- The application performs the function that the user expected.
- It can tolerate the user making mistakes or using the software in unexpected ways.
- Its performance is good enough for the required use case, under the expected load and data volume.
- The system prevents any unauthorized access and abuse.
### Then Reliability is about making systems work correctly, even when faults occur.
- The system that anticipates faults and can cope with them called "fault-tolerant" or "resilient".
- It's impossible to prevent all faults.
#### Fault: A fault is usually defined as one component of the system deviating from its spec.
#### Failure: The system as a whole stops providing the required service to the user.
- Faults can lead to failures, but not all faults lead to failures.
- It is usually best to design fault tolerance mechanisms that prevent faults from causing failures.
- Chaos monkey is a tool that randomly terminates servers in your production system to test if the system can tolerate it.
### When to prevent faults?
- This is the case of security matters
- If an attacker has compromised a system and gained access to a sensitive data.
### Faults types:
- Hardware faults
  - Hard drives crash, RAM becomes faulty, the power supply unit fails, the motherboard burns out, and so on.
  - Hardware faults are usually handled by replacing the hardware component (Redundancy).
- Software errors
  - Bugs in the code (e.g., unhandled exceptional conditions such as division by zero, null pointer dereference, or invalid format string).
  - Software errors can be handled by testing the software thoroughly, including writing automated tests that simulate various kinds of faults.
  - Examples: 
    - Using a language that checks for null pointer dereference at compile time.
    - Using a type system that ensures that a variable is always initialized before it is used.
    - Using a linter that statically analyzes the code to find suspicious patterns.
- Human errors:
  - Humans are known to be unreliable, 10-25% of incidents are caused by human error.
  - Solutions:
    - Design systems in a way that minimizes opportunities for error.
    - Decouple the places where people make the most mistakes from the places where they can cause failures (production and sandbox).
    - Test thoroughly at all levels, from unit tests to whole-system integration tests and manual tests.
    - Easy rollbacks.
    - Set up detailed and clear monitoring.
    - Implement good management practices and training.
### How important is reliability?
- It's not just for nuclear power stations and air traffic control systems.
- It's important for any system that stores or manipulates our data.
- Even if the system is not life-critical, reliability is still important, for example, if the system is difficult to repair or has a high cost of failure.
- There are situations in which we may choose to sacrifice reliability for other things, such as development speed or new features.
## Scalability
### Scalability definition:
