# Pinned Host Memory

![Pageable Memory & Pinned Memory](https://devblogs.nvidia.com/wp-content/uploads/2012/12/pinned-1024x541.jpg)

* CPU端分配的内存默认是pageable的，而GPU不能直接获取pageable的主机端内存
* 当数据需要在主机端和设备端进行copy时，CUDA driver需要分配临时的page-locked/pinned内存作为中转
* 使用`cudaMallocHost()`或`cudaHostAlloc()`来分配主机端pinned memory

**注: pinned memory可能分配失败，可用下列代码检查**

```cpp
cudaError_t status = cudaMallocHost((void**)&h_aPinned, bytes);
if (status != cudaSuccess)
  printf("Error allocating pinned host memory\n");
```

**再注: 过多分配pinned memory会降低系统可用的物理内存，从而降低操作系统和其他程序的性能**
