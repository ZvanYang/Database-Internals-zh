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

- LSM Trees 130 
  - LSM Tree Structure 132 
  - Updates and Deletes 136 
  - LSM Tree Lookups 137 
  - Merge-Iteration 137 
  - Reconciliation 140 
  - Maintenance in LSM Trees 141 
- Read, Write, and Space Amplification 143 
  - RUM Conjecture 144 
  - Implementation Details 145 
  - Sorted String Tables 145 
  - Bloom Filters 146 
  - Skiplist 148 
  - Disk Access 150 
  - Compression 151 
- Unordered LSM Storage 152 
  - Bitcask 153 
  - WiscKey 154 
- Concurrency in LSM Trees 155 
- Log Stacking 157 
  - Flash Translation Layer 157 
  - Filesystem Logging 159 
- LLAMA and Mindful Stacking 160 
  - Open-Channel SSDs 161 
- Summary 162

### Part I Conclusion

### Part II. Distributed Systems

##### 8. Introduction and Overview. . . 

- Concurrent Execution 171 
  - Shared State in a Distributed System 173 
- Fallacies of Distributed Computing 174 
  - Processing 175 
  - Clocks and Time 176
  - State Consistency 177 
  - Local and Remote Execution 178 
  - Need to Handle Failures 178 
  - Network Partitions and Partial Failures 179 
  - Cascading Failures 180
- Distributed Systems Abstractions 181 
  - Links 182 
- Two Generals’ Problem 187 
- FLP Impossibility 189 
- System Synchrony 190 
- Failure Models 191 
  - Crash Faults 191 
  - Omission Faults 192 
  - Arbitrary Faults 193 
  - Handling Failures 193 
- Summary 193

##### 9. Failure Detection. . .

- Heartbeats and Pings 196 
  - Timeout-Free Failure Detector 197 
  - Outsourced Heartbeats 198 
- Phi-Accural Failure Detector 199 
- Gossip and Failure Detection 200 
- Reversing Failure Detection Problem Statement 201 
- Summary 202

##### 10. Leader Election

- Bully Algorithm 207 Next-In-Line Failover 208 
- Candidate/Ordinary Optimization 209 
- Invitation Algorithm 210 
- Ring Algorithm 211 
- Summary 212

##### 11. Replication and Consistency

- Achieving Availability 216 
- Infamous CAP 216
  - Use CAP Carefully 217
  - Harvest and Yield 218 
- Shared Memory 219 
- Ordering 221
- Consistency Models 222
  - Strict Consistency 223 
  - Linearizability 223 
  - Sequential Consistency 227 
  - Causal Consistency 229
- Session Models 233 
- Eventual Consistency 234 
- Tunable Consistency 235 
- Witness Replicas 236 
- Strong Eventual Consistency and CRDTs 238 
- Summary 240

##### 12. Anti-Entropy and Dissemination

- Read Repair 245 
- Digest Reads 246 
- Hinted Handoff 246 
- Merkle Trees 247 
- Bitmap Version Vectors 248 
- Gossip Dissemination 250
  - Gossip Mechanics 251 
  - Overlay Networks 251 
  - Hybrid Gossip 253 
  - Partial Views 254
- Summary 255

13. ##### Distributed Transactions

- Making Operations Appear Atomic 258 
- Two-Phase Commit 259
  - Cohort Failures in 2PC 261
  - Coordinator Failures in 2PC 262 
- Three-Phase Commit 264 
  - Coordinator Failures in 3PC 265 
- Distributed Transactions with Calvin 266 
- Distributed Transactions with Spanner 268 
- Database Partitioning 270 
  - Consistent Hashing 271 
- Distributed Transactions with Percolator 272 
- Coordination Avoidance 275 
- Summary 277

##### 14. Consensus

- Broadcast 280 
- Atomic Broadcast 281
  - Virtual Synchrony 282
  - Zookeeper Atomic Broadcast (ZAB) 283 
- Paxos 285 
  - Paxos Algorithm 286 
  - Quorums in Paxos 287 
  - Failure Scenarios 288 Multi-Paxos 291 
  - Fast Paxos 292 
  - Egalitarian Paxos 293 
  - Flexible Paxos 296 
  - Generalized Solution to Consensus 297 
- Raft 300 
  - Leader Role in Raft 302 
  - Failure Scenarios 304
- Byzantine Consensus 305 
  - PBFT Algorithm 306 
  - Recovery and Checkpointing 309 
- Summary 309

### Part II Conclusion

### A. Bibliography

### Index
