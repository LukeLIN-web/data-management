Matrix Algebra Framework for Portable, Scalable and Efficient Query Engines for RDF Graphs



https://dl.acm.org/doi/10.1145/3302424.3303962

## 摘要

MAGiQ represents the RDF graph as a sparse matrix and defines a domain-specific language of algebraic oper- ations.



## 1introduction

We propose MAGiQ1: a matrix algebra framework for implementing SPARQL query engines.



怎么做:

MAGiQ stores the RDF graph as a sparse integer matrix, and translates SPARQL queries into concise matrix algebra programs that operate on the matrix represen- tation

## 2 overview



### 2.2

1.  loading the input RDF graph, encoding its strings into numerical IDs, and building a bi-directional dic- tionary. The encoded graph is represented as a sparse square integer matrix
2. MAGiQ translates SPARQL queries into matrix algebra programs,  the optimizer utilizes matrix algebra properties to reorder the operations to generate more efficient programs

是怎么translates 的?

怎么存储边? 是另外有个矩阵吗? 



MAGiQ inherits the excellent scalability of the underlying libraries in terms of data size and the number of compute nodes. 





#### 代码

https://github.com/fjamour/MAGiQ
