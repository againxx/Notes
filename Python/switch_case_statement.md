# The Pythonic Way to Implement Switch-case Statement

## Workflow of switch-case statement in other language
1. Compiler generates a jump table for switch case statement
2. The switch variable/expression is evaluated once
3. Switch statement looks up the evaluated variable/expression in the jump table and directly decides which code block to execute
4. If no match is found, then the code under default case is executed

> Because of the jump table, a switch statement is much faster than an if-else-if ladder.
> Instead of evaluating each condition sequentially, it only has to look up the evaluated variable/expression once
> and directly jump to the appropriate branch of code to execute it.

## Implement switch-case statement in Python
The Pythonic way to implement switch statement is to use the powerful dictionary mappings,
you can even use function names or lambda as dict value and use dict.get method to implement
default case.

```python
def one():
    return "January"

def two():
    return "February"

def three():
    return "March"

def four():
    return "April"

def numbers_to_months(argument):
switcher = {
    1: one,
    2: two,
    3: three,
    4: four
}
# Get the function from switcher dictionary
func = switcher.get(argument, lambda: "Invalid month")
# Execute the function
print func()
```

In fact, if you’re calling methods on objects, you can even use a dispatch method to dynamically determine
which function needs to be called during runtime.
```python
class Switcher(object):
def numbers_to_months(self, argument):
    """Dispatch method"""
    method_name = 'month_' + str(argument)
    # Get the method from 'self'. Default to a lambda.
    method = getattr(self, method_name, lambda: "Invalid month")
    # Call the method as we return it
    return method()

def month_1(self):
    return "January"

def month_2(self):
    return "February"

def month_3(self):
    return "March"
```

## Advantage of Python's Approach
Since you can alter Python dictionaries during runtime (add, remove or update key-value pairs),
you can easily change your very switch statement on the fly.

## Reference
[How to implement a switch-case statement in Python](https://jaxenter.com/implement-switch-case-statement-python-138315.html)
