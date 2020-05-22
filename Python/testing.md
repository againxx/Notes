 # Unit Test

## Why Would I Test?
* Prove that code works like I think it should
* Give examples to others of how code is used
* Get a safety net for future changes

## Four Phases of Testing
1. Setup (Arrange)
2. Exercise (Act)
3. Verify (Assert)
4. Cleanup

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
* `--fixtures` (show all available fixtures)

### Convention
* test all your files start with `test_` in current directory
* test all your function start with `test_` in test files

### Test Exceptions
* `with pytest.raises(SomeError)` 期待抛出异常, 如果不抛出则test失败
* `context.value` can be used for asserting

```python
with pytest.raises(CalculatorError) as context:
    result = calculator.add("two", "three")

assert str(context.value) == 'wrong'
```
### Test Multiple Examples
One failure test won't abort the other one.

```python
@pytest.mark.parametrize(
    "a, b, expected",
    [
        (1, 1, 2),
        (2, 1, 3),
        (3, 2, 5),
    ],
)
def test_with_param(a, b, expected):
    assert demo.add(a, b) == expected
```

### Put Tests into Class

Just use a class with a name start with `Test` and fill it with some `test_` methods

### Fixture

* Fixture可以用来处理一些多个tests公用的setup
* Fixture需要定义在`conftest.py`中, fixture会在调用它的测试函数之前被调用
* 一个测试函数能调用多个fixtures, 自定义的fixture也能调用其他的fixture
```python
@pytest.fixture
def my_fixture():
    return some_obj
```

#### Bultin fixtures
* `capsys`
捕获系统的输出, stdout/stderr
```python
def test_capsys(capsys):
    print("hello")
    out, err = capsys.readouterr()
    assert out == "hello\n"
```

* `monkeypatch`
用一个虚假的函数去代替一个真实的函数, 从而避免在test时避免一些高计算或者高延迟的操作
```python
def test_monkeypatch(monkeypatch):
    def fake_add(a, b):
        return 42
    monkeypatch.setattr(demo, "add", fake_add)
    assert demo.add(2, 3) == 42
```

另一种类似的方法是利用`unittest.mock.patch`装饰器
```python
from unittest.mock import patch

def mocked_current_utc_time():
    return datetime.datetime(2018, 3, 26, 12)
    
@patch('demo.current_utc_time', new=mocked_current_utc_time)
def test_that_mock_works():
    result = demo.current_utc_time()
    truth = datetime.datetime(2018, 3, 26, 12)
    assert result == truth
```

* `tmpdir`
创建一个临时文件夹, 语法类似os.path
```python
def test_tmpdir(tmpdir):
    some_file = tmpdir.join("something.txt")
    some_file.write('{"hello": "world"}')

    result = demo.read_json(str(some_file))
    assert result["hello"] == "world"
```

* `tmp_path`
创建一个临时文件夹, 语法类似pathlib

### Coverage
`pytest --cov` 查看代码中有百分之多少被test了(覆盖率)
`pytest --cov=<package_name>` 只查看给定package中的覆盖率
`pytest --cov-report term-missing --cov=<package_name>` 在终端显示代码中的哪些行没有覆盖

### Numpy.testing

Test equaling of two floats
```python
from numpy.testing import assert_almost_equal, assert_array_almost_equal
assert_almost_equal(actual, desired, decimal=7)
assert_array_almost_equal(actual_arr, desired_arr, decimal=7)
```

### Image Testing

### Other Features
* use `mark` to run specified tests

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
