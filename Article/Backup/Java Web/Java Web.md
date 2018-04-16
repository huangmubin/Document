# 1.0 Java 语言基础
## 1.1 Java 开发周边
### 1.1.1 集成环境 Eclipse

### 1.2.1 JUnit 测试框架

> 使用 JUnit 添加测试案例流程

* 右键 项目文件 
    * 选择 属性(Properties)
    * 选择 Java Build Path
    * 选择 Libraries
    * 点击 Add Library ...
    * 选择 JUnit4 并 确定
* 右键 需要添加测试单元的 Java 文件
    * 选择 New - JUnit Test Case
    * 选择对应选项
    * 确定 生成 Test Case 类
* 右键 Test Case 类
    * Run As - JUnit Test

> 知识点

* Test Case 类中的 Test 方法必须要 
    * 添加 `@Test` 前缀
    * 必须是 `public` 方法
* Run As - JUnit Test 运行测试方法 
    * 右键特定方法则运行特定方法的测试
    * 右键 Test Case 类则运行所有 `@Test` 方法。
* 运行时机
    * `@BeforeClass` 方法会在整个测试之前运行，必须静态方法
    * `@Before` 方法会在每个 `@Test` 测试开始之前运行
    * `@After` 方法会在每个 `@Test` 测试之后运行
    * `@AfterClass` 方法会在整个测试之后运行，必须静态方法
* Assert 断言方法，如果正确则通过，否则不通过


> 示例

```
package junit_demo;

import org.junit.After;
import org.junit.AfterClass;
import org.junit.Before;
import org.junit.BeforeClass;
import org.junit.Test;

public class JunitDemoTest {

	
	JunitDemoRun junit;
	
	@BeforeClass
	public static void setUpBeforeClass() throws Exception {
		System.out.println("setUpBeforeClass");
	}

	@Before
	public void setUp() throws Exception {
		System.out.println("setUp");
		junit = new JunitDemoRun();
	}

	@Test
	public void test() {
		junit.run();
	}

	@Test
	public void test2() {
		junit.run2();
		Assert.assertTrue(false); // 不通过
	}
	
	@After
	public void tearDown() throws Exception {
		junit = null;
		System.out.println("tearDown");
	}

	@AfterClass
	public static void tearDownAfterClass() throws Exception {
		System.out.println("tearDownAfterClass");
	}

}
```


