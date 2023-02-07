

| Reviewer **(R2)**                                            |
| ------------------------------------------------------------ |
| [The Gamma Database Machine Project](http://cs341.pbworks.com/f/Gamma+-+tkde90.pdf) |
| D.J. DeWitt, S. Ghandeharizadeh, D.A. Schneider, A. Bricker, H. Hsiao, R. Rasmussen, *IEEE TKDE, 2(1)*, pp. 44-62, 1990. |
| CS  341      ÷                                               |

Matrix Algebra Framework for Portable, Scalable and Efficient Query Engines for RDF Graphs

https://dl.acm.org/doi/10.1145/3302424.3303962

## Summary 

1. MAGiQ represents the RDF graph as a sparse matrix and defines a domain-specific language of algebraic operations. 
2. MAGiQ is a matrix algebra framework for implementing SPARQL query engines. 
3. MAGiQ stores the RDF graph as a sparse integer matrix and translates SPARQL queries into concise matrix algebra programs that operate on the matrix representation.

## Advantage

1. There is no implementation of something as complex as a SPARQL query engine. 
2. The sparse matrix algebra paradigm eliminates the need for building exhaustive indices. So that MAGiQ loads data faster and uses less memory. 
3. MAGiQ inherits the excellent scalability of the underlying libraries in terms of data size and the number of compute nodes. The scalability of MAGiQ does not pose an adverse effect on performance.
4. Although the concepts require much background knowledge, the  figure's illustration is clear. And tables are precise.

## Weaknesses

1.  MAGiQ has poor performance for selective queries.
2. In some cases, it still slower than the SOTA distributed-memory engine AdPart. 
3. MAGiQ (CombBLAS) is suitable for querying very large datasets, which might not be the most commonly used dataset.

## Justification

1. This paper explains the main idea clearly. This paper gives many equation examples.
2.  The author implements MAGiQ, and their experiment results show that loading time is quicker(Table 3), and Runtimes for data-intensive queries is faster (Table 4). The evidence is sufficient.
3. This paper is provoking and introduces enough background knowledge.

