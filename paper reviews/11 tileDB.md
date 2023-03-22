

| Reviewer **(R2)**                         |
| ----------------------------------------- |
| **The TileDB Array Data Storage Manager** |
| VLDB2016                                  |
| CS  341                                   |

## summary

1. TileDB is a novel storage manager optimized for dense, sparse, multi-dimensional arrays in scientific applications. 
2. TileDB organizes array elements into fragments, which are dense or sparse, and groups contiguous array elements into fixed-capacity data tiles.
3. Faster read and write performance than other array storage systems, including HDF5, SciDB, and Vertica.

## advantage

1. Fragment organization allows TileDB to turn random writes into sequential writes and efficiently read data using a novel read algorithm.
2. TileDB enables parallelization via multi-threading and multi-processing, with lightweight locking ensuring thread-/process-safety and atomicity.
3. This paper demonstrates that TileDB is considerably faster than adaptations of the Vertica relational column store for dense array storage management and at least as fast for the case of sparse arrays.

## drawback

1. It needs to provide more discussion on the flexibility and ease of use of TileDB.
2. The paper does not explore other potential use cases or applications for TileDB.
3. The paper needs to discuss the potential limitations or trade-offs of using TileDB.

## Justification

1. TileDB delivers comparable performance to HDF5 for dense array storage, with faster random writes and substantially faster reads and writes than SciDB. 
2. TileDB uses a tile-based storage format that optimizes data layout for I/O performance, reducing disk seeks and improving the locality of reference. This further improves both read and write performance.
3. TileDB is considerably faster than adaptations of Vertica for dense array storage and at least as fast for sparse arrays. TileDB performs equivalent to the parallel Vertica columnar database on sparse arrays while offering a programmer-friendly API- based interface similar to HDF5.
4. TileDB obtained a great amount of funds in 2021. 



### 其他软件

HDF5 只支持dense. 不支持稀疏.  inplace write, 

科学数据很难压缩. 因为有一定uncertainty

parallel HDF5, 不支持变长的数组. 

SciDB 也是mit做的. 

有的软件 只append 不直接inplace write, 快速写, 就没有random IO,  tradeoff 就是read 的时候要执行一个算法,比较慢.  

### 细节

一个tile差不多2 ×2 , 提供了API, 数据库使用者只用修改parameter就可以改变底层结构 . tile extents , tile order, cell order . 

把一些fragment 组合起来.  

这个技术也可以用在tensor上. 稀疏tensor .





一作作者, 在intel出钱和mit合作的实验室.和老师还认识. 





如果老哥创建了大量小文件 , 可能把超算的文件系统搞炸了.  所以需要 HDF5, tileDB来管理. 3百万个img 移动非常慢. 







外国人会直接夸奖别人, 中国人很少直接夸奖别人. 爱会传递. 痛苦也会传递. 
