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





## 4 SPARQL to Matrix Algebra

### 4.1 Query Translation

MAGiQ如何将无常量的非循环图查询（即树查询）转化为矩阵代数程序；我们在4.2节中描述了具有循环和常量的查询所需的修改。首先，以深度优先方式遍历查询图的无向版本，生成一个闭合行走（第3行），使连接非叶节点的边出现两次：一次是向下遍历树时，一次是回溯时。在DFS-walk中，当发现一条边时，将其标记为前向边，而在回溯时遇到的边则标记为后向边。然后，提取的行走（Query-Translation中的qwalk）通过第4-21行中的循环引导程序生成。

```
```

生成的绑定矩阵对应于在RDF图中具有谓词p的入边节点，或者是A′中的行。qwalk中类型为forward的边会导致一个 ⊗ 操作，其中第一个操作数是前一个变量w1的绑定的选择矩阵，如果当前边e和前一条边pe共享相同的查询变量作为第一个节点（第13-17行）。否则，选择矩阵中使用pe的第二个变量的绑定（第16行）。如果qwalk中的边的方向与有向查询图中相应边的方向不匹配，则下一个绑定是具有指向先前绑定的出边的节点，或等效地是A′中的行；因此，在A′上进行行选择（第17行）。最后，类型为back的边在正在考虑的绑定矩阵上进行列选择，以消除另一个选择无效的绑定（第18-19行）。





## 实验

we demonstrate how MAGiQ can effortlessly be ported on a variety of architectures such as Intel CPUs, NVIDIA GPU

This machine is equipped with a desktop-grade NVIDIA Quadro P6000 GPU with 24GB GDDR5X GPU memory

our versions of MAGiQ with different back-end libraries: SuiteSparse, Matlab- CPU, Matlab-GPU, and CombBLAS. 

MAGiQ (Matlab-GPU) uses multiple CPU threads while MAGiQ (Matlab-GPU) uses a single GPU.

他是怎么用GPU的? 

CombBLAS是啥?  Combinatorial BLAS (CombBLAS) 是一个可扩展的分布式内存并行图形库，提供了一组小型但功能强大的线性代数原语，专门针对图形分析。



#### 代码

https://github.com/Samir55/MAGIQ 



https://github.com/DrTimothyAldenDavis/GraphBLAS

https://github.com/PASSIONLab/CombBLAS

The folder doesn't have the massive datasets (0.5 trillion edges) because those are too large and we only kept them on the supercomputer storage for a while. I believe the data generator and the scalable encoder we've written are in the folder. Unfortunately, the organization of the content isn't ideal, although I believe you will find your way through (with enough persistence :]).

Regarding the lubm320_nomultiedges, I believe this is the dataset you will want to use: [https://www.dropbox.com/home/Fuad_Cloud/Research/Matrix-Algebra/code/MAGIC/data/nomultiedges/lubm320_nomultiedges?preview=encoded.nt](https://urldefense.com/v3/__https://www.dropbox.com/home/Fuad_Cloud/Research/Matrix-Algebra/code/MAGIC/data/nomultiedges/lubm320_nomultiedges?preview=encoded.nt__;!!Nmw4Hv0!2TwRbPfXUquLJHeM8oQmpRzU8GoMFezf63SJzsdFsrjholGUlp62YCDL_4XVypJQSBtJORP8MEA0EjQQrSVwhGGepRCVRQ$). 

The way this file was created is we first used the LUBM data generator ([https://www.dropbox.com/home/Fuad_Cloud/Research/Matrix-Algebra/disorganized/shaheen_backup_my_code/trill_exp/lubm-uba](https://urldefense.com/v3/__https://www.dropbox.com/home/Fuad_Cloud/Research/Matrix-Algebra/disorganized/shaheen_backup_my_code/trill_exp/lubm-uba__;!!Nmw4Hv0!2TwRbPfXUquLJHeM8oQmpRzU8GoMFezf63SJzsdFsrjholGUlp62YCDL_4XVypJQSBtJORP8MEA0EjQQrSVwhGFIeH8RVw$)), which generates an actual RDF dataset, then we used an encoder to produce the integer coded nodes and edges. There is the encoder that you can use through the interface (the one you pointed to in your email), and there is a large scale encoder that scales to very large graphs ([https://www.dropbox.com/home/Fuad_Cloud/Research/Matrix-Algebra/disorganized/shaheen_backup_my_code/trill_exp/paracoder/src](https://urldefense.com/v3/__https://www.dropbox.com/home/Fuad_Cloud/Research/Matrix-Algebra/disorganized/shaheen_backup_my_code/trill_exp/paracoder/src__;!!Nmw4Hv0!2TwRbPfXUquLJHeM8oQmpRzU8GoMFezf63SJzsdFsrjholGUlp62YCDL_4XVypJQSBtJORP8MEA0EjQQrSVwhGFY3856bQ$)). 如果您想从头开始生成数据集，我建议您从 lubm-uba 生成器开始，然后使用 paracoder 工具。paracoder 工具生成一堆文件，您可以将这些文件与 paramerge 组合。尽管这些工具旨在在 Shaheen 上执行，但您也可以在桌面上使用它们。 







### 目标

We neee to use CuBlas from nvidia instead of Comblas or graphblas

https://github.com/nvidia/cudalibrarysamples

https://docs.nvidia.com/cuda/cublas/

https://docs.nvidia.com/cuda/cublas/index.html#example-code

让他运行在cuda project中.  V100

MQ_TWOCB MQ_TWOCM ?啥意思?

### cublas

cuBLAS库用于进行矩阵运算，它包含两套API，一个是常用到的cuBLAS API，需要用户自己分配GPU内存空间，按照规定格式填入数据，；还有一套CUBLASXT API，可以分配数据在CPU端，然后调用函数，它会自动管理内存、执行计算。既然都用cuda了，其实还是用第一套API多一点。

现在装好cuda会自带cuBLAS库的，只要include [头文件](https://www.zhihu.com/search?q=头文件&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A"438551588"})“cublas_v2.h”就可以调用它了.2021.11

cuBLAS采用的是列优先的存储

银河系CUDA编程指南(1)——用cuBLAS库进行一个简单矩阵乘法计算 - Meddle的文章 - 知乎 https://zhuanlan.zhihu.com/p/427262454



