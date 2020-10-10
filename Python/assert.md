# Assert

`assert <expression> ["," expression]`

## Simple Form
`assert expression` is equivalent to
```python
if __debug__:
    if not expression: raise AssertionError
```

## Extended Form
`assert expression1, expression2`
```python
if __debug__:
    if not expression1: raise AssertionError(expression2)
```

* In current implementation, the builtin variable `__debug__` is `True` under normal circumstance, `False` when optimization is requested (command line option `-O`)

## When to Use Assert
* Parameters scrutiny
