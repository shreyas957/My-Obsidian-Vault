2025-09-12 15:48

Status: [[complete]]

Tags: [[System Design]]


# CAP Theorem 
CAP : Consistency, Availability, Partition tolerance
According to the CAP theorem, only two of the three desirable characteristics *consistency*, *availability,* and *partition tolerance* —can be shared or present in a networked shared-data system or distributed system.

1) Consistency: All nodes/users see the same data at same time. 
2) Availability: Every request gets the response(successful or not)\
3) Partition tolerance: System works despite network failures between nodes.


![[CAP-Theorem-1.png]]
As in distributed systems,  the partition tolerance is important, then we have to choose between either consistency or availability. 

![[CAP-Theorame-2.png]]
Based on above example, ....
## How does it influence my design?

### Strong consistency
- implement distributed transactions
- limit to a single node
- discuss consensus protocols
- accept higher latency
- Example tools
  - PostgreSQL
  - Trad RDBMS
  - Spanner
  - NoSQL with strong consistency mode (DynamoDB)
### Availability
- use multiple replicas
- CDC(change-data-capture) and eventual consistency is ok
- Example tools
  - DynamoDB (in multi-AZ mode)
  - Cassandra

## Different parts of a system can have different requirements?
**Ticketmaster**
- availability for CRUD on events
- consistency for booking tickets
**Tinder**
- availability for viewing profile data
- consistency for matching
## Different types of consistency
1. Strong Consistency: all reads reflect most recent write
2. Causal Consistency: related events appear in order
3. Read-your-writes Consistency: user sees their own updates
4. Eventual Consistency: updates will propagate eventually

# References
