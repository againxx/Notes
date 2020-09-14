# Tensor Operations

Every tensor operation has two variants:
* **Inplace** (with an underscore, e.g. `abs_()`) operates on the tensor's content
* **Functional** (without an underscore, e.g. `abs()`) creates a copy of the tensor with the performed modification, leaving the original tensor untouched

Two places to look for operations:
* The `torch` package, where the fucntion accepts the tensor as an argument
* The `tensor` class, where it operates on the called tensor

## Common Operations
* `view()` return a view tensor that shares the same underlying data with the original tensor
* `is_contiguous()` returns True if self tensor is contiguous in memory in the order specified by memory format
* `contiguous()` copying data when the tensor is not contiguous
