 # Pytest

## Frameworks
* pytest
* unittest (built-in)

**Different Between Pytest and Unittest**
* pytest api: `assert`
* unittest api: `assertEqual`, `assertTrue`, `assertIs`...

## Useful Options
* `-s` (print all string output)
* `-v` (print names of individual tests as they run)
* `-x` (stop at first failure)
* `-k` (only run tests matching following keywords)
* `--fixtures` (show all available fixtures)

## Convention
* test all your files start with `test_` in current directory
* test all your function start with `test_` in test files

## Test Exceptions
* `with pytest.raises(SomeError)` 期待抛出异常, 如果不抛出则test失败
* `context.value` can be used for asserting

```python
with pytest.raises(CalculatorError) as context:
    result = calculator.add("two", "three")

assert str(context.value) == 'wrong'
```

## Test Multiple Examples
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

## Put Tests into Class

Just use a class with a name start with `Test` and fill it with some `test_` methods

## Coverage
`pytest --cov` 查看代码中有百分之多少被test了(覆盖率)
`pytest --cov=<package_name>` 只查看给定package中的覆盖率
`pytest --cov-report term-missing --cov=<package_name>` 在终端显示代码中的哪些行没有覆盖

## Numpy.testing

Test equaling of two floats
```python
from numpy.testing import assert_almost_equal, assert_array_almost_equal
assert_almost_equal(actual, desired, decimal=7)
assert_array_almost_equal(actual_arr, desired_arr, decimal=7)
assert np.allclose(actual, desired)
```

## Image Testing

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

## Debugging
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

## Other Features
* use `mark` to run specified tests
