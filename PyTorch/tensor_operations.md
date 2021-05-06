# Tensor Operations

Every tensor operation has two variants:
* **Inplace** (with an underscore, e.g. `abs_()`) operates on the tensor's content
    - Another option for placing the result into an existing tensor is to use `out` argument in function call
* **Functional** (without an underscore, e.g. `abs()`) creates a copy of the tensor with the performed modification, leaving the original tensor untouched

Two places to look for operations:
* The `torch` package, where the fucntion accepts the tensor as an argument
* The `tensor` class, where it operates on the called tensor

## Memory Operations
* `view()` return a view tensor that shares the same underlying data with the original one
* `clone()` return a copy tensor, by default the copied tensor will track the gradient if the original one does
* `detach()` detach the tensor from the current graph, then the result will never require gradient
    - The returned tensor shares the same storage with the original one
    - Use `detach().clone()` to get a fully unrelated and untracked tensor
* `is_contiguous()` returns True if self tensor is contiguous in memory in the order specified by memory format (e.g. row first)
* `contiguous()` copying data when the tensor is not contiguous

## Shape Operations
* `torch.unsqueeze(dim=)` add additional size 1 dimension into the tensor, which is useful when
    - Add batch dimension
    - Ease broadcasting
* `torch.squeeze(dim=)` remove additional size 1 dimension from the tensor
* `torch.reshape() / tensor.reshape()` will return a view of the original tensor (but there are some exceptions)
