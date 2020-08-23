# Argparse

New in Python 3.2

## How to use
```python
import argparse

parser = argparse.ArgumentParser()
# positional argument
parser.add_argument("arg_name", help="Help docs", type=int) # default type is str
# optional argument
parser.add_argument("-o", "--output", help="Another help docs", action="store_true")
parser.add_argument("-v", "--verbosity", help ="increse output verbosity", type=int, choices=[0, 1, 2])
parser.parse_args()
```

## Different types of argument
* Positional argument (solely based on where it appears on the command line)
* Optional argument
    - `-h` option is already inbuilt by default
    - `action="store_true"` if the option is specified, assign the value `True` to args.output, otherwise `False`
    - `action="count"` will count the appearance number of an option (e.g. -vv), and can use `default=0` to specify the default count
    - `choices=[list of choices]` to restrict the values an option can accept
* The order between the positional and optional arguments does not matter

### Examples
```python
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("x", type=int, help="the base")
parser.add_argument("y", type=int, help="the exponent")
parser.add_argument("-v", "--verbosity", action="count", default=0,
                    help="increase output verbosity")
args = parser.parse_args()
answer = args.x**args.y
if args.verbosity >= 2:
    print("Running '{}'".format(__file__))
if args.verbosity >= 1:
    print("{}^{} == ".format(args.x, args.y), end="")
print(answer)
```

## Conflicting Options
Use `add_mutually_exclusive_group()` to specify options that conflict with each other

```python
import argparse

parser = argparse.ArgumentParser(description="calculate X to the power of Y")
group = parser.add_mutually_exclusive_group()
group.add_argument("-v", "--verbose", action="store_true")
group.add_argument("-q", "--quiet", action="store_true")
parser.add_argument("x", type=int, help="the base")
parser.add_argument("y", type=int, help="the exponent")
args = parser.parse_args()
answer = args.x**args.y

if args.quiet:
    print(answer)
    elif args.verbose:
        print("{} to the power {} equals {}".format(args.x, args.y, answer))
        else:
            print("{}^{} == {}".format(args.x, args.y, answer))
```
