# pytest使用

## pytest介绍

pytest框架可以轻松编写小型测试，然后进行扩展以支持应用程序和库的复杂功能测试。

## 功能

- 有关失败的断言语句的详细信息（无需记住self.assert*名称）
- 自动发现测试模块和函数
- 支持运行由nose, unittest编写的测试case
- 方便的和持续集成工具集成
- 具有很多第三方插件，并且可以自定义扩展

## 如何使用pytest

### pytest测试用例编写规则

- 测试文件以test_开头（以_test结尾也可以）
- 测试类以Test开头，并且不能带有 init 方法
- 测试函数以test_开头
- 断言使用基本的assert即可

### pytest使用方法

1. pytest中使用assert断言

例如：
```python
    assert a == b
```

2. 跳过测试

使用`pytest.mark.skip` 标记跳过测试,使用`pytest.mark.skipif`为测试函数指定被忽略的条件。

3. 参数化

`pytest.mark.parametrize(argnames, argvalues)`可以给测试函数传参

4. Fixture

Fixture是一些函数，pytest 会在执行测试函数之前（或之后）加载运行它们。
Pytest 使用文件 conftest.py 集中管理固件
在复杂的项目中，可以在不同的目录层级定义 conftest.py，其作用域为其所在的目录和子目录。
不要自己显式调用 conftest.py，pytest 会自动调用，可以把 conftest 当做插件来理解。

    1) 预处理和后处理

    Pytest 使用 yield 关键词将固件分为两部分，yield 之前的代码属于预处理，会在测试前执行；yield 之后的代码属于后处理，将在测试完成后执行。

    2)  作用域

    在定义固件时，通过 scope 参数声明作用域，可选项有：

    - function: 函数级，每个测试函数都会执行一次固件；
    - class: 类级别，每个测试类执行一次，所有方法都可以使用；
    - module: 模块级，每个模块执行一次，模块内函数和方法都可使用；
    - session: 会话级，一次测试只执行一次，所有被找到的函数和方法都可用。

    默认的作用域为 function。

    3) 自动执行

    想让固件自动执行，可以在定义时指定 autouse 参数。

    4) 固件的名称默认为定义时的函数名，如果不想使用默认，可以通过 name 选项指定名称

    5) 与函数参数化使用 @pytest.mark.parametrize 不同，固件在定义时使用 params 参数进行参数化。

    固件参数化依赖于内置固件 request 及其属性 param。

    6) 内置Fixfure

    tmpdir & tmpdir_factory
    用于临时文件和目录管理，默认会在测试结束时删除。
    使用 tmpdir.mkdir() 创建目临时录，tmpdir.join() 创建临时文件（或者使用创建的目录）。
    tmpdir_factory 可以在所有作用域使用，包括 function, class, module, session。

    monkeypatch
    monkeypath 用于运行时动态修改类或模块。

    Pytest 内置 monkeypatch 提供的函数有：

    - setattr(target, name, value, raising=True)，设置属性；
    - delattr(target, name, raising=True)，删除属性；
    - setitem(dic, name, value)，字典添加元素；
    - delitem(dic, name, raising=True)，字典删除元素；
    - setenv(name, value, prepend=None)，设置环境变量；
    - delenv(name, raising=True)，删除环境变量；
    - syspath_prepend(path)，添加系统路径；
    - chdir(path)，切换目录。

 
## 链接

- [目录](directory.md)
- 上一部分：[mock](mock.md)
- 下一节: [coverage](coverage.md)
