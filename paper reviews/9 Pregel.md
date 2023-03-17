

| Reviewer **(R2)**                                            |
| ------------------------------------------------------------ |
| **Pregel: A System for Large-Scale Graph Processing**        |
| Grzegorz Malewicz, Matthew H. Austern, Aart J. C. Bik, James C. Dehnert, Ilan Horn, Naty Leiser, and Grzegorz Czajkowski |
| CS  341                                                      |

## Summary 

- Pregel is a distributed computing framework developed by Google for processing large-scale graphs. It is designed to handle graphs with billions of vertices and edges.
- Pregel provides a simple programming model for expressing graph algorithms as a sequence of iterations. 
- Pregel can handle various tasks, including PageRank, Semi-Clustering, and Bipartite Matching.

## Advantage

1. This is the initial idea of message passing.(其实不是, 是来自于 bulk sync model, 很多想法都是老的,但是应用是新的) This vertex-centric approach evolved into the message-passing mechanism in current graph neural networks. 
2. The model has been designed for efficient, scalable, and fault-tolerant implementation on clusters of thousands of commodity computers, and its implied synchronicity makes reasoning about programs more accessible.
3. It is easy to program. It provides abstract API so that it can run transparently.
4. Pregel provides fault tolerance to cope with failures during computation.

## Drawback

1. Pregel requires a significant amount of resources to operate effectively. These requirements may make Pregel less accessible to smaller organizations or research groups with limited resources.
2. Limited generality: it may not be the best option for current graph neural network tasks.

## Justification

1. Programs are expressed as a sequence of iterations, in each of which a vertex can receive messages sent in the previous iteration, send messages to other vertices, and modify its state and that of its outgoing edges or mutate graph topology. 
2. Pregel is designed to handle machine failures and network delays, ensuring that computation continues even in the presence of faults. Fault tolerance is achieved through checkpointing. Worker failures are detected using regular “ping” messages that the master issues to workers. When one or more workers fail, the current state of the partitions assigned to these workers is lost. This approach saves compute resources during recovery by only recomputing lost partitions, and can improve the la- tency of recovery since each worker may be recovering fewer partitions.
3. The API is intuitive, flexible, and easy to implement and parallelize graph algorithms. 

Vipin Kumar 发明了metis, 明尼苏达大学的. 

bulk sync model.  bulk是说一个node保存variable和 code, 每个node 发送message 到queue, barrier同步. 所有人都收到了, 那就更新, 然后开始下一个iteration.

一开始用在hpc, 没人用来做graph. 

urika machine 用来做图处理   一个机架上用网络连接, 可以malloc 2TB的内存. 这也是NUMA.  买 Shrien2 之后, 他们送了一个urika给老师. 然后用16个机器超过urika性能的时候还发了一篇论文. 

 超过1个CPU基本上就有NUMA. 







