2025-09-15 22:58

Status: [[Spring Boot]]

Tags: [[complete]]

# Transaction Management (@Transactional)
## Critical Section: 
It is code segment, where shared resources are being accessed and modified. 
- The **critical section** is the portion of a transaction where it accesses shared data, and thus must be executed in isolation from other transactions to avoid conflicts.
- When multiple requests try to access the critical section, data inconsistency can occur.
- Solution --> Use  ***`Transactions`***
-  Helps to achieve ACID properties.

## ACID: 
1. Atomicity: Ensure all operations within transaction are successful. If any operation get failed, the entire transaction is rolled back.
2. Consistency: Ensure DB state before and after transaction is consistent only.
3. Isolation: Ensures that, Even if multiple transactions are running in parallel they do not interfere with each other. (Proper locking and synchronization mechanism is used)
4. Durability: Ensure committed transaction is never lost despite system crash or power failure. 

## @Transactional: 
1. Need dependency, In case of relational database, we can use `spring-boot-starter-data-jpa` Also database driver dependency is also required.
2. Activate transaction management by using **`@EnableTransactionManagement`**. (Spring boot generally autoconfigure it, so no need to use.)
3.  @Transactional annotation can be used at class level & method level. 
	1. **At class level**: transaction is applied to all public methods and method will get executed within a transaction. 
	2. **At method level**: Transaction applied to particular method only. If we put it on private or protected methods it will be ignored.
4. Transaction management in spring boot uses AOP. 
	1. Uses pointcut expression to search for methods which has @Transactional annotation
	2. Once the point cut expression matches  run an "Around" types of advice. `invokeWithinTransaction`  method present in `TransactionalInterceptor` class. 

## Hierarchy of transactions managers: 
![[Transactions Managers Spring Boot.png]]

## Transaction Management:
#### 1. Declarative:
- Transaction management through annotations. We use `@TRansactional` annotation.
- Based on the underlying datasource, like JPA or JDBC Spring boot will  automatically choose correct transaction manager. 
#### 2. Programmatic:
- Transaction management through code.
- Flexible, but difficult to maintain.
- e.g. See code repository for examples
---
## Some Spring Transaction API:
#### 1. `TransactionTemplate`
- Helper class for declarative-style programmatic transactions.
- It wraps  `PlatformTransactionManager` to simplify transaction logic
- Automatically handles:
	- Starting transactions
	- Committing on success
	- Rolling back on exceptions (based on policy)
#### 2. `TransactionStatus`
- Represents the status of currently running transaction.
- Used to:
	- Mark transaction for rollback (`setRollbackOnly()`)
	- Check if transaction is new (`isNewTransaction()`)
#### 3. `TransactionCallback`
- A functional interface used with `TransactionTemplate`
- Contains the logic to be executed inside the transaction.
- Returns transaction status when executed.
#### 4. `TransactionException`
- Root exception class for transaction related exceptions.
- Thrown when error occur during transaction(commit failure, rollback issue)
---

## Propagation:
- When we create  new transaction, it first checks the transaction ***PROPAGATION*** value set, and this tells use weather we have to create a new transaction or  not.
- Propagation defines our business logic’s transaction boundary. Spring manages to start and pause a transaction according to our _propagation_ setting.
- Spring calls `TransactionManager::getTransaction` to get or create a transaction according to the propagation. It supports some of the propagations for all types of  `TransactionManager`, but there are a few of them that are only supported by specific implementations of  `TransactionManager.

#### 1. REQUIRED  (default):
use currently active transaction
```java
@Transactional(propagation=Propagation.REQUIRED)
	if(parent txn present) 
		use it;
	else
		create new txn;
```
#### 2. REQUIRED_NEW:
We need `JTATransactionManager` for actual transaction suspension
```java
@Transactional(propagation=Propagation.REQUIRED_NEW)
	if(parent txn present)
		suspend parent txn;
		create new txn and once finished;
		resume parent txn; 
	else
		create new txn and execute method;
