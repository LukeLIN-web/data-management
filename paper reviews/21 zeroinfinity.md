

| Reviewer **(R2)**                                            |
| ------------------------------------------------------------ |
| zeRO-Infinity: Breaking the GPU Memory Wall for Extreme Scale Deep Learning |
| SC21                                                         |
| CS  341                                                      |

## summary

1. Present ZeRO-Infinity, a novel heterogeneous system technology that can train very large models on limited resources.
1. achieves excellent training throughput and scalability, unencumbered by the limited CPU or NVMe bandwidth
1. ZeRO-Infinity extends the ZeRO family of technology with new innovations in heterogeneous memory access. 

## advantage

1.  Can fit models with tens and even hundreds of trillions of parameters for training on current-generation GPU clusters.
1.  It sustains over 25 petaflops on 512 NVIDIA V100 GPUs (40% of peak) while demonstrating super linear scalability. 
1.  The proposed approach is easy to use and integrates with existing deep learning frameworks.

## drawback

1. Splitting the model and data across multiple GPUs and levels of memory increases the communication overhead during training.
1. requires more memory to store additional copies of the model parameters and activations
1. It is only suitable for fine-tuning because the pre-train process with this technology is too slow.

## Justification

1. Present ZeRO-Infinity, a novel heterogeneous system technology that leverages GPU, CPU, and NVMe memory to allow for unprecedented model scale on limited resources without requiring model code refactoring.
1. The proposed approach is easy to use and integrate with existing deep learning frameworks, requiring minimal changes to the codebase and enabling easy adoption by the deep learning community.
1. Demonstrates that it is possible to transcend the GPU memory wall by leveraging cheap and slow, but massive, CPU or NVMe memory in parallel across multiple devices to achieve the aggregate bandwidth necessary for efficient training on the current generation of GPU clusters.



