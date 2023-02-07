

| Reviewer **(R2)**                                            |
| ------------------------------------------------------------ |
| [The Gamma Database Machine Project](http://cs341.pbworks.com/f/Gamma+-+tkde90.pdf) |
| D.J. DeWitt, S. Ghandeharizadeh, D.A. Schneider, A. Bricker, H. Hsiao, R. Rasmussen, *IEEE TKDE, 2(1)*, pp. 44-62, 1990. |
| CS  341                                                      |

## Summary 

1. First, all relations are horizontally partitioned across multiple disk drives enabling relations to be scanned in parallel. 
2. novel parallel algorithms based on hashing are used to implement the complex relational operators such as join and aggregate functions
3. dataflow scheduling techniques are used to coordinate multioperator queries.

## Strengths

1. propose a novel idea that route the resulting tuple to the process indicated in the split table.
2. The number of control messages are reduced.
3.  Employs a one page read-ahead mechanism. This mechanism enables the processing of one page to be overlapped with the I/O for the subsequent page.

## Weaknesses

1.  This paper shows how they develop Gamma from version 1.0 to version2.0. Nowadays we don't present the process in the papers, we usually directly present the final results for concise.
2. decluster all relations across all nodes with disks. It will be better as proposed in [COPE88], is to use the "heat" of a relation to determine the degree to which the relation is declustered.
3. These hash- based join algorithms cannot be used to execute non-equijoin operations

## Justification

1. The experimental results show that both selection and join queries are linear speedup.
2. 

