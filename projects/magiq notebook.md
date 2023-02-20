Matrix Algebra Framework for Portable, Scalable and Efficient Query Engines for RDF Graphs

https://dl.acm.org/doi/10.1145/3302424.3303962

## 摘要

MAGiQ represents the RDF graph as a sparse matrix and defines a domain-specific language of algebraic operations.

## 1introduction

We propose MAGiQ1: a matrix algebra framework for implementing SPARQL query engines.

稀疏矩阵乘法作为第三个范式. 

怎么做:

MAGiQ stores the RDF graph as a sparse integer matrix, and translates SPARQL queries into concise matrix algebra programs that operate on the matrix representation

## 2 overview

### 2.2

1.  loading the input RDF graph, encoding its strings into numerical IDs, and building a bi-directional dictionary. The encoded graph is represented as a sparse square integer matrix
2. MAGiQ translates SPARQL queries into matrix algebra programs,  the optimizer utilizes matrix algebra properties to reorder the operations to generate more efficient programs

是怎么translates 的?

怎么存储边? 是另外有个矩阵吗? 

MAGiQ inherits the excellent scalability of the underlying libraries in terms of data size and the number of compute nodes. 

## 实验

we demonstrate how MAGiQ can effortlessly be ported on a variety of architectures such as Intel CPUs, NVIDIA GPU

This machine is equipped with a desktop-grade NVIDIA Quadro P6000 GPU with 24GB GDDR5X GPU memory

our versions of MAGiQ with different back-end libraries: SuiteSparse, Matlab- CPU, Matlab-GPU, and CombBLAS. 

MAGiQ (Matlab-GPU) uses multiple CPU threads while MAGiQ (Matlab-GPU) uses a single GPU.

他是怎么用GPU的? 

CombBLAS是啥?  Combinatorial BLAS (CombBLAS) 是一个可扩展的分布式内存并行图形库，提供了一组小型但功能强大的线性代数原语，专门针对图形分析。



#### 代码

https://github.com/fjamour/MAGiQ

https://github.com/DrTimothyAldenDavis/GraphBLAS

https://github.com/PASSIONLab/CombBLAS

### 目标

We neee to use CuBlas from nvidia instead of Comblas or graphblas

https://github.com/nvidia/cudalibrarysamples

https://docs.nvidia.com/cuda/cublas/

https://docs.nvidia.com/cuda/cublas/index.html#example-code

让他运行在cuda project中. 

V100

代码结构

1. 

MQ_TWOCB MQ_TWOCM ?啥意思?