```
#### 3. SUPPORTS:
```java
@Transactional(propagation=Propagation.SUPPORTS)
	if(parent txn present) 
		use it;
	else
		execute method without any transaction;
```
#### 4. NOT_SUPPORTED;
```java
@Transactional(propagation=Propagation.NOT_SUPPORTED)
	if(parent txn present) 
		suspend parent txn;
		execute method without any transaction;
		resume parent txn;
	else
		execute method without any transaction;
```
#### 5. MANDATORY:
active i.e. parent transaction is used.
```java
@Transactional(propagation=Propagation.MANDATORY)
	if(parent txn present) 
		use it;
	else
		throw exception;
```
#### 6. NEVER:
If there is active transaction, throw exception
```java
@Transactional(propagation=Propagation.NEVER)
	if(parent txn present) 
		throw exception;
	else
		execute method without any transaction;
```
---
## Isolation levels:
Isolation levels, tell us, how changes made by one transaction are visible to other transactions running in parallel.
`@Transactional(isolation = Isolation.READ_COMMITTED)`

| Isolation Level  | Dirty Read Possible | Non-Repeatable Read Possible | Phantom Read Possible | Concurrency |
| ---------------- | ------------------- | ---------------------------- | --------------------- | ----------- |
| READ_UNCOMMITTED | Yes                 | Yes                          | Yes                   | Hight       |
| READ_COMMITTED   | No                  | Yes                          | Yes                   | `↑`         |
| REPEATABLE_READ  | No                  | No                           | Yes                   | `↑`         |
| SERIALIZABLE     | No                  | No                           | No                    | Low         |
- The default isolation level depends on the database we are using.
- Most relational databases uses READ_COMMITTED as default isolation level.
#### Dirty Read problem: 
Transaction A reads un-committed data of another transaction.
And If another transaction get rolled back, the un-committed data read by transaction A is called dirty read.
#### Non-Repeatable Read problem: 
The transaction reads same data, but get different results.
If suppose transaction A, Reads the same row multiple times and there is chance that it get different value due to update by different transaction, then its called as non-repeatable read problem.
#### Phantom read problem:  
`Rows comming up out of nowhere`
A transaction can read data that was not there when transaction started.
If suppose transaction A, executes same query multiple times, but there is chance that the row returned are different then its knows as Phantom read problem.
This can happen if another transaction insert some data in tables.

#### DB Locking types:
Locking make sure that no other transaction update the locked row.

| Lock Type           | Another Shared Lock | Another exclusive lock |
| ------------------- | ------------------- | ---------------------- |
| Have Shared Lock    | Yes                 | Yes                    |
| Have Exclusive Lock | No                  | Yes                    |
- Shared lock(s) = READ locks
- Exclusive lock(s) = WRITE lock

| Isolation Level        | Dirty Read Possible | Non-Repeatable Read Possible | Phantom Read Possible |
|------------------------|---------------------|-------------------------------|------------------------|
| READ_UNCOMMITTED       | Yes                 | Yes                           | Yes                    |
| READ_COMMITTED         | No                  | Yes                           | Yes                    |
| REPEATABLE_READ        | No                  | No                            | Yes                    |
| SERIALIZABLE           | No                  | No                            | No                     |

| Isolation Level    | Locking Strategy                                                                                 |
|--------------------|--------------------------------------------------------------------------------------------------|
| Read Uncommitted   | **Read**: No Lock acquired  <br> **Write**: No Lock acquired                                     |
| Read Committed     | **Read**: Shared Lock acquired and released as soon as read is done  <br> **Write**: Exclusive Lock acquired and held till end of transaction |
| Repeatable Read    | **Read**: Shared Lock acquired and released only at end of transaction  <br> **Write**: Exclusive Lock acquired and released only at end of transaction |
| Serializable       | Same as Repeatable Read Locking Strategy + apply Range Lock and release at end of transaction    |

# References
