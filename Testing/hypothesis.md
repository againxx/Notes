# Hypothesis

* Hypothesis is a property-based testing framework, which lets you write tests like this:
    1. For all data matching some specification
    2. Perform some operations on the data
    3. Assert something about the results 
* It's powerful in finding edge cases which you wouldn't have thought to look for

## Key decorators
### given
* Take test function and turn it into a parametrized one
* When called, this test function will be run over a wide range of matching data from a strategy

### example
* Make sure this example (particular edge case) will be tested every time 
* It's can show what kinds of data are valid inputs

## Search Strategies
A way to generate testing data that meets the specification
* `text()`
* `integers()`
* `booleans()`
* `lists()`

## Interesting Mechanisms
* Remember failing examples
* Simplify failing examples it finds to produce simple and easy-understanding ones
