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
* Fixture可以定义在`test_xxx.py`中, 或者定义在`conftest.py`中, fixture会在调用它的测试函数之前被调用
* 一个测试函数能调用多个fixtures, 自定义的fixture也能调用其他的fixture
* Fixture可以指定scope, 比如对整个test文件都可用
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
assert np.allclose(actual, desired)
```

### Image Testing

利用mpl包来进行针对matplotlib的图片测试, 使用之前先`pip install pytest-mpl`

```python
@pytest.mark.mpl_image_compare(remove_text=True)
def test_plotting_result():
    # some plotting code here and return the figure directly
    return fig

# mpl_image_compare还有个tolerance参数可以设置图片的误差范围
@pytest.mark.mpl_image_compare(remove_text=True, tolerance=0.1)
```

mpl会默认在tests/baseline里找test图片的ground truth. 可以让其先生成, 然后人工比较, 之后即可作为真解测试.
```shell
# 生成图片供肉眼查看
pytest -k test_plotting_result --mpl-generate-path=tests/baseline
# 实际的测试
pytest --mpl
```

### Debugging
```shell
pytest --pdb # invoke PDB on every failure
pytest -x --pdb # drop to PDB on first failure, the end test session
pytest --pdb --maxfail=3 # drop to PDB for first three failures

pytest --trace # invoke PDB at the start of every test
```

To set breakpoints in test code.
```python
import pdb; pdb.set_trace()
# Python3.7 or after
breakpoint()
```

### Other Features
* use `mark` to run specified tests

## Unit Test for Deep Learning

Test all weights have been trained

```python
def test_conv_net():
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
