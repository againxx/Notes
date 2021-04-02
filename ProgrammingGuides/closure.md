# Closure

## What's closure
* A closure is a record storing a function together with an environment
* A closure unlike a plain function, allows the function to access those captured variables through
  the closure's reference to them, even when the function is invoked outside their scope
* A closure can close over free variables (variables that are not defined in the function itself) from outer environment

## Examples
### Python
```python
def outer_func(msg):
    message = msg

    def inter_func():
        print(message)

    return inter_func

hi_func = outer_func("Hi")
hello_func = outer_func("Hello")

# The free variable message is captured by the inter_func
hi_func() # "Hi"
hello_func() # "Hello"
```

### Javascript
```javascript
function html_tag(tag) {
    function wrap_text(msg) {
        console.log('<' + tag + '>' + msg + '</' + tag + '>');
    }
    return wrap_text;
}

print_h1 = html_tag('h1');
print_p = html_tag('p');
print_h1('Test Headline!');
print_p('Test paragraph!');
```
