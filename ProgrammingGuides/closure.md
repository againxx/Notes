# Closure

## What's a closure
* A closure is a record (function) storing a nested function together with an environment
    - Environment: the *nonglobal* *free* variables that exist when the function is defined
    - Global variables are easy to access, so we don't need to capture them
* A closure unlike a plain function, allows the function to access those captured variables through
  the closure's reference to them, even when the function is invoked outside their scope
* A closure can close over free variables (variables that are not defined in the function itself) from outer environment
* A closure **is not equal** to anonymous function, albeit they always come together

![Closure Demonstration](https://gitee.com/againxx/image-storage/raw/master/images/20210611195814.png =750x)

## Examples
### Python
```python
def make_averager():
    series = []

    def average(new_value):
        series.append(new_value)
        total = sum(series)
        return total / len(series)

    return average


print(avg.__code__.co_varnames)
# ('new_value', 'total')
print(avg.__code__.co_freevars)
# ('series',)
print(avg.__closure__[0].cell_contents)
# [10, 11, 12]
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

### C++
```cpp
auto make_averager() {
    std::vector<double> series;
    // Note we need to capture by value and mutable lambda to
    // enable mutate the series inside the lambda
    auto average = [=](double new_value) mutable {
        series.emplace_back(new_value);
        double total = std::accumulate(series.cbegin(), series.cend(), 0.0);
        return total / series.size();
    };
    return average;
}

```

## Reference
* Fluent Python 7.5 Closures
