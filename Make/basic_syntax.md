# Basic Syntax

A Makefile consists of a set of rules. A rule generally looks like:
```make
targets: prerequisites
    command1
    command2
    command3
```

* The _targets_ all **file** names, separated by spaces.
* The _commands_ are a series of steps typically used to make the target(s). These need to start with a **tab** character
* The _prerequisites_ are also file names, separated by spaces. These files need to exist before the commands for the target are run.
