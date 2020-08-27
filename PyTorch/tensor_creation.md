# The Creation of Tensors

## Types
**Notice**: torch dtype is different from numpy dtype, which is listed in the following parentheses.
* float types
    - 16-bit: `torch.HalfTensor` (`torch.float16` / `torch.half`)
    - 32-bit: `torch.FloatTensor` (`torch.float32` / `torch.float`)
    - 64-bit: `torch.DoubleTensor` (`torch.float64` / `torch.double`)
* int types
    - 8-bit signed: `torch.CharTensor` (`torch.int8`)
    - 8-bit unsigned: `torch.ByteTensor` (`torch.uint8`)
    - 16-bit: `torch.ShortTensor` (`torch.int16` / `torch.short`)
    - 32-bit: `torch.IntTensor` (`torch.int32` / `torch.int`)
    - 64-bit: `torch.LongTensor` (`torch.int64` / `torch.long`)
* bool type
    - `torch.BoolTensor` (`torch.bool`)

## Three ways to create a tensor
* By calling a constructor of the required type
* By converting a NumPy array or a Python list into a tensor, the type will taken from the array's type
* By asking PyTorch to create a tensor with specific data for you

### Constructor way
```python
# Uninitialized 3x2 tensor
a = torch.FloatTensor(3, 2)

# Provide a iterable (a list or tuple)
b = torch.FloatTensor([[1, 2, 3], [3, 2, 1]])
```

### Converting
```python
n = np.zeros(shape=(3, 2)) # dtype=np.float64 by default
b = torch.tensor(n) # dtype=torch.float64

c = torch.tensor(n, dtype=torch.float32)
```

### Specific data
```python
e = torch.empty(3, 3) # uninitialized

a = torch.zeros(2, 3) # 2x3 zeros
a = torch.zeros_like(e)

b = torch.ones(1, 2)
b = torch.ones_like(e)
```

## Scalar tensors (0D tensor)
```python
a = torch.tensor([1, 2, 3])
s = a.sum() # s: tensor(6)
s.item() # use item() to access the actual python value of a scalar tensor
b = torch.tensor(1) # directly create a scalar tensor
```
