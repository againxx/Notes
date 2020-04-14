# Underscore
There are 5 use cases of underscore (`_`)
1. For storing the value of last expression in interpreter.
2. For ignoring the specific values. (so-called “I don’t care”)
3. To give special meanings to name of variables or functions.
4. To use as ‘Internationalization(i18n)’ or ‘Localization(l10n)’ functions. (Not meet yet)
5. To separate the digits of number literal value.

## Value of the last expression
When used in interactive interpreter, the interpreter uses the speical variable called `_` to store the value of last expression

## For ignoring values
If some values are not used, just assign the values to `_`
```python
# Ignore multiple values, It's called "Extend Unpacking" which is only available in python 3.x
x, *_, y = (1, 2, 3, 4, 5) # x = 1, y = 5

# Underscore can also be used in function parameters
def refresh(_):
    cwd = self.fm.get_directory(original_path)
    cwd.load_content()
```

## Give special meanings to variables and functions

### _single_leading_underscore
This is used for declaring **private** variables/functions/methods/classes in a module. 
Anything with this convention are ignored in `from module import *`. 

### single_trailing_underscore_
This convention could be used for avoiding conflict with Python keywords or built-ins. You might not use it often. (not real private)
```python
list_ = List.objects.get(1) # Avoid conflict with 'list' built-in type
```
### __double_leading_underscore
Double underscore will mangle the attribute names of a class to avoid conflicts of attribute names between classes. 
(so-called “mangling” that means that the compiler or interpreter modify the variables or function names with some rules, not use as it is) 

The mangling rule of Python is adding the `_ClassName` to front of attribute names are declared with double underscore. 
That is, if you write method named `__method` in a class, the name will be mangled in `_ClassName__method` form.

Sometimes, some people use it as like real private ones using these features, but it is not for private and not recommended for that.

### __double_leading_and_trailing_underscore__
"Magic method" such as `__init__`, `__len__`, seems like some operator overload in C++

## Seperate the digits of number
This feature was added in Python 3.6. It is used for separating digits of numbers using underscore for readability.
```python
dec_base = 1_000_000
bin_base = 0b_1111_0000
hex_base = 0x_1234_abcd

print(dec_base) # 1000000
print(bin_base) # 240
print(hex_base) # 305441741
```
