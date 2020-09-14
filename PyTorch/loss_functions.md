# Loss Functions

* Loss functions are resided in the `nn` package and are implemented as an `nn.Module` subclass
* Usually accept two arguments the prediction and label

## Common Loss Functions
* `nn.MSELoss` mean square error loss, which is standard loss for regression problems
* `nn.BCELoss` and `nn.BCEWithLogitsLoss`, the first one expects probability values, and the second one assumes raw scores
  and applies `Sigmoid` itself. The second way is usually more numerically stable and efficient
* `nn.CrossEntropyLoss` and `nn.NLLLoss`, the first one expects raw scores and applies `LogSoftmax` internally, the
  second one expects to have log probabilities as input (NLL stands for negative log likelihood)
