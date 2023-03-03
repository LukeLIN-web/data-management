

| Reviewer **(R2)**                                            |
| ------------------------------------------------------------ |
| [MapReduce: Simplified Data Processing on Large Clusters](http://research.google.com/archive/mapreduce.html) |
| J Dean and S. Ghemawat, Proc. of Symposium on Operating System Design and Implementation (OSDI), 2004 |
| CS  341                                                      |

## Summary 

-  The paper introduces the MapReduce programming model.
-  Developers write code that implements the Map and Reduce functions, and the MapReduce framework distributes the work across a large cluster of servers.
-  The paper describes how MapReduce has been used to solve various data processing problems, including large-scale graph computations and machine learning.

## Strengths

1. Innovative and influential: The paper introduces the MapReduce programming model, a novel approach to distributed data processing at the time of publication. 
1. This framework can simplify the development of large-scale, distributed data processing applications.
1. Practical and empirical: The paper is grounded in practical experience and empirical evaluation. 

## Weaknesses

1. Limited discussion of limitations: it doesn't provide an in-depth discussion of its limitations.
2. Not suitable for real-time computation. MapReduce is unable to return results within milliseconds. MapReduce is not ideal for online data processing.
3. Mapreduce cannot handle DAG (Directed Acyclic Graph) computation or stream processing.

## Justification

1. The authors describe how MapReduce has been used to solve various data processing problems and provide performance results that demonstrate the scalability and effectiveness of the approach.
2. The paper is well-written and presents its ideas clearly and concisely. 
3. MapReduce's processing method for dependencies data is to write the output results of each MapReduce job to disk after use, which can result in a large amount of disk I/O and cause poor performance.



来自于 函数式编程.

lambda 函数是图灵完备的. mapreduce 也是图灵完备的. 但是不是所有都高效. 

函数式编程, 就是源于 声明式编程. 

超算上MPI比 mapreduce 快很多. MPI 协议复杂很多, 开发时间更久.  所以需要运行很久的程序可以用MPI,精心优化一下.  

谷歌买一堆便宜电脑,而不是买一些高级电脑,  这样成本更低. 

mapreduce并不是efficient, 而是 economical. 

easy parallel. 

从此, 人们开始关注 kv数据库, 非关系型数据库.

mapreduce ,  有很大的带宽从cpu到disk.

2004年的论文,  到了2010年, 谷歌认为mapreduce 不适合 graph 计算. 

现在认为mapreduce不适合 keeping state.
