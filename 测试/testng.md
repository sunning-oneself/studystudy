# TestNG使用

## TestNG文档

- https://testng.org/doc/documentation-main.html

## TestNG安装(基于eclipse+maven)

pom.xml添加

```xml
  	<dependency>
            <groupId>org.testng</groupId>
            <artifactId>testng</artifactId>
            <version>6.8.7</version>
            <scope>test</scope>
	</dependency>
```
记得Maven install一下

## TestNG基本使用与运行

新建一个maven工程，新建一个TestNG的class，可以直接新建一个class来使用，也可以新建一个TestNG的class

## 注解

------|------
注解  |	描述
-----|----
@BeforeSuite|	在该套件的所有测试都运行在注释的方法之前，仅运行一次
-----|----
@AfterSuite|	在该套件的所有测试都运行在注释方法之后，仅运行一次
-----|----
@BeforeClass|	在调用当前类的第一个测试方法之前运行，注释方法仅运行一次
-----|----
@AfterClass |	在调用当前类的第一个测试方法之后运行，注释方法仅运行一次
-----|----
@BeforeTest |	注释的方法将在属于test标签内的类的所有测试方法运行之前运行
-----|----
@AfterTest |	注释的方法将在属于test标签内的类的所有测试方法运行之后运行
-----|----
@BeforeGroups	| 配置方法将在之前运行组列表。 此方法保证在调用属于这些组中的任何一个的第一个测试方法之前不久运行
-----|----
@AfterGroups |	此配置方法将在之后运行组列表。该方法保证在调用属于任何这些组的最后一个测试方法之后不久运行
-----|----
@BeforeMethod |	注释方法将在每个测试方法之前运行
-----|----
@AfterMethod	| 注释方法将在每个测试方法之后运行
-----|----
@DataProvider	| 标记一种方法来提供测试方法的数据。 注释方法必须返回一个Object [] []，其中每个Object []可以被分配给测试方法的参数列表。 要从该DataProvider接收数据的@Test方法需要使用与此注释名称相等的dataProvider名称
-----|----
@Factory |	将一个方法标记为工厂，返回TestNG将被用作测试类的对象。 该方法必须返回Object []
-----|----
@Listeners |	定义测试类上的侦听器
-----|----
@Parameters |	描述如何将参数传递给@Test方法
-----|----
@Test |	将类或方法标记为测试的一部分，此标记若放在类上，则该类所有公共方法都将被作为测试方法

## 预期异常测试

```java
  @Test(expectedExceptions = ArithmeticException.class)
  public void testDivisionWithException() {
	  int i = 1 / 0;
	  System.out.println("异常");
  }
```

## 忽略测试

```java
	@Test(enabled = false)
	public void test3() {
		System.out.println("test3");
	}
```

## 超时测试

```java
	@Test(timeOut = 1)
	public void test4() throws InterruptedException {
		Thread.sleep(10);
		System.out.println("test4");
	}
```

https://blog.csdn.net/df0128/article/details/83243822

## 链接

- [目录](directory.md)
- 上一部分：[httprunner流程](httprunner流程.md)
