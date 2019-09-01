# mock使用

## mock介绍

    在python3.3版本开始，mock包成为python标准库unittest.mock的一部分。以前版本中，mock是一个单独的PyPI的安装包
    unittest.mock允许使用模拟对象替换受测试系统的部分，并对如何使用它们进行断言。

## mock常用方法
    
    1)mock里有个patch函数，可以替换指定程序中的值，patch可以用作装饰器，也可以用在with语句中
    2)断言
    assert_called() 断言被调用过几次
    assert_called_once() 断言只被调用过一次
    assert_called_with() 断言是以指定参数进行断言的
    assert_called_with_once() 断言只被调用过一次,断言是以指定参数进行断言的
