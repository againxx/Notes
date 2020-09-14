# Optimizers

* Popular optimizer implementations are provided in `torch.optim` package
* All optimizers expose unified interface.
    - On construction, you need to pass an iterable of tensors, which will be modified during optimization process
    - Usual practice is to pass the result of the `parameters()` call of the upper-level `nn.Module` instance 

## Common Optimizers
* `SGD`: vanilla stochastic gradient descend algorithm with optional momentum extension
* `RMSProp`
* `Adagrad`
* `Adam`: a quite successful and popular combination of both `RMSProp` and `Adagrad`

## Common Blueprint of a Training Loop
```python
for batch_x, batch_y in iterate_batches(data, batch_size=32):
    batch_x_t = torch.tensor(batch_x)
    batch_y_t = torch.tensor(batch_y)
    out_t = net(batch_x_t)
    loss_t = loss_function(out_t, batch_y_t) # a tensor of one single loss value
    loss_t.backward()
    optimizer.step()
    optimizer.zero_grad()
```

### Logic behind
* Every tensor in the computation graph remembers its parent
* The call of `backward()` will unroll the graph of the performed computations and calculate gradients for every leaf tensor with `require_grad=True`
* Usually such tensors are model's parameters such as the weights, biases and convolution filters
* Every time a gradient is calculated, it's accumulated in the `tensor.grad` field, so one tensor can participate in a transformation muliple times
  and its gradients will be properly summed together (e.g. one single RNN cell could be applied to muliple input items)
* The last, but not least, piece of training loop is to zero gradients of parameters by calling `zero_grad()` on network or optimizer
