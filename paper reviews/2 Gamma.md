

| Reviewer **(R2)**                                            |
| ------------------------------------------------------------ |
| [The Gamma Database Machine Project](http://cs341.pbworks.com/f/Gamma+-+tkde90.pdf) |
| D.J. DeWitt, S. Ghandeharizadeh, D.A. Schneider, A. Bricker, H. Hsiao, R. Rasmussen, *IEEE TKDE, 2(1)*, pp. 44-62, 1990. |
| CS  341                                                      |

## Summary 

1. Wisconsin developed Gamma from 1984 to 1990. It proposes the shared-nothing split table and hash-join concepts. 
2. First, all relations are horizontally partitioned across multiple disk drives enabling relations to be scanned in parallel. 
3. Novel parallel algorithms based on hashing are used to implement complex relational operators such as join and aggregate functions.
4. Dataflow scheduling techniques are used to coordinate multi-operator queries.

## Strengths

1. Propose a novel idea that routes the resulting tuple to the process indicated in the split table.
2. The number of control messages are reduced.
3.  Employs a one-page read-ahead mechanism, enabling the processing of one page to be overlapped with the I/O for the subsequent page.

## Weaknesses

1.  This paper shows how they develop Gamma from version 1.0 to version 2.0. Nowadays, we don't present the process in the papers. Instead, we usually directly give the final results concisely.
2. Declutter all relations across all nodes with disks. As proposed in [COPE88], it will be better to use the "heat" of a relation to determine the degree to which the relation is decluttered.
3. These hash-based join algorithms cannot be used to execute non-equijoin operations.
4. Too wordy, maybe can use some algorithm to present.

## Justification

1. The experimental results show that both selection and join queries are linear speedups.
2. The paper has a comprehensive performance evaluation that assesses the impact of relationship size and response time for select, join, aggregate, and update queries. It also proves that Gamma is well scalable.

