# unittest使用

## unittest的工作原理

unittest中最核心的四部分是：TestCase，TestSuite，TestRunner，TestFixture
（1）一个TestCase的实例就是一个测试用例。测试用例就是指一个完整的测试流程，包括测试前准备环境的搭建（setUp），执行测试代码（run），以及测试后环境的还原（tearDown）。元测试（unit test）的本质也就在这里，一个测试用例是一个完整的测试单元，通过运行这个测试单元，可以对某一个问题进行验证。
（2）而多个测试用例集合在一起，就是TestSuite，而且TestSuite也可以嵌套TestSuite。
（3）TestLoader是用来加载TestCase到TestSuite中的。
（4）TextTestRunner是来执行测试用例的，其中的run(test)会执行TestSuite/TestCase中的run(result)方法
（5）测试的结果会保存到TextTestResult实例中，包括运行了多少测试用例，成功了多少，失败了多少等信息。
 综上，整个流程就是首先要写好TestCase，然后由TestLoader加载TestCase到TestSuite，然后由TextTestRunner来运行TestSuite，运行的结果保存在TextTestResult中，整个过程集成在unittest.main模块中。

## unittest编写测试用例规则

- 一个testcase必须是unittest.TestCase子类
- 测试方法应以test 开头

```python
import unittest

class TestStringMethods(unittest.TestCase):

    def test_upper(self):
        self.assertEqual('foo'.upper(), 'FOO')
```

## 运行单元测试

1) 在文件最后加入
```python
if __name__ == '__main__':
    unittest.main()
```

2) python -m unittest 文件名

## unittest的用法

1) TestCase
- 常用的断言

```python
    assertEqual(a, b)     a == b
    assertNotEqual(a, b)     a != b
    assertTrue(x)     bool(x) is True
    assertFalse(x)     bool(x) is False      
    assertIsNone(x)     x is None
    assertIsNotNone(x)     x is not None   
    assertIn(a, b)     a in b    
    assertNotIn(a, b)     a not in b
```

- 跳过测试用例

    - 使用 skipXxx 装饰器来跳过测试用例。unittest 一共提供了 3 个装饰器，分别是 ＠unittest.skip(reason)、@unittest.skipIf(condition, reason) 和 ＠unittest.skipUnless(condition, reason)。其中 skip 代表无条件跳过，skipIf 代表当 condition 为 True 时跳过；skipUnless 代表当 condition 为 False 时跳过。
    - 使用TestCase 的 skipTest() 方法来跳过测试用例。

3) TestFixture

    - setUp()&tearDown()：在每个测试方法（用例）运行时被调用一次
    - setUpClass()&tearDownClass(): 每个类只调用一次。必须使用@classmethod 装饰器
    - setUpModule()&tearDownModule(): 整个文件级别上只调用一次 setUp/tearDown

4) TestSuite

    unittest.main()是将模块下的测试用例全部执行，而且是按ascii码顺序执行测试用例,使用TestSuit可以自定义测试组件
    可以使用TestLoader来加载TestCase到TestSuite中。
    - unittest.TestLoader().loadTestsFromTestCase(testCaseClass)
    - unittest.TestLoader().loadTestsFromModule(module)
    - unittest.TestLoader().loadTestsFromName(name,module=None)
    - unittest.TestLoader().loadTestsFromNames(names,module=None)
    - unittest.TestLoader().discover(start_dir，pattern ='test * .py'，top_level_dir = None)

5) TestRunner
    
    TextTestRunner.run(suit)开始执行测试用例,TextTestResult用来保存测试用例结果
