# Building Blocks

## Basic Introduction
* PyTorch's basic functionality blocks reside in `torch.nn` package
* All modules follow the convention of callable, i.e. the instance of any class can act as a function
* All classes in the `torch.nn` package inherit from the `nn.Module` base class

## Useful Methods
All `nn.Module` children provide
* `parameters()`: returns an iterator of all variables that require gradient computation (module weights)
* `zero_grad()`: initializes all gradients of all parameters to zero
* `to(device)`: moves all module parameters to a given device
* `state_dict()`: returns the dictionary with all module parameters and is useful for model serialization
* `load_state_dict()`: initializes the module with the state dictionary

## Layers
| Torch Functions                                                      | Keras Functions                                         |
|----------------------------------------------------------------------|---------------------------------------------------------|
| `nn.Linear(in_features, out_features, bias)`                         | `layers.Dense(units, activation, use_bias)`             |
| `nn.ReLU()`                                                          | `activation='relu' / layers.ReLU()`                     |
| `nn.Sigmoid()`                                                       | `activation='sigmoid'`                                  |
| `nn.Tanh()`                                                          | `activation='tanh'`                                     |
| `nn.Softmax(dim)`                                                    | `activation='softmax' / layers.Softmax(axis)`           |
| `nn.Conv2d(in_channels, out_channels, kernel_size, stride, padding)` | `layers.Conv2D(filters, kernel_size, strides, padding)` |
| `nn.MaxPool2d(kernel_size, stride, padding)`                         | `layers.MaxPooling2D(pool_size, strides, padding)`      |
| `nn.Dropout(p)`                                                      | `layers.Dropout(rate)`                                  |

## Sequential
PyTorch way
```python
s = nn.Sequential(
    nn.Linear(2, 5),
    nn.ReLU(),
    nn.Linear(5, 20),
    nn.ReLU(),
    nn.Linear(20, 10),
    nn.Dropout(p=0.3),
    nn.Softmax(dim=1)) # assume that the first dimension is batch
```

Keras way
```python
model = models.Sequential()
model.add(layers.Dense(5, activation='relu', input_shape=(2,)))
model.add(layers.Dense(20, activation='relu')
model.add(layers.Dense(10, activation=None)
model.add(layers.Dropout(0.3))
model.add(layers.Softmax(axis=1)) # the batch dimension is included as the zero dimension
```
