# Double-Stringize Trick

It's a trick to turn a macro's content into a string

> ... After the arguments for the invocation of a function-like macro have been identified,
> argument substitution takes place. A parameter in the replacement list, unless preceded by
> a # or ## preprocessing token or followed by a ## preprocessing token (see below), is replaced
> by the corresponding argument after all macros contained therein have been expanded...

Since macro parameter (which is another macro by itself) preceded by a # will not be expanded, we need use two macros to force its expansion

## Example
```c
#define STR1(x) #x
#define STR2(x) STR1(x)
#define THE_ANSWER 42
#define THE_ANSWER_STR STR2(THE_ANSWER) /* "42" */
```

## Reference
[c - How, exactly, does the double-stringize trick work? - Stack Overflow](https://stackoverflow.com/questions/2751870/how-exactly-does-the-double-stringize-trick-work)
