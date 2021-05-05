# Tensor Broadcasting

Broadcasting is a way to perform an operation between tensors that have similar shapes
* Commonly used when multiplying a tensor of learning weights by a batch of input tensors

## Rules
* Each tensor must have at least one dimension - no empty tensors
* Comparing the dimension sizes of the two tensors, going from **last** to **first**
    - Each size must be equal, or
    - One of the dimensions must be of size 1, or
    - The dimension does not exist in one of the tensors
