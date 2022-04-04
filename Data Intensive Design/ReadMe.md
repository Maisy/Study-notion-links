# 데이터 중심 애플리케이션 설계

https://maisy.notion.site/edu-ff53c329de16471bba675620c56241a2

[Part1. 데이터 시스템의 기초](https://www.notion.so/Part1-5bfa81c95ba94a4f801741385ac526b3)

[Part2. 분산 데이터](https://www.notion.so/Part2-7551b76bf3fa4742a0a6938cf5a992ee)

[Part3. 파생 데이터](https://www.notion.so/Part3-68401983852d4e4fa9387d969f81453a)

---
Table of contents

I. Foundations of Data Systems

1. Reliable, Scalable, and Maintainable Applications
2. Data Models and Query Languages
3. Storage and Retrieval
   Data Structures That Power Your Database
   Hash Indexes
   SSTables and LSM-Trees
   B-Trees
   Comparing B-Trees and LSM-Trees
   Other Indexing Structures
   Transaction Processing or Analytics?
   Data Warehousing
   Stars and Snowflakes: Schemas for Analytics
   Column-Oriented Storage
   Column Compression
   Sort Order in Column Storage
   Writing to Column-Oriented Storage
   Aggregation: Data Cubes and Materialized Views
   Summary
4. Encoding and Evolution
   Formats for Encoding Data
   Language-Specific Formats
   JSON, XML, and Binary Variants
   Thrift and Protocol Buffers
   Avro
   The Merits of Schemas
   Modes of Dataflow
   Dataflow Through Databases
   Dataflow Through Services: REST and RPC
   Message-Passing Dataflow
   Summary
   II. Distributed Data
5. Replication
   Leaders and Followers
   Synchronous Versus Asynchronous Replication
   Setting Up New Followers
   Handling Node Outages
   Implementation of Replication Logs
   Problems with Replication Lag
   Reading Your Own Writes
   Monotonic Reads
   Consistent Prefix Reads
   Solutions for Replication Lag
   Multi-Leader Replication
   Use Cases for Multi-Leader Replication
   Handling Write Conflicts
   Multi-Leader Replication Topologies
   Leaderless Replication
   Writing to the Database When a Node Is Down
   Limitations of Quorum Consistency
   Sloppy Quorums and Hinted Handoff
   Detecting Concurrent Writes
   Summary
6. Partitioning
   Partitioning and Replication
   Partitioning of Key-Value Data
   Partitioning by Key Range
   Partitioning by Hash of Key
   Skewed Workloads and Relieving Hot Spots
   Partitioning and Secondary Indexes
   Partitioning Secondary Indexes by Document
   Partitioning Secondary Indexes by Term
   Rebalancing Partitions
   Strategies for Rebalancing
   Operations: Automatic or Manual Rebalancing
   Request Routing
   Parallel Query Execution
   Summary
7. Transactions
   The Slippery Concept of a Transaction
   The Meaning of ACID
   Single-Object and Multi-Object Operations
   Weak Isolation Levels
   Read Committed
   Snapshot Isolation and Repeatable Read
   Preventing Lost Updates
   Write Skew and Phantoms
   Serializability
   Actual Serial Execution
   Two-Phase Locking (2PL)
   Serializable Snapshot Isolation (SSI)
   Summary
8. The Trouble with Distributed Systems
   Faults and Partial Failures
   Cloud Computing and Supercomputing
   Unreliable Networks
   Network Faults in Practice
   Detecting Faults
   Timeouts and Unbounded Delays
   Synchronous Versus Asynchronous Networks
   Unreliable Clocks
   Monotonic Versus Time-of-Day Clocks
   Clock Synchronization and Accuracy
   Relying on Synchronized Clocks
   Process Pauses
   Knowledge, Truth, and Lies
   The Truth Is Defined by the Majority
   Byzantine Faults
   System Model and Reality
   Summary
9. Consistency and Consensus
   Consistency Guarantees
   Linearizability
   What Makes a System Linearizable?
   Relying on Linearizability
   Implementing Linearizable Systems
   The Cost of Linearizability
   Ordering Guarantees
   Ordering and Causality
   Sequence Number Ordering
   Total Order Broadcast
   Distributed Transactions and Consensus
   Atomic Commit and Two-Phase Commit (2PC)
   Distributed Transactions in Practice
   Fault-Tolerant Consensus
   Membership and Coordination Services
   Summary
   III. Derived Data
10. Batch Processing
    Batch Processing with Unix Tools
    Simple Log Analysis
    The Unix Philosophy
    MapReduce and Distributed Filesystems
    MapReduce Job Execution
    Reduce-Side Joins and Grouping
    Map-Side Joins
    The Output of Batch Workflows
    Comparing Hadoop to Distributed Databases
    Beyond MapReduce
    Materialization of Intermediate State
    Graphs and Iterative Processing
    High-Level APIs and Languages
    Summary
11. Stream Processing
    Transmitting Event Streams
    Messaging Systems
    Partitioned Logs
    Databases and Streams
    Keeping Systems in Sync
    Change Data Capture
    Event Sourcing
    State, Streams, and Immutability
    Processing Streams
    Uses of Stream Processing
    Reasoning About Time
    Stream Joins
    Fault Tolerance
    Summary
12. The Future of Data Systems
    Data Integration
    Combining Specialized Tools by Deriving Data
    Batch and Stream Processing
    Unbundling Databases
    Composing Data Storage Technologies
    Designing Applications Around Dataflow
    Observing Derived State
    Aiming for Correctness
    The End-to-End Argument for Databases
    Enforcing Constraints
    Timeliness and Integrity
    Trust, but Verify
    Doing the Right Thing
    Predictive Analytics
    Privacy and Tracking
    Summary

[from](https://www.oreilly.com/library/view/designing-data-intensive-applications/9781491903063/)
