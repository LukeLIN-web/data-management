

| Reviewer **(R2)**                                            |
| ------------------------------------------------------------ |
| [**Bigtable: A Distributed Storage System for Structured Data**](http://research.google.com/archive/mapreduce.html) |
| Fay Chang, Jeffrey Dean, Sanjay Ghemawat, Wilson C. Hsieh, Deborah A. Wallach Mike Burrows, Tushar Chandra, Andrew Fikes, Robert E. Gruber |
| CS  341                                                      |

## Summary 

- Describe the simple data model provided by Bigtable, which gives clients dynamic control over data layout and format.
- Describe the design and implementation of Bigtable. Bigtable uses a distributed, multi-dimensional sorted map to store data as key/value pairs and is designed to handle massive amounts of structured data across thousands of commodity servers.
- The system provides a flexible data model and a rich set of operations, including advanced features such as compression and in-memory caching.
- Overall, the paper is a seminal work in distributed storage systems and has significantly impacted subsequent NoSQL databases and distributed systems.

## Strengths

1. Innovative solution: The paper presents an innovative solution for storing and managing massive amounts of structured data using a distributed, multi-dimensional sorted map. 
1. The paper provides a detailed description of the Bigtable system, including its design, implementation, and API.
1. Scalability and fault tolerance: Bigtable is designed to be highly scalable, making it suitable for use in large-scale applications. 

## Weaknesses

1. Technical complexity: The paper is highly technical and assumes a deep understanding of distributed systems, which may make it challenging for non-experts to comprehend. 
2. Big-table doesn't provide cross-row transaction support because the cross-row transaction is not scalable.   就是不支持多行transaction 为了efficient, transaction别的都要等. 
3. Lack of open-source implementation: While the paper provides a detailed description of the Bigtable system, it does not provide an open-source implementation that can be used and tested by researchers and practitioners. 

## Justification

1. This approach was unique at the time of publication and has significantly impacted subsequent NoSQL databases and distributed systems. For example, MegaStore and Spanner reuse some parts of Bigtable.
2. Bigtable provides a flexible data model, a rich set of operations and includes advanced features such as compression and in-memory caching. These features make Big Table a powerful tool for storing and analyzing large amounts of structured data.
3. The paper provides examples of several applications built on Bigtable, including Google's web indexing system, Google Earth, and the Google Code hosting service. These examples demonstrate the versatility and usefulness of Bigtable in various domains.

为什么需要GFS ?  组合所有disk, 放入大文件, 使用mapreduce , 

但是GFS是un structured的. 所以需要bigtable作为数据库给大部分人用. 

lock service 叫做chubby.

chubby找到chubby file, 找到root tablet(1st metadata tablets). 然后找到 metadata tablets , 找到usertable.

一般就2层, 太多层会很慢. 

GFS一般会创建3个副本.

client要write,   发送给scheduler, 把log 写入 tablet . 然后写到memtable, memtable 攒够了之后, 就commit, 删除log.

SSTable是什么? 

sstable 记录了一系列kv pair.  
