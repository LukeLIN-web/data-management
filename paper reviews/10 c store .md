

| Reviewer **(R2)**                                            |
| ------------------------------------------------------------ |
| C-Store: A Column-oriented DBMS                              |
| Grzegorz Malewicz, Matthew H. Austern, Aart J. C. Bik, James C. Dehnert, Ilan Horn, Naty Leiser, and Grzegorz Czajkowski |
| CS  341                                                      |

## summary

1. C-Store is a column-oriented DBMS that stores data by column rather than by row. 
2. It combines a read-optimized column store and a writeable store connected by a tuple mover. 
3. C-Store is optimized for queries, using bitmap indexes in a B Tree, and is substantially faster than popular commercial products.

## advantage

1. It uses different ways to optimize read access, such as bitmap indexes in a B Tree.
2. Reasonable encoding of data in storage and even in memory to improve the efficiency of storage and query
3. implementing transactions, high availability, and snapshot isolation. The use of snapshot isolation to avoid 2PC and locking for queries.

## drawback

1. It has a complex architecture may be challenging for users to understand and work with.
2. It may not be optimal for queries involving many columns or requiring complex joins across multiple tables.
3. It may not be as well-suited for transaction processing workloads.

## Justification

1. Combine a read-optimized column store and an update/insert-oriented writeable store in a single piece of the system software connected by a tuple mover.  
2. It proposes a hybrid architecture with a WS component optimized for frequent insert and update and an RS component optimized for query performance.
3. It is not stored according to the <table, [Indexes]> model but according to the Projections of columns. Redundant storage of elements of a table in several overlapping projections in different orders, so that a query can be solved using the most advantageous projection. High availability and improved performance through K-safety using a sufficient number of overlapping projections.





VLDB'05: C-Store: A Column-oriented DBMS - - 知乎 https://zhuanlan.zhihu.com/p/386369591



在每个 projection 中，如果有 k 列，那么会有 `k` 个存储单列的数据结构。它们按照其中的一列 `sort key` 来排序。

每个 *projection* 都会水平分片到至少一个 `segments` 里面。C-Store 的 partition 是基于 sort key 来进行 partition的。每个 segment 都会有个 *segment identifier*, Sid. 这个数字要求大于0.

当需要处理 SQL 的时候，请求会处理相关的 projections. 但同时，c-store 需要把几个 sort key 不同的 projections 组合成要返回的数据，这实际上依赖一个类似 [join](https://www.zhihu.com/search?q=join&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A"386369591"}) 的功能。c-store 依靠 storage keys 和 join indices 来支持这些操作：

1. storage keys 是针对 segment 而言的，这个被称作 SK. 在 RS 的同个 segment 中，不会实际存储 SK, 他们就是 1, 2, 3... 这样按顺序排列。在 WS 中，他们需要维护这个，这和 WS 的结构和逻辑有关。
2. Join Indices 是一个额外的索引，用于把 projection X 的 `<SegmentID, SortKey>` 按顺序映射到另一个 projections 中，这个结构维护是比较昂贵的。 

C-Store 通过上述的把一列存储多份，然后实现了恢复机制，来做到 *[k-safety](https://www.zhihu.com/search?q=k-safety&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A"386369591"})*. 这也需要定义的 [schema](https://www.zhihu.com/search?q=schema&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A"386369591"}) 的支持。



《Column-Stores vs. Row-Stores》读后感 - abei的文章 - 知乎 https://zhuanlan.zhihu.com/p/54433448



在零售数据仓库中, 某人想知道在暴风雪来临时最北方在销售什么，以及飓风来临时，大西洋沿岸卖什么？

​    进一步说，没人会执行一个select * 来查询事实表的所有数据。而是总是指定一个聚合，从表的100个属性中取出6种。下一个查询又是不通的集合，而且在过滤条件中几乎没有位置信息。

​    在这种情况下，很明显列存从磁盘中取出数据到内存中的数据要比行存少16倍（6列和100列）。

   进一步考虑一个存储块，在列存中，一个块中只有一个属性，而行存中有100个。在数据压缩上也有明显优势。

​	另外，行存在每个记录都有一个记录头（在SQLServer占16个字节）。相反的，列存中没有这个记录头。

​    最后，基于行的[执行程序](https://www.zhihu.com/search?q=执行程序&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A"121070567"})有一个内部循环，通过该循环检查输出中的记录的有效性。于是，这个内循环的开销是可以按每条记录的检查次数来估算的。而在[列存储](https://www.zhihu.com/search?q=列存储&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A"121070567"})中，基本操作就是检索列然后过滤出符合条件的项。于是，内循环的开销是按每列检查来支付而不是每行一次性检查。这样的话，列存的执行器在CPU上更高效，从磁盘中检索的数据也越少。在很多真实环境中，列存比行存快50-100倍。

main assumption是 数据在disk上.  当然也有很多in memory DB  ,比如 monet DB. 

Join Indices 就是pre compute的join,  VERTICA公司. 

 pre的技能.  千万不能暴露你不懂, 就选你最懂的讲. 不懂的都不讲.  不用覆盖所有的!!  做多错多, 差的宁可不做. 也就是不要灌水的思想. 

