# Unit Test

## Why Would I Test?
* Prove that code works like I think it should
* Give examples to others of how code is used
* Get a safety net for future changes

## Frameworks
* pytest
* unittest (built-in)

**Different Between Pytest and Unittest**
* pytest api: `assert`
* unittest api: `assertEqual`, `assertTrue`, `assertIs`...

## Pytest

### Useful Options
* `-s` (print all string output)
* `-v` (print names of individual tests as they run)
* `-x` (stop at first failure)
* `-k` (only run tests matching following keywords)

### Convention
* test all your files start with `test_` in current directory
* test all your function start with `test_` in test files
* three steps to construct test function
    1. Arrange
    2. Act
    3. Assert

### Others
* `with pytest.raises(SomeError)` 期待抛出异常, 如果不抛出则test失败
* `context.value` can be used for asserting

```python
with pytest.raises(CalculatorError) as context:
    result = calculator.add("two", "three")
    
assert str(context.value) == 'wrong'
```

## Unit Test for Deep Learning

Test all weights have been trained

```python
def test_convnet():
  image = tf.placeholder(tf.float32, (None, 100, 100, 3)
  model = Model(image)
  sess = tf.Session()
  sess.run(tf.global_variables_initializer())
  before = sess.run(tf.trainable_variables())
  _ = sess.run(model.train, feed_dict={
               image: np.ones((1, 100, 100, 3)),
               })
  after = sess.run(tf.trainable_variables())
  for b, a, n in zip(before, after):
      # Make sure something changed.
      assert (b != a).any()
```
