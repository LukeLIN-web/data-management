

| Reviewer **(R2)**                                     |
| ----------------------------------------------------- |
| TensorFlow: A system for large-scale machine learning |
| M. Abadi et al osdi2016                               |
| CS  341                                               |

## summary

1. TensorFlow is an open-source software library for numerical computation and large-scale machine learning.
2. It is designed to be flexible and scalable, allowing developers to build and train various types of machine-learning models on a variety of platforms.
3. TensorFlow offers high-level APIs for building and training neural networks.

## advantage

1. TensorFlow can scale to handle large datasets and complex models.
2. TensorFlow can run on a variety of platforms.
3. TensorFlow provides high-level APIs for building and training neural networks.
4. TensorFlow Serving and TensorFlow Lite can be quickly deployed to cloud, server, mobile, and IoT devices.

## drawback

1. Compatibility issues: TensorFlow's rapid development pace can sometimes lead to compatibility issues
1. Steep learning curve: TensorFlow has a steep learning curve, especially for beginners. 
1. Lack of documentation: it can be challenging to navigate and may not always provide clear explanations or examples for specific use cases. 

## Justification

1. TensorFlow's dataflow representation subsumes existing work on parameter server systems. It offers a set of uniform abstractions that allow users to harness large-scale heterogeneous systems, both for production tasks and for experimenting with new approaches.
2. The requirement for compatibility with different versions of the CUDA library and the migration of function interfaces between different versions can lead to a significant amount of time spent setting up the environment when reproducing other people's code.
3. TensorFlow uses a single dataflow graph to represent all computation and state in a machine learning algorithm, including the individual mathematical operations, the parameters and their update rules, and the input pre-processing.

