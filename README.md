# Database-Internals-zh
Database Internals:A Deep Dive into How Distributed Data Systems Work的中文翻译



### Part I. Storage Engines存储引擎

##### 1. Introduction and Overview.介绍和总览

- DBMS Architecture DBMS架构
- Memory-Versus Disk-Based DBMS 基于内存与磁盘的DBMS
  - Durability in Memory-Based Stores基于内存存储的持久化
- Column- Versus Row-Oriented DBMS 面向列与面向行的DBMS
  - Row-Oriented Data Layout面向行的数据布局
  - Column-Oriented Data Layout面向列的数据布局
  - Distinctions and Optimizations区别和优化
  - Wide Column Stores宽列存储
- Data Files and Index Files数据文件和索引文件
  - Data Files数据文件
  - Index Files索引文件
  - Primary Index as an Indirection作为间接索引的主索引
- Buffering, Immutability, and Ordering
- Summary总结

##### 2. B-Tree Basics.B树基本知识

- Binary Search Trees
  1. Tree Balancing
  2. Trees for Disk-Based Storage
- Disk-Based Structures
  1. Hard Disk Drives
  2. Solid State Drives
  3. On-Disk Structures
- Ubiquitous B-Trees
  - B-Tree Hierarchy
  - Separator Keys
  - B-Tree Lookup Complexity
  - B-Tree Lookup Algorithm
  - Counting Keys
  - B-Tree Node Splits
  - B-Tree Node Merges
- Summary

##### 3. File Formats

- Motivation
- Binary Encoding
  - Primitive Types
  - Strings and Variable-Size Data
  - Bit-Packed Data: Booleans, Enums, and Flags
-  General Principles
-  Page Structure
- Slotted Pages
- Cell Layout
- Combining Cells into Slotted Pages
- Managing Variable-Size Data
- Versioning
- Checksumming
- Summary

##### 4. Implementing B-Trees

- Page Header 
  - Magic Numbers
  -  Sibling Links
  - Rightmost Pointers 
  - Node High Keys 
  - Overflow Pages
- Binary Search  
  - Binary Search with Indirection Pointers 
- Propagating Splits and Merges
  - Breadcrumbs
- Rebalancing 
- Right-Only Appends 
  - Bulk Loading 
- Compression
- Vacuum and Maintenance
  - Fragmentation Caused by Updates and Deletes
  - Page Defragmentation
- Summary

##### 5. Transaction Processing and Recovery

- Buffer Management 
  - Caching Semantics 
  - Cache Eviction 
  - Locking Pages in Cache 
  - Page Replacement
- Recovery
  - Log Semantics
  - Operation Versus Data Log 
  - Steal and Force Policies 
  - ARIES
- Concurrency Control 
  - Serializability
  - Transaction Isolation
  - Read and Write Anomalies 
  - Isolation Levels
  - Optimistic Concurrency Control 
  - Multiversion Concurrency Control 
  - Pessimistic Concurrency Control 
  - Lock-Based Concurrency Control
- Summary

##### 6. B-Tree Variants

- Copy-on-Write
  - Implementing Copy-on-Write: LMDB 

- Abstracting Node Updates
- Lazy B-Trees
  - WiredTiger
  - Lazy-Adaptive Tree 
- FD-Trees
  - Fractional Cascading
  - Logarithmic Runs 
- Bw-Trees
  - Update Chains
  - Taming Concurrency with Compare-and-Swap 
  - Structural Modification Operations 
  - Consolidation and Garbage Collection
- Cache-Oblivious B-Trees
  - van Emde Boas Layout
- Summary

##### 7. Log-Structured Storage.

- LSM Trees  
  - LSM Tree Structure  
  - Updates and Deletes  
  - LSM Tree Lookups  
  - Merge-Iteration  
  - Reconciliation  
  - Maintenance in LSM Trees  
- Read, Write, and Space Amplification  
  - RUM Conjecture  
  - Implementation Details  
  - Sorted String Tables  
  - Bloom Filters  
  - Skiplist  
  - Disk Access  
  - Compression  
- Unordered LSM Storage  
  - Bitcask  
  - WiscKey  
- Concurrency in LSM Trees  
- Log Stacking  
  - Flash Translation Layer  
  - Filesystem Logging  
- LLAMA and Mindful Stacking  
  - Open-Channel SSDs  
- Summary 

### Part I Conclusion

### Part II. Distributed Systems

##### 8. Introduction and Overview. . . 

- Concurrent Execution  
  - Shared State in a Distributed System  
- Fallacies of Distributed Computing  
  - Processing  
  - Clocks and Time 
  - State Consistency  
  - Local and Remote Execution  
  - Need to Handle Failures  
  - Network Partitions and Partial Failures  
  - Cascading Failures 
- Distributed Systems Abstractions  
  - Links  
- Two Generals’ Problem  
- FLP Impossibility  
- System Synchrony  
- Failure Models  
  - Crash Faults  
  - Omission Faults  
  - Arbitrary Faults  
  - Handling Failures  
- Summary 

##### 9. Failure Detection. . .

- Heartbeats and Pings  
  - Timeout-Free Failure Detector  
  - Outsourced Heartbeats  
- Phi-Accural Failure Detector  
- Gossip and Failure Detection  
- Reversing Failure Detection Problem Statement  
- Summary 

##### 10. Leader Election

- Bully Algorithm  
- Next-In-Line Failover  
- Candidate/Ordinary Optimization  
- Invitation Algorithm  
- Ring Algorithm  
- Summary 

##### 11. Replication and Consistency

- Achieving Availability  
- Infamous CAP 
  - Use CAP Carefully 
  - Harvest and Yield  
- Shared Memory  
- Ordering 
- Consistency Models 
  - Strict Consistency  
  - Linearizability  
  - Sequential Consistency  
  - Causal Consistency 
- Session Models  
- Eventual Consistency  
- Tunable Consistency  
- Witness Replicas  
- Strong Eventual Consistency and CRDTs  
- Summary 

##### 12. Anti-Entropy and Dissemination

- Read Repair  
- Digest Reads  
- Hinted Handoff  
- Merkle Trees  
- Bitmap Version Vectors  
- Gossip Dissemination 
  - Gossip Mechanics  
  - Overlay Networks  
  - Hybrid Gossip  
  - Partial Views 
- Summary 

13. ##### Distributed Transactions

- Making Operations Appear Atomic  
- Two-Phase Commit 
  - Cohort Failures in 2PC 
  - Coordinator Failures in 2PC  
- Three-Phase Commit  
  - Coordinator Failures in 3PC  
- Distributed Transactions with Calvin  
- Distributed Transactions with Spanner  
- Database Partitioning  
  - Consistent Hashing  
- Distributed Transactions with Percolator  
- Coordination Avoidance  
- Summary 

##### 14. Consensus

- Broadcast  
- Atomic Broadcast 
  - Virtual Synchrony 
  - Zookeeper Atomic Broadcast (ZAB)  
- Paxos  
  - Paxos Algorithm  
  - Quorums in Paxos  
  - Failure Scenarios  
  - Multi-Paxos  
  - Fast Paxos  
  - Egalitarian Paxos  
  - Flexible Paxos  
  - Generalized Solution to Consensus  
- Raft 300 
  - Leader Role in Raft  
  - Failure Scenarios 
- Byzantine Consensus  
  - PBFT Algorithm  
  - Recovery and Checkpointing  
- Summary 

### Part II Conclusion

### A. Bibliography

### Index
