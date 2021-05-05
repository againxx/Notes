# GPU Acceleration

## GPU information
* `torch.cuda.is_available()` to check gpu accessibility
* `torch.cuda.device_count()`

## GPU tensor creation
* Every tensor type has its GPU equivalent, which reside in the `torch.cuda` package instead of just `torch`
* GPU tensors can also be created by `device` argument in factory method (`rand`, `zeros`, etc.)
* To convert tensors between CPU and GPU, there is a tensor method `to(device)`, that creates a copy of the tensor to a specified device
    - "cpu"
    - "cuda"
    - "cuda:1" (second GPU card)
    - using `torch.device` class, which accepts the device name and optional index (robust way to make the code **device agnostic**)
* To access the device that your tensor is currently residing in, it has a `device` property
