# Command Pattern

> Encapsulate a request as a object, thereby letting you parameterize clients with different
> requests, queue or log requests, and support undoable operations

> Commands are an object-oriented replacement for callbacks

![UML for command pattern](https://gitee.com/againxx/image-storage/raw/master/images/20210611090431.png =750x)

## Goal
* Decouple an object that invokes an operation (the Invoker) for the provider object that implements it (the Receiver)

## Advantages
1. It's easy to design a command queue (in the Invoker)
2. Can log the commands when necessary
3. the Receiver can deny the request when it can be fulfilled
4. Support redo and undo actions (in the Invoker)
5. Easy to add new concrete commands

## Python Function Implementation
* Use first-class functions or other callables to replace single method classes with less boilerplate code

```python
# Simple command can be implemented using a normal function
# For MacroCommand, we can use a callable object

class MacroCommand:
    """A command that executes a list of commands"""

    def __init__(self, commands):
        self.commands = list(commands)

    def __call__(self):
        for command in self.commands:
            command()
```
