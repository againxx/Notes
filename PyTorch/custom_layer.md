# Custom Layer
By subclassing the `nn.Module` class, you can create your own building blocks

## Functionality that nn.Module Provides
* It tracks all submodules that current module includes (assigned to current modulde's properties)
* It provides functions to deal with all parameters of the registered submodules
    - `children()` returns an iterator over immediate children modules
    - `parameters()` obtains the full list of modulde's parameters
    - `zero_grad()` zeros their gradients
    - `to(device)` move to CPU or GPU
    - `state_dict()` and `load_state_dict()` serialize and deserialize the module
    - `apply()` perform generic transformation to every submodule using your own callable
* Every module needs to perform its data transformation in the `forward()` method by overriding it
* Register a hook function to tweak module transformation or gradients flow

## Example
```python
class OurModule(nn.Module):
    def __init__(self, num_inputs, num_classes, dropout_prob=0.3):
        super(OurModule, self).__init__()
        # By assigning a Sequential (inheriting from nn.Module) instance to our field
        # We automatically register this module
        self.pipe = nn.Sequential(
            nn.Linear(num_inputs, 5),
            nn.ReLU(),
            nn.Linear(5, 20),
            nn.ReLU(),
            nn.Linear(20, num_classes),
            nn.Dropout(p=dropout_prob),
            nn.Softmax(dim=1)
        )
    
    def forward(self, x):
        return self.pipe(x)

if __name__ == "__main__":
    net = OurModule(num_inputs=2, num_classes=3)
    v = torch.FloatTensor([[2, 3]])
    out = net(v)
    print(net)
    print(out)
```
