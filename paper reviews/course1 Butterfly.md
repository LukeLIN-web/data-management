1月25日

#### summary

This paper proposes a novel approach to approximate butterfly counting in bipartite graphs. This algorithm exploits the properties of the bipartite graph. This approach is highly efficient as it captures a quadratic number of butterflies with linear cost. Further, this paper sample vertices with probabilities proportional to their degrees and adjust the final output to ensure its unbiasedness. 

What's more, they generalize the above solution to approximate bi-triangle counting. They did theoretical analysis and experiments using multiple large real datasets. The results show that their methods reach high accuracy significantly faster than SOTA.

#### Advantages

1. This algorithm exploits properties of the bipartite graph.
2. This algorithm achieves a lower asymptotic time complexity compared to the SOTA.
3. This algorithm can extend to bi-triangle counting. 

#### Disadvantages

1. 



#### Comments

This paper proposes a novel approach to approximate butterfly counting in bipartite graphs.  It computes a subset of butterflies and then derives an unbiased estimator of the total number of butterflies.  The figures are precise.  This paper uses a larger sampling unit to reduce sample variance.  And then, this paper tries to sample pairs of vertices with a large common neighbor set with higher probabilities to capture more butterflies.  

This paper discusses baseline solutions that combine known solutions for local sampling and exact bi-triangle counting.  And then presents the proposed algorithm. 
This paper did a thorough experiment to support their theoretical conclusion.  The results show that Weighted Pair Sampling consistently achieves the best performance(lower relative error) and outperforms alternatives in different densities.











A single vertex has bigger sample variance, whereas "popular" vertex may form numerous butterflies, an isolated vertex may not form any butterfly at all. A larger sampling unit S, such as an edge  
