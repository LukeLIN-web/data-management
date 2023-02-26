

| Reviewer **(R2)**                                            |
| ------------------------------------------------------------ |
| The Case for RAMClouds: Scalable High-Performance Storage Entirely in DRAM |
| *CACM* in July 2011.                                         |
| CS  341                                                      |

## Summary 

-  RamCloud is an open-source distributed in-memory data storage system developed at Stanford University. It is designed to provide low-latency, high-throughput access to large-scale data sets by storing them entirely in DRAM across a cluster of commodity servers. 
-  RamCloud proposes a novel architecture that achieves high performance by avoiding disk I/O and utilizing fast, low-latency networking between the servers. 
-  RamCloud is a promising technology for applications that require very low-latency access to large data sets.

## Strengths

1. Low latency. RAMCloud keeps all data in DRAM so that applications can read RAMCloud objects remotely over a data center network.
1. Scalability. RamCloud is designed to scale out horizontally across a cluster of commodity servers. This allows it to handle large amounts of data and high request rates by adding more servers to the cluster.
1. Consistency: RamCloud provides strong consistency guarantees, meaning that all clients see the same version of the data at the same time. This is important for applications that require accurate and up-to-date data.

## Weaknesses

1. High cost per bit and increased energy usage per bit.
2. Require more floor space in a data center than a system based on disk or flash memory.  就是内存需要多个机子, 内存的体积比较大,比硬盘大很多. 
1. This paper doesn't show the experimental results.

## Justification

1. RamCloud achieves scalability by utilizing a distributed architecture that allows it to scale out horizontally across a cluster of commodity servers. By partitioning data, RamCloud can distribute the workload evenly across the servers and avoid hotspots or bottlenecks.
2. RamCloud provides a key-value store interface that supports transactions, snapshots, and durability using a combination of replication and backup techniques.
3. RAMClouds will require high bandwidth and low latency from the networking infrastructure.



1000 + servers,  100TB+

目标 5-10 micro seconds

1M op/sec/server

提供 100-1000x 吞吐量



master把log 分成多份.  分到不同的server中保存. 

恢复的时候, server从磁盘读入, 发送给master. 

这个项目搞了8年. 有很多paper 产出. 

怎么让几千个 服务器同时工作? 大厂才有的烦恼. 

只用一些机器的memory, 不用他们的cpu. 

SAP hana .也是一个in memory . in cloud. 

这个也很像 spark. 

mapreduce 要解决  low bandwith of disk . 

https://web.stanford.edu/~ouster/cgi-bin/projects.php
