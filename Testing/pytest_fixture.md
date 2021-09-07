# Pytest Fixture

* Fixture可以用来处理一些多个tests公用的setup
* Fixture可以定义在`test_xxx.py`中, 或者定义在`conftest.py`中, fixture会在调用它的测试函数之前被调用
* 一个测试函数能调用多个fixtures, 自定义的fixture也能调用其他的fixture
```python
@pytest.fixture
def my_fixture():
    return some_obj
```

## Bultin fixtures
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

## Scopes
Pytest fixtures have five different scopes
* function
* class
* module
* package
* session

### Function
* Function is the default scope without explicitly adding `scope="function"`
* The fixture will be executed per test function
* It works for fixtures that
    - used only once
    - contain a very light operation
    - you want a different value each time

```python
import pytest
import json
from datetime import datetime

@pytest.fixture()
def only_used_once():
    with open("app.json") as f:
        config = json.load(f)
    return config

@pytest.fixture()
def light_operation():
    return "I'm a constant"

@pytest.fixture()
def need_different_value_each_time():
    return datetime.now()
```

### Class
* The scope class runs the fixture per test class
* To use a fixture with class score, put `@pytest.mark.usefixtures("fixture-name")` before the test class, and the fixture will be executed _before_ any test function.

### Reference
[Understand 5 Scopes of Pytest Fixtures | by Xiaoxu Gao | Better Programming](https://betterprogramming.pub/understand-5-scopes-of-pytest-fixtures-1b607b5c19ed)
