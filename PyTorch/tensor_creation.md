# The Creation of Tensors

## Types
**Notice**: torch dtype is different from numpy dtype, which is listed in the following parentheses.
* float types
    - 16-bit: `torch.HalfTensor` (`torch.float16` / `torch.half`) 1 sign, 5 exponent, 10 significand
    - 16-bit: `torch.BFloat16Tensor (torch.bfloat16)` 1 sign, 8 exponent, 7 significand
    - 32-bit: `torch.FloatTensor` (`torch.float32` / `torch.float`) this is the **default** type
    - 64-bit: `torch.DoubleTensor` (`torch.float64` / `torch.double`)
* int types
    - 8-bit signed: `torch.CharTensor` (`torch.int8`)
    - 8-bit unsigned: `torch.ByteTensor` (`torch.uint8`)
    - 16-bit: `torch.ShortTensor` (`torch.int16` / `torch.short`)
    - 32-bit: `torch.IntTensor` (`torch.int32` / `torch.int`)
    - 64-bit: `torch.LongTensor` (`torch.int64` / `torch.long`)
* bool type
    - `torch.BoolTensor` (`torch.bool`)

## Four ways to create a tensor
* By calling a constructor of the required type
* By converting a NumPy array or a Python list into a tensor, the type will taken from the array's type
* By asking PyTorch to create a tensor with specific data for you
* By converting a given tensor to another type

### Constructor way
```python
# Uninitialized 3x2 tensor
a = torch.FloatTensor(3, 2)

# Provide a iterable (a list or tuple)
b = torch.FloatTensor([[1, 2, 3], [3, 2, 1]])
```

### Converting
* `torch.tensor()` always copies `data`
* use `torch.as_tensor() / torch.from_numpy()` to avoid a copy, if you have a numpy array
* `tensor.to()` method can also be used to cast tensor into different types
* `tensor.numpy()` method will return a numpy array with shared memory
```python
n = np.zeros(shape=(3, 2)) # dtype=np.float64 by default
b_copy = torch.tensor(n) # dtype=torch.float64
# or
b_nocopy = torch.as_tensor(n, dtype=torch.float64)
# from_numpy only accept one ndarray as argument
b_nocopy = torch.from_numpy(n)

c = torch.tensor(n, dtype=torch.float32)

d = c.to(torch.int32) # casting into integer tensor

e_np = d.numpy()
```

### Specific data
```python
e = torch.empty(3, 3) # uninitialized

a = torch.zeros(2, 3) # 2x3 zeros
a = torch.zeros_like(e)

b = torch.ones(1, 2)
b = torch.ones_like(e)

torch.manual_seed(123) # set seed for random number generator
c = torch.rand(3, 4)
c = torch.rand_like(e)
```

## Scalar tensors (0D tensor)
```python
a = torch.tensor([1, 2, 3])
s = a.sum() # s: tensor(6)
s.item() # use item() to access the actual python value of a scalar tensor
b = torch.tensor(1) # directly create a scalar tensor
```
