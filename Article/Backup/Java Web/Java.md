
> http://www.runoob.com/java/java-tutorial.html

# 1.0 开发环境

## 1.1 环境配置

## 1.2 Eclipse

### 1.2.1 MyEclipse

## 1.3 JUnit 测试框架

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

# 2.0 基础语法

## 2.1 语法概述

> 基本语法

* 大小写敏感
* 类名：首字母必须大写
* 方法名：首字母必须小写
* 源文件名：必须以 .java 作为后缀，并且与类名称一致。
* 主方法入口：`public static void main(String []args)`

> 标识符

* a-z，$, _ 都是合法的标识符
* 数字可以在首字母之外的位置

> 修饰符

* 访问控制修饰符：default, public, protected, private
* 非访问控制修饰符：final, abstract, strictfp

> 变量

* 局部变量
* 类变量（静态变量）
* 成语变量（非静态变量）

> 枚举

```
class EnumDemo {
    enum EnumCase{ONE, TWO, THREE}
    EnumCase unit
}

public class Demo {
    public static void main(String []args) {
        EnumDemo unit = new EnumDemo();
        unit.unit = EnumDemo.EnumCase.ONE;
    }
}
```

> 关键字

...

> 注释

```
// 单行
/* 单行 */
/*
 * 多行
 */
```

## 2.2 基本数据类型

* byte: 8位
* short: 16位
* int: 32位
* long: 100L
* float: 32位，10.0f
* double: 64位
* boolean: 1位
* char: 16位， Unicode

> 包装类都有方法 SIZE， MIN_VALUE，MAX_VALUE
> 隐藏类型转换会从低位自动提升到高位
> 强制类型转换： (int)

## 2.3 变量类型

`type identifier [ = value][, identifier [ = value] ...];`

## 2.4 修饰符

> 访问修饰符

* default (即缺省，什么也不写）: 在同一包内可见，不使用任何修饰符。使用对象：类、接口、变量、方法。
* private : 在同一类内可见。使用对象：变量、方法。 注意：不能修饰类（外部类）
* public : 对所有类可见。使用对象：类、接口、变量、方法
* protected : 对同一包内的类和所有子类可见。使用对象：变量、方法。 注意：不能修饰类（外部类）。

> static

* 静态变量
* 静态方法

> final 

* 变量：只能被初始化一次，然后不可改动数据或引用。
* 方法：可以被继承但是无法被修改。
* 类：无法被继承。

> abstract 抽象类标识符，无法被实例化，必须被继承，扩展后才可用。

```
abstract class AbstractDemo {
   private String value;
   public abstract void run(); // 抽象方法
}

class SubDemo extends AbstractDemo {
    public void run() {
        ... 实现抽象方法
    }
}
```

> synchronized 只能被一个线程访问，可以同时加四个访问修饰符

```
public synchronized void singleMethod() {
    ...
}
```

> volatile 强制多线程每次访问都进行数据更新，可以是 Null.

volatile 修饰的成员变量在每次被线程访问时，都强制从共享内存中重新读取该成员变量的值。而且，当成员变量发生变化时，会强制线程将变化值回写到共享内存。这样在任何时刻，两个不同的线程总是看到某个成员变量的同一个值。

> transient 序列化时忽略该修饰符修饰的变量。

## 2.5 运算符

* 算术运算符
* 关系运算符
* 位运算符
* 逻辑运算符
* 赋值运算符
* 其他运算符
    * instanceof 运算符：

```
位运算符

A = 0011 1100
B = 0000 1101
-----------------
A&b = 0000 1100
A | B = 0011 1101
A ^ B = 0011 0001
~A= 1100 0011


操作符	描述	例子
＆	如果相对应位都是1，则结果为1，否则为0	（A＆B），得到12，即0000 1100
|	如果相对应位都是0，则结果为0，否则为1	（A | B）得到61，即 0011 1101
^	如果相对应位值相同，则结果为0，否则为1	（A ^ B）得到49，即 0011 0001
〜	按位补运算符翻转操作数的每一位，即0变成1，1变成0。	（〜A）得到-61，即1100 0011
<< 	按位左移运算符。左操作数按位左移右操作数指定的位数。	A << 2得到240，即 1111 0000
>> 	按位右移运算符。左操作数按位右移右操作数指定的位数。	A >> 2得到15即 1111
>>> 	按位右移补零操作符。左操作数的值按右操作数指定的位数右移，移动得到的空位以零填充。	A>>>2得到15即0000 1111
```

```
instanceof
该运算符用于操作对象实例，检查该对象是否是一个特定类型（类类型或接口类型）。
instanceof运算符使用格式如下：
( Object reference variable ) instanceof  (class/interface type)
```

## 2.6 循环结构

### 2.6.1 while

```
while(/* 布尔表达式 */) {
    // 循环内容
}

do {
    // 循环内容
}while(/* 布尔表达式 */)
```

### 2.6.2 for

```
for(/* 初始化 */; /* 布尔表达式 */; /* 更新 */) {
    // 循环内容
}

for(/* 声明语句 */ : /* 数组 */) {
    // 循环内容
}
```

### 2.6.3 break continue 

## 2.7 分支结构

### 2.7.1 if else

```
if(/* 布尔表达式 */) {
    // ...
}
else if(/* 布尔表达式 */) {
    // ...
}
else {
    // ...
}
```

### switch

```
switch(/* byte, short, int, char, String */) {
    case /**/ :
        // ...
        break;
    case /**/ :
        // ...
        break;
    default:
        // ...
}
```

# 3.0 常用类

## 3.1 Number

> 所有包装类都是抽象类 Number 的子类

* Integer
* Long
* Byte
* Double
* Float
* Short

> 常用方法

* Number

// 类型转换
public abstract int intValue();
public abstract long longValue();
public abstract float floatValue();
public abstract double doubleValue();
public byte byteValue();
public short shortValue();

* Integer

// 字符串输出
public static String toString(int i, int radix);
public static String toUnsignedString(int i, int radix);
public static String toHexString(int i);
public static String toOctalString(int i)
.....



## 3.2 Math

Java 的 Math 包含了用于执行基本数学运算的属性和方法，如初等指数、对数、平方根和三角函数。

> 常用方法

// 指数、对数、平方根和三角函数

## 3.3 Character

> 常用方法

// 字符检查，大小写转换方法

## 3.4 String

> 常用方法

// 字符串对比方法
// 字符串拼接方法
// 字符串检索方法

## 3.5 StringBuffer

当对字符串进行修改的时候，需要使用 StringBuffer 和 StringBuilder 类。
和 String 类不同的是，StringBuffer 和 StringBuilder 类的对象能够被多次的修改，并且不产生新的未使用对象。

> 常用方法

// 字符串修改方法

# 4.0 数组

> 数组声明

```
int[] values;
int values[];
```

> 创建数组

```
//
int[] values;
values = new int[10]; // 创建长度为 10 的 int 数组

//
int[] values = new int[10]; 

// 
int[] values = {0,1,2,3,4,5,6,7,8,9,};
```

> 多维数组

```
int[][] = new int[2][3];
```

## 4.1 Array 类

* 赋值：fill 方法
* 排序：sort 方法
* 比较：equals 方法
* 查找：binarySearch 方法

# 5.0 日期时间 

## 5.1 Date

> 获取当前时间

```
Date date = new Date();
System.out.println(date.toString());
// Mon May 04 09:51:52 CDT 2013
```

> 日期比较

* getTime() // 获取时间戳
* 对比
    * before()
    * after()
    * equals()
* compareTo()

> 格式化日期

```
Date date = new Date( );
SimpleDateFormat format = new SimpleDateFormat ("E yyyy.MM.dd 'at' hh:mm:ss a zzz");
System.out.println("Current Date: " + format.format(date));
// Current Date: Sun 2014.07.18 at 14:14:09 PM PDT
```

> 解析字符串为时间

```
public static void main(String args[]) {
    SimpleDateFormat ft = new SimpleDateFormat ("yyyy-MM-dd"); 

    String input = args.length == 0 ? "1818-11-11" : args[0]; 

    System.out.print(input + " Parses as "); 

    Date t; 

    try { 
        t = ft.parse(input); 
        System.out.println(t); 
    } catch (ParseException e) { 
        System.out.println("Unparseable using " + ft); 
    }
}

// $ java DateDemo
// 1818-11-11 Parses as Wed Nov 11 00:00:00 GMT 1818
// $ java DateDemo 2007-12-01
// 2007-12-01 Parses as Sat Dec 01 00:00:00 GMT 2007
```

## 5.2 sleep 休眠

> 堵塞当前线程

```
try { 
    System.out.println(new Date( ) + "\n"); 
    Thread.sleep(1000*3);   // 休眠3秒
    System.out.println(new Date( ) + "\n"); 
} catch (Exception e) { 
    System.out.println("Got an exception!"); 
}
```

## 5.3 Calendar 日历

> 获取系统当前日期

```
Calendar c = Calendar.getInstance();//默认是当前日期
```

> 设置 Calendar 日期

```
//创建一个代表2009年6月12日的Calendar对象
Calendar c1 = Calendar.getInstance();
c1.set(2009, 6 - 1, 12);

// public final void set(int year,int month,int date)
// public void set(int field,int value)
```

> 移动 Calendar 日期 

```
c1.add(Calendar.DATE, 10); // +10 天
```

> 获取 Calendar 日期

```
Calendar c1 = Calendar.getInstance();
// 获得年份
int year = c1.get(Calendar.YEAR);
// 获得月份
int month = c1.get(Calendar.MONTH) + 1;
// 获得日期
int date = c1.get(Calendar.DATE);
// 获得小时
int hour = c1.get(Calendar.HOUR_OF_DAY);
// 获得分钟
int minute = c1.get(Calendar.MINUTE);
// 获得秒
int second = c1.get(Calendar.SECOND);
// 获得星期几（注意（这个与Date类是不同的）：1代表星期日、2代表星期1、3代表星期二，以此类推）
int day = c1.get(Calendar.DAY_OF_WEEK);
```

## 5.4 GregorianCalendar 公历日历

Calendar类实现了公历日历，GregorianCalendar是Calendar类的一个具体实现。

# 6.0 正则表达式

## 6.1 主要类

> java.util.regex 包主要包括以下三个类：

* Pattern 类：

pattern 对象是一个正则表达式的编译表示。Pattern 类没有公共构造方法。要创建一个 Pattern 对象，你必须首先调用其公共静态编译方法，它返回一个 Pattern 对象。该方法接受一个正则表达式作为它的第一个参数。

* Matcher 类：

Matcher 对象是对输入字符串进行解释和匹配操作的引擎。与Pattern 类一样，Matcher 也没有公共构造方法。你需要调用 Pattern 对象的 matcher 方法来获得一个 Matcher 对象。

* PatternSyntaxException：

PatternSyntaxException 是一个非强制异常类，它表示一个正则表达式模式中的语法错误。

```
import java.util.regex.*;
 
class RegexExample1{
   public static void main(String args[]){
      String content = "I am noob " +
        "from runoob.com.";
 
      String pattern = ".*runoob.*";
 
      boolean isMatch = Pattern.matches(pattern, content);
      System.out.println("字符串中是否包含了 'runoob' 子字符串? " + isMatch);
   }
}
// 字符串中是否包含了 'runoob' 子字符串? true
```

## 6.2 捕获组

> 将数据以表达式来进行分组
> group(0) 必然是元数据

```
import java.util.regex.Matcher;
import java.util.regex.Pattern;
 
public class RegexMatches
{
    public static void main( String args[] ){
 
      // 按指定模式在字符串查找
      String line = "This order was placed for QT3000! OK?";
      String pattern = "(\\D*)(\\d+)(.*)";
 
      // 创建 Pattern 对象
      Pattern r = Pattern.compile(pattern);
 
      // 现在创建 matcher 对象
      Matcher m = r.matcher(line);
      if (m.find( )) {
         System.out.println("Found value: " + m.group(0) );
         System.out.println("Found value: " + m.group(1) );
         System.out.println("Found value: " + m.group(2) );
         System.out.println("Found value: " + m.group(3) ); 
      } else {
         System.out.println("NO MATCH");
      }
   }
}
// Found value: This order was placed for QT3000! OK?
// Found value: This order was placed for QT
// Found value: 3000
// Found value: ! OK?
```

## 6.3 表达式语法

| 字符 | 说明 |
|:-- |:-- |
|\\|将下一字符标记为特殊字符、文本、反向引用或八进制转义符。例如，"n"匹配字符"n"。"\n"匹配换行符。序列"\\\\"匹配"\"，"\\("匹配"("。|
|^|匹配输入字符串开始的位置。如果设置了 RegExp 对象的 Multiline 属性，^ 还会与"\n"或"\r"之后的位置匹配。|
|$|匹配输入字符串结尾的位置。如果设置了 RegExp 对象的 Multiline 属性，$ 还会与"\n"或"\r"之前的位置匹配。|
|*|零次或多次匹配前面的字符或子表达式。例如，zo* 匹配"z"和"zoo"。* 等效于 {0,}。|
|+|一次或多次匹配前面的字符或子表达式。例如，"zo+"与"zo"和"zoo"匹配，但与"z"不匹配。+ 等效于 {1,}。|
|?|零次或一次匹配前面的字符或子表达式。例如，"do(es)?"匹配"do"或"does"中的"do"。? 等效于 {0,1}。|
|{n}|n 是非负整数。正好匹配 n 次。例如，"o{2}"与"Bob"中的"o"不匹配，但与"food"中的两个"o"匹配。|
|{n,}|n 是非负整数。至少匹配 n 次。例如，"o{2,}"不匹配"Bob"中的"o"，而匹配"foooood"中的所有 o。"o{1,}"等效于"o+"。"o{0,}"等效于"o*"。|
|{n,m}|M 和 n 是非负整数，其中 n <= m。匹配至少 n 次，至多 m 次。例如，"o{1,3}"匹配"fooooood"中的头三个 o。'o{0,1}' 等效于 'o?'。注意：您不能将空格插入逗号和数字之间。|
|?|当此字符紧随任何其他限定符（*、+、?、{n}、{n,}、{n,m}）之后时，匹配模式是"非贪心的"。"非贪心的"模式匹配搜索到的、尽可能短的字符串，而默认的"贪心的"模式匹配搜索到的、尽可能长的字符串。例如，在字符串"oooo"中，"o+?"只匹配单个"o"，而"o+"匹配所有"o"。|
|.|匹配除"\r\n"之外的任何单个字符。若要匹配包括"\r\n"在内的任意字符，请使用诸如"[\s\S]"之类的模式。|
|(pattern)|匹配 pattern 并捕获该匹配的子表达式。可以使用 $0…$9 属性从结果"匹配"集合中检索捕获的匹配。若要匹配括号字符 ( )，请使用"\("或者"\)"。|
|(?:pattern)|匹配 pattern 但不捕获该匹配的子表达式，即它是一个非捕获匹配，不存储供以后使用的匹配。这对于用"or"字符 (|) 组合模式部件的情况很有用。例如，'industr(?:y|ies) 是比 'industry|industries' 更经济的表达式。|
|(?=pattern)|执行正向预测先行搜索的子表达式，该表达式匹配处于匹配 pattern 的字符串的起始点的字符串。它是一个非捕获匹配，即不能捕获供以后使用的匹配。例如，'Windows (?=95|98|NT|2000)' 匹配"Windows 2000"中的"Windows"，但不匹配"Windows 3.1"中的"Windows"。预测先行不占用字符，即发生匹配后，下一匹配的搜索紧随上一匹配之后，而不是在组成预测先行的字符后。|
|(?!pattern)|执行反向预测先行搜索的子表达式，该表达式匹配不处于匹配 pattern 的字符串的起始点的搜索字符串。它是一个非捕获匹配，即不能捕获供以后使用的匹配。例如，'Windows (?!95|98|NT|2000)' 匹配"Windows 3.1"中的 "Windows"，但不匹配"Windows 2000"中的"Windows"。预测先行不占用字符，即发生匹配后，下一匹配的搜索紧随上一匹配之后，而不是在组成预测先行的字符后。|
|x\|y|匹配 x 或 y。例如，'z|food' 匹配"z"或"food"。'(z|f)ood' 匹配"zood"或"food"。|
|[xyz]|字符集。匹配包含的任一字符。例如，"[abc]"匹配"plain"中的"a"。|
|[^xyz]|反向字符集。匹配未包含的任何字符。例如，"[^abc]"匹配"plain"中"p"，"l"，"i"，"n"。|
|[a-z]|字符范围。匹配指定范围内的任何字符。例如，"[a-z]"匹配"a"到"z"范围内的任何小写字母。|
|[^a-z]|反向范围字符。匹配不在指定的范围内的任何字符。例如，"[^a-z]"匹配任何不在"a"到"z"范围内的任何字符。|
|\b|匹配一个字边界，即字与空格间的位置。例如，"er\b"匹配"never"中的"er"，但不匹配"verb"中的"er"。|
|\B|非字边界匹配。"er\B"匹配"verb"中的"er"，但不匹配"never"中的"er"。|
|\cx|匹配 x 指示的控制字符。例如，\cM 匹配 Control-M 或回车符。x 的值必须在 A-Z 或 a-z 之间。如果不是这样，则假定 c 就是"c"字符本身。|
|\d|数字字符匹配。等效于 [0-9]。|
|\D|非数字字符匹配。等效于 [^0-9]。|
|\f|换页符匹配。等效于 \x0c 和 \cL。|
|\n|换行符匹配。等效于 \x0a 和 \cJ。|
|\r|匹配一个回车符。等效于 \x0d 和 \cM。|
|\s|匹配任何空白字符，包括空格、制表符、换页符等。与 [ \f\n\r\t\v] 等效。|
|\S|匹配任何非空白字符。与 [^ \f\n\r\t\v] 等效。|
|\t|制表符匹配。与 \x09 和 \cI 等效。|
|\v|垂直制表符匹配。与 \x0b 和 \cK 等效。|
|\w|匹配任何字类字符，包括下划线。与"[A-Za-z0-9_]"等效。|
|\W|与任何非单词字符匹配。与"[^A-Za-z0-9_]"等效。|
|\xn|匹配 n，此处的 n 是一个十六进制转义码。十六进制转义码必须正好是两位数长。例如，"\x41"匹配"A"。"\x041"与"\x04"&"1"等效。允许在正则表达式中使用 ASCII 代码。|
|\num|匹配 num，此处的 num 是一个正整数。到捕获匹配的反向引用。例如，"(.)\1"匹配两个连续的相同字符。|
|\n|标识一个八进制转义码或反向引用。如果 \n 前面至少有 n 个捕获子表达式，那么 n 是反向引用。否则，如果 n 是八进制数 (0-7)，那么 n 是八进制转义码。|
|\nm|标识一个八进制转义码或反向引用。如果 \nm 前面至少有 nm 个捕获子表达式，那么 nm 是反向引用。如果 \nm 前面至少有 n 个捕获，则 n 是反向引用，后面跟有字符 m。如果两种前面的情况都不存在，则 \nm 匹配八进制值 nm，其中 n 和 m 是八进制数字 (0-7)。|
|\nml|当 n 是八进制数 (0-3)，m 和 l 是八进制数 (0-7) 时，匹配八进制转义码 nml。|
|\un|匹配 n，其中 n 是以四位十六进制数表示的 Unicode 字符。例如，\u00A9 匹配版权符号 (©)。|

## 6.4 Matcher 类

* 索引方法
    * start
    * end
* 研究方法
    * lookingAt
    * find
    * matches
* 替换方法
    * appendReplacement
    * appendTail
    * replaceAll
    * replaceFirst
    * quoteReplacement

```
import java.util.regex.Matcher;
import java.util.regex.Pattern;
 
public class RegexMatches
{
    private static final String REGEX = "\\bcat\\b";
    private static final String INPUT =
                                    "cat cat cat cattie cat";
 
    public static void main( String args[] ){
       Pattern p = Pattern.compile(REGEX);
       Matcher m = p.matcher(INPUT); // 获取 matcher 对象
       int count = 0;
 
       while(m.find()) {
         count++;
         System.out.println("Match number "+count);
         System.out.println("start(): "+m.start());
         System.out.println("end(): "+m.end());
      }
   }
}

// Match number 1
// start(): 0
// end(): 3
// Match number 2
// start(): 4
// end(): 7
// Match number 3
// start(): 8
// end(): 11
// Match number 4
// start(): 19
// end(): 22
```

```
import java.util.regex.Matcher;
import java.util.regex.Pattern;
 
public class RegexMatches
{
    private static final String REGEX = "foo";
    private static final String INPUT = "fooooooooooooooooo";
    private static final String INPUT2 = "ooooofoooooooooooo";
    private static Pattern pattern;
    private static Matcher matcher;
    private static Matcher matcher2;
 
    public static void main( String args[] ){
       pattern = Pattern.compile(REGEX);
       matcher = pattern.matcher(INPUT);
       matcher2 = pattern.matcher(INPUT2);
 
       System.out.println("Current REGEX is: "+REGEX);
       System.out.println("Current INPUT is: "+INPUT);
       System.out.println("Current INPUT2 is: "+INPUT2);
 
 
       System.out.println("lookingAt(): "+matcher.lookingAt());
       System.out.println("matches(): "+matcher.matches());
       System.out.println("lookingAt(): "+matcher2.lookingAt());
   }
}

Current REGEX is: foo
Current INPUT is: fooooooooooooooooo
Current INPUT2 is: ooooofoooooooooooo
lookingAt(): true
matches(): false
lookingAt(): false
```

```
import java.util.regex.Matcher;
import java.util.regex.Pattern;
 
public class RegexMatches
{
   private static String REGEX = "a*b";
   private static String INPUT = "aabfooaabfooabfoob";
   private static String REPLACE = "-";
   public static void main(String[] args) {
      Pattern p = Pattern.compile(REGEX);
      // 获取 matcher 对象
      Matcher m = p.matcher(INPUT);
      StringBuffer sb = new StringBuffer();
      while(m.find()){
         m.appendReplacement(sb,REPLACE);
      }
      m.appendTail(sb);
      System.out.println(sb.toString());
   }
}

-foo-foo-foo-
```

# 7.0 方法

## 7.1 方法的定义

```
修饰符 返回值类型 方法名(参数类型 参数名){
    ...
    方法体
    ...
    return 返回值;
}

/** 返回两个整型变量数据的较大值 */
public static int max(int num1, int num2) {
   int result;
   if (num1 > num2)
      result = num1;
   else
      result = num2;
 
   return result; 
}
```

## 7.2 可变参数

```
// typeName... parameterName
public class VarargsDemo {
    public static void main(String args[]) {
        // 调用可变参数的方法
        printMax(34, 3, 3, 2, 56.5);
        printMax(new double[]{1, 2, 3});
    }
 
    public static void printMax( double... numbers) {
        if (numbers.length == 0) {
            System.out.println("No argument passed");
            return;
        }
 
        double result = numbers[0];
 
        for (int i = 1; i <  numbers.length; i++){
            if (numbers[i] >  result) {
                result = numbers[i];
            }
        }
        System.out.println("The max value is " + result);
    }
}
```

## 7.3 finalize 方法

```
protected void finalize()
{
   // 在这里终结代码
}
```

# 8.0 Stream、File、IO 

## 8.1 控制台

### 8.1.1 输入

```
BufferedReader br = new BufferedReader(new 
                      InputStreamReader(System.in));
int c = br.read(); // -1 为流结束
String line = br.readLine();
```

### 8.1.2 输出

```
import java.io.*;
 
// 演示 System.out.write().
public class WriteDemo {
   public static void main(String args[]) {
      int b; 
      b = 'A';
      System.out.write(b);
      System.out.write('\n');
      System.out.print(b);
      System.out.print('\n');
      System.out.println(b);
   }
}
```

## 8.2 读写文件

### 8.2.1 FileInputStream

```
// 直接创建一个输入流来读取文件
InputStream f = new FileInputStream("C:/java/hello");

// 使用文件对象来创建输入流
File f = new File("C:/java/hello");
InputStream out = new FileInputStream(f);
```

> 常用方法

* close
* finalize
* read
* available

### 8.2.2 FileOutputStream

```
// 文件名
OutputStream f = new FileOutputStream("C:/java/hello")

// 文件对象
File f = new File("C:/java/hello");
OutputStream f = new FileOutputStream(f);
```

> 常用方法

* close
* finalize
* write

### 8.2.3 其他文件 I/O 类

* File
* FileReader
* FileWriter

#### 8.2.3.1 创建目录

> mkdir() 方法创建文件夹，成功则 true, 失败 false。中间路径不自动创建。
> mkdirs() 创建文件夹以及中间路径

```
// 创建目录 "/tmp/user/java/bin"
import java.io.File;
 
public class CreateDir {
  public static void main(String args[]) {
    String dirname = "/tmp/user/java/bin";
    File d = new File(dirname);
    // 现在创建目录
    d.mkdirs();
  }
}
```

#### 8.2.3.2 读取目录

```
import java.io.File;
 
public class DirList {
  public static void main(String args[]) {
    String dirname = "/tmp";
    File f1 = new File(dirname);
    if (f1.isDirectory()) {
      System.out.println( "目录 " + dirname);
      String s[] = f1.list();
      for (int i=0; i < s.length; i++) {
        File f = new File(dirname + "/" + s[i]);
        if (f.isDirectory()) {
          System.out.println(s[i] + " 是一个目录");
        } else {
          System.out.println(s[i] + " 是一个文件");
        }
      }
    } else {
      System.out.println(dirname + " 不是一个目录");
    }
  }
}

目录 /tmp
bin 是一个目录
lib 是一个目录
demo 是一个目录
test.txt 是一个文件
README 是一个文件
index.html 是一个文件
include 是一个目录
```

#### 8.2.3.3 删除目录

```
// 删除 /tmp/java/ 文件夹，即使不为空
import java.io.File;
 
public class DeleteFileDemo {
  public static void main(String args[]) {
      // 这里修改为自己的测试目录
    File folder = new File("/tmp/java/");
    deleteFolder(folder);
  }
 
  //删除文件及目录
  public static void deleteFolder(File folder) {
    File[] files = folder.listFiles();
        if(files!=null) { 
            for(File f: files) {
                if(f.isDirectory()) {
                    deleteFolder(f);
                } else {
                    f.delete();
                }
            }
        }
        folder.delete();
    }
}
```

### 8.2.4 示例

```
//文件名 :fileStreamTest2.java
import java.io.*;
 
public class fileStreamTest2{
  public static void main(String[] args) throws IOException {
    
    File f = new File("a.txt");
    FileOutputStream fop = new FileOutputStream(f);
    // 构建FileOutputStream对象,文件不存在会自动新建
    
    OutputStreamWriter writer = new OutputStreamWriter(fop, "UTF-8");
    // 构建OutputStreamWriter对象,参数可以指定编码,默认为操作系统默认编码,windows上是gbk
    
    writer.append("中文输入");
    // 写入到缓冲区
    
    writer.append("\r\n");
    //换行
    
    writer.append("English");
    // 刷新缓存冲,写入到文件,如果下面已经没有写入的内容了,直接close也会写入
    
    writer.close();
    //关闭写入流,同时会把缓冲区内容写入文件,所以上面的注释掉
    
    fop.close();
    // 关闭输出流,释放系统资源
 
    FileInputStream fip = new FileInputStream(f);
    // 构建FileInputStream对象
    
    InputStreamReader reader = new InputStreamReader(fip, "UTF-8");
    // 构建InputStreamReader对象,编码与写入相同
 
    StringBuffer sb = new StringBuffer();
    while (reader.ready()) {
      sb.append((char) reader.read());
      // 转成char加到StringBuffer对象中
    }
    System.out.println(sb.toString());
    reader.close();
    // 关闭读取流
    
    fip.close();
    // 关闭输入流,释放系统资源
 
  }
}
```

# 9.0 Scanner

> 获取用户输入

```
import java.util.Scanner; 
 
public class ScannerDemo {  
    public static void main(String[] args) {  
        Scanner scan = new Scanner(System.in); 
    // 从键盘接收数据  
 
    //next方式接收字符串
        System.out.println("next方式接收：");
        // 判断是否还有输入
        if(scan.hasNext()){   
          String str1 = scan.next();
          System.out.println("输入的数据为："+str1);  
        }  
 
    }  
}
```

> next()

* 一定要读取到有效字符后才可以结束输入。
* 对输入有效字符之前遇到的空白，next() 方法会自动将其去掉。
* 只有输入有效字符后才将其后面输入的空白作为分隔符或者结束符。
* next() 不能得到带有空格的字符串。

> nextLine()

* 以Enter为结束符,也就是说 nextLine()方法返回的是输入回车之前的所有字符。
* 可以获得空白。

> hasNextXXX() nextXXX()

可以获取 int 或者 float, double

# 10.0 异常处理

* 检查性异常：最具代表的检查性异常是用户错误或问题引起的异常，这是程序员无法预见的。例如要打开一个不存在文件时，一个异常就发生了，这些异常在编译时不能被简单地忽略。
* 运行时异常： 运行时异常是可能被程序员避免的异常。与检查性异常相反，运行时异常可以在编译时被忽略。
* 错误： 错误不是异常，而是脱离程序员控制的问题。错误在代码中通常被忽略。例如，当栈溢出时，一个错误就发生了，它们在编译也检查不到的。

## 10.1 捕获异常

```
try{
   // 程序代码
}catch(异常类型1 异常的变量名1){
  // 程序代码
}catch(异常类型2 异常的变量名2){
  // 程序代码
}catch(异常类型2 异常的变量名2){
  // 程序代码
}
```

```
// 文件名 : ExcepTest.java
import java.io.*;
public class ExcepTest{
 
   public static void main(String args[]){
      try{
         int a[] = new int[2];
         System.out.println("Access element three :" + a[3]);
      }catch(ArrayIndexOutOfBoundsException e){
         System.out.println("Exception thrown  :" + e);
      }
      System.out.println("Out of the block");
   }
}

Exception thrown  :java.lang.ArrayIndexOutOfBoundsException: 3
Out of the block
```

## 10.2 throws/throw 关键字

```
import java.io.*;
public class className
{
  public void deposit(double amount) throws RemoteException
  {
    // Method implementation
    throw new RemoteException();
  }
  //Remainder of class definition
}
```

## 10.3 finally 关键字

finally 总会被执行

```
try{
  // 程序代码
}catch(异常类型1 异常的变量名1){
  // 程序代码
}catch(异常类型2 异常的变量名2){
  // 程序代码
}finally{
  // 程序代码
}
```

## 10.4 声明自定义异常

```
// 文件名InsufficientFundsException.java
import java.io.*;
 
//自定义异常类，继承Exception类
public class InsufficientFundsException extends Exception
{
  //此处的amount用来储存当出现异常（取出钱多于余额时）所缺乏的钱
  private double amount;
  public InsufficientFundsException(double amount)
  {
    this.amount = amount;
  } 
  public double getAmount()
  {
    return amount;
  }
}
```

## 10.5 通用异常

* JVM(Java虚拟机) 异常：由 JVM 抛出的异常或错误。例如：NullPointerException 类，ArrayIndexOutOfBoundsException 类，ClassCastException 类。
* 程序级异常：由程序或者API程序抛出的异常。例如 IllegalArgumentException 类，IllegalStateException 类。

# 11.0 面向对象

## 11.1 对象和类

* 对象：对象是类的一个实例（对象不是找个女朋友），有状态和行为。例如，一条狗是一个对象，它的状态有：颜色、名字、品种；行为有：摇尾巴、叫、吃等。
* 类：类是一个模板，它描述一类对象的行为和状态。

```
public class ClassName {
    /* 成员变量 */
    /* 类变量 */
    /* 方法 */
    /* 类方法 */

    /* 构造方法 */
    public ClassName(...) { }
}

// 创建对象
ClassName value = new ClassName();
```

## 11.2 继承

```
class 父类 {    
}

class 子类 extends 父类 {
}
```

* 子类拥有父类非private的属性，方法。
* 子类可以拥有自己的属性和方法，即子类可以对父类进行扩展。
* 子类可以用自己的方式实现父类的方法。
* Java的继承是单继承，但是可以多重继承，单继承就是一个子类只能继承一个父类，多重继承就是，例如A类继承B类，B类继承C类，所以按照关系就是C类是B类的父类，B类是A类的父类，这是java继承区别于C++继承的一个特性。
* 提高了类之间的耦合性（继承的缺点，耦合度高就会造成代码之间的联系）。


> implemenets 实现接口

```
public interface A {
    public void eat();
    public void sleep();
}
 
public interface B {
    public void show();
}
 
public class C implements A,B {
}
```

> super 与 this

super 指向父类方法，this 指向本类

> final

final 关键字声明类可以把类定义为不能继承的，即最终类；或者用于修饰方法，该方法不能被子类重写。

> 构造器

子类构造器中如果不显式的调用父类构造器，则自动调用父类无参数构造器。

```
class SuperClass {
  private int n;
  SuperClass(){
    System.out.println("SuperClass()");
  }
  SuperClass(int n) {
    System.out.println("SuperClass(int n)");
    this.n = n;
  }
}
class SubClass extends SuperClass{
  private int n;
  
  SubClass(){
    super(300);
    System.out.println("SubClass");
  }  
  
  public SubClass(int n){
    System.out.println("SubClass(int n):"+n);
    this.n = n;
  }
}
public class TestSuperSub{
  public static void main (String args[]){
    SubClass sc = new SubClass();
    SubClass sc2 = new SubClass(200); 
  }
}

SuperClass(int n)
SubClass
SuperClass()
SubClass(int n):200
```

## 11.3 重写 (Override) 与重载 (Overload)

### 11.3.1 重写

```
class Animal{
   public void move(){
      System.out.println("动物可以移动");
   }
}
 
class Dog extends Animal{
   public void move(){
      System.out.println("狗可以跑和走");
   }
}
```

> 无法调用该指针以外的方法

```
class Animal{
   public void move(){
      System.out.println("动物可以移动");
   }
}
 
class Dog extends Animal{
   public void move(){
      System.out.println("狗可以跑和走");
   }
   public void bark(){
      System.out.println("狗可以吠叫");
   }
}
 
public class TestDog{
   public static void main(String args[]){
      Animal a = new Animal(); // Animal 对象
      Animal b = new Dog(); // Dog 对象
 
      a.move();// 执行 Animal 类的方法
      b.move();// 执行 Dog 类的方法
      b.bark();// 抛出错误，虽然 Dog 有，但是 Animal 没有这个方法
   }
}
```

> 重写规则

* 参数列表必须完全与被重写方法的相同；
* 返回类型必须完全与被重写方法的返回类型相同；
* 访问权限不能比父类中被重写的方法的访问权限更低。例如：如果父类的一个方法被声明为public，那么在子类中重写该方法就不能声明为protected。
* 父类的成员方法只能被它的子类重写。
* 声明为final的方法不能被重写。
* 声明为static的方法不能被重写，但是能够被再次声明。
* 子类和父类在同一个包中，那么子类可以重写父类所有方法，除了声明为private和final的方法。
* 子类和父类不在同一个包中，那么子类只能够重写父类的声明为public和protected的非final方法。
* 重写的方法能够抛出任何非强制异常，无论被重写的方法是否抛出异常。但是，重写的方法不能抛出新的强制性异常，或者比被重写方法声明的更广泛的强制性异常，反之则可以。
* 构造方法不能被重写。
* 如果不能继承一个方法，则不能重写这个方法。

> super 关键字

可以在重写方法中使用 super 关键字调用父类方法

### 11.3.2 重载

> 重载(overloading) 是在一个类里面，方法名字相同，而参数不同。返回类型可以相同也可以不同。
> 每个重载的方法（或者构造函数）都必须有一个独一无二的参数类型列表。
> 最常用的地方就是构造器的重载。

* 被重载的方法必须改变参数列表(参数个数或类型或顺序不一样)；
* 被重载的方法可以改变返回类型；
* 被重载的方法可以改变访问修饰符；
* 被重载的方法可以声明新的或更广的检查异常；
* 方法能够在同一个类中或者在一个子类中被重载。
* 无法以返回值类型作为重载函数的区分标准。

## 11.4 多态

> 多态是同一个行为具有多个不同表现形式或形态的能力。

```
// 
abstract class Animal {
    abstract void eat();  
}

class Cat extends Animal {  
    public void eat() {  
        System.out.println("吃鱼");  
    }  
    public void work() {  
        System.out.println("抓老鼠");  
    }  
}  
  
class Dog extends Animal {  
    public void eat() {  
        System.out.println("吃骨头");  
    }  
    public void work() {  
        System.out.println("看家");  
    }  
}

// 调用
public class Test {
    public static void main(String[] args) {
      show(new Cat());  // 以 Cat 对象调用 show 方法
      show(new Dog());  // 以 Dog 对象调用 show 方法
                
      Animal a = new Cat();  // 向上转型  
      a.eat();               // 调用的是 Cat 的 eat
      Cat c = (Cat)a;        // 向下转型  
      c.work();        // 调用的是 Cat 的 work
  }  
            
    public static void show(Animal a)  {
      a.eat();  
        // 类型判断
        if (a instanceof Cat)  {  // 猫做的事情 
            Cat c = (Cat)a;  
            c.work();  
        } else if (a instanceof Dog) { // 狗做的事情 
            Dog c = (Dog)a;  
            c.work();  
        }  
    }  
}

吃鱼
抓老鼠
吃骨头
看家
吃鱼
抓老鼠
```

### 11.4.1 多态的实现方式

* 重写

这个内容已经在上一章节详细讲过，就不再阐述，详细可访问：Java 重写(Override)与重载(Overload)。

* 接口

    1. 生活中的接口最具代表性的就是插座，例如一个三接头的插头都能接在三孔插座中，因为这个是每个国家都有各自规定的接口规则，有可能到国外就不行，那是因为国外自己定义的接口类型。
    2. java中的接口类似于生活中的接口，就是一些方法特征的集合，但没有方法的实现。具体可以看 java接口 这一章节的内容。

* 抽象类和抽象方法

## 11.5 抽象类

```
public abstract class Employee {
    public abstract void pay();
}

public class Salary extends Employee {
    public void pay() {
        // ...
    }
}
```

* 抽象类不能被实例化，如果被实例化，就会报错，编译无法通过。只有抽象类的非抽象子类可以创建对象。
* 抽象类中不一定包含抽象方法，但是有抽象方法的类必定是抽象类。
* 抽象类中的抽象方法只是声明，不包含方法体，就是不给出方法的具体实现也就是方法的具体功能。
* 构造方法，类方法（用static修饰的方法）不能声明为抽象方法。
* 抽象类的子类必须给出抽象类中的抽象方法的具体实现，除非该子类也是抽象类。

## 11.6 封装

通过可见性进行控制。

## 11.7 接口

## 11.8 包

# 12.0 高级教程

## 12.1 数据结构

### 12.1.1 枚举（Enumeration）

* boolean hasMoreElements( )
* Object nextElement( )

```
import java.util.Vector;
import java.util.Enumeration;
 
public class EnumerationTester {
 
   public static void main(String args[]) {
      Enumeration<String> days;
      Vector<String> dayNames = new Vector<String>();
      dayNames.add("Sunday");
      dayNames.add("Monday");
      dayNames.add("Tuesday");
      dayNames.add("Wednesday");
      dayNames.add("Thursday");
      dayNames.add("Friday");
      dayNames.add("Saturday");
      days = dayNames.elements();
      while (days.hasMoreElements()){
         System.out.println(days.nextElement()); 
      }
   }
}

Sunday
Monday
Tuesday
Wednesday
Thursday
Friday
Saturday
```

### 12.1.2 位集合（BitSet）
### 12.1.3 向量（Vector）
### 12.1.4 栈（Stack）
### 12.1.5 字典（Dictionary）Map

Dictionary 已经过时，现在使用 Map.

### 12.1.6 哈希表（Hashtable）

Properties
### 12.1.7 属性（Properties）

## 12.2 集合框架

### 12.2.1 集合接口

* Collection 接口
    * Collection 是最基本的集合接口，一个 Collection 代表一组 Object，Java不提供直接继承自Collection的类，只提供继承于的子接口(如List和set)。
* List 接口
    * List接口是一个有序的Collection，使用此接口能够精确的控制每个元素插入的位置，能够通过索引(元素在List中位置，类似于数组的小标)来访问List中的元素，而且允许有相同的元素。
* Set
    * Set 具有与 Collection 完全一样的接口，只是行为上不同，Set 不保存重复的元素。
* SortedSet
    * 继承于Set保存有序的集合。
* Map
    * 将唯一的键映射到值。
* Map.Entry
    * 描述在一个Map中的一个元素（键/值对）。是一个Map的内部类。
* SortedMap
    * 继承于Map，使Key保持在升序排列。
* Enumeration
    * 这是一个传统的接口和定义的方法，通过它可以枚举（一次获得一个）对象集合中的元素。这个传统接口已被迭代器取代。

### 12.2.2 集合实现

* AbstractCollection 
    * 实现了大部分的集合接口。
* AbstractList 
    * 继承于AbstractCollection 并且实现了大部分List接口。
* AbstractSequentialList 
    * 继承于 AbstractList ，提供了对数据元素的链式访问而不是随机访问。
* LinkedList
    * 该类实现了List接口，允许有null（空）元素。主要用于创建链表数据结构，该类没有同步方法，如果多个线程同时访问一个List，则必须自己实现访问同步，解决方法就是在创建List时候构造一个同步的List。例如：
    * `Listlist=Collections.synchronizedList(newLinkedList(...));`
    * LinkedList 查找效率低。
* ArrayList
    * 该类也是实现了List的接口，实现了可变大小的数组，随机访问和遍历元素时，提供更好的性能。该类也是非同步的,在多线程的情况下不要使用。ArrayList 增长当前长度的50%，插入删除效率低。
* AbstractSet 
    * 继承于AbstractCollection 并且实现了大部分Set接口。
* HashSet
    * 该类实现了Set接口，不允许出现重复元素，不保证集合中元素的顺序，允许包含值为null的元素，但最多只能一个。
* LinkedHashSet
    * 具有可预知迭代顺序的 Set 接口的哈希表和链接列表实现。
* TreeSet
    * 该类实现了Set接口，可以实现排序等功能。
* AbstractMap 
    * 实现了大部分的Map接口。
* HashMap 
    * HashMap 是一个散列表，它存储的内容是键值对(key-value)映射。
    * 该类实现了Map接口，根据键的HashCode值存储数据，具有很快的访问速度，最多允许一条记录的键为null，不支持线程同步。
* TreeMap 
    * 继承了AbstractMap，并且使用一颗树。
* WeakHashMap 
    * 继承AbstractMap类，使用弱密钥的哈希表。
* LinkedHashMap 
    * 继承于HashMap，使用元素的自然顺序对元素进行排序.
* IdentityHashMap 
    * 继承AbstractMap类，比较文档时使用引用相等。

### 12.2.3 迭代器

```
public class Test{
 public static void main(String[] args) {
     List<String> list=new ArrayList<String>();
     list.add("Hello");
     list.add("World");
     list.add("HAHAHAHA");
     //第一种遍历方法使用foreach遍历List
     for (String str : list) {            //也可以改写for(int i=0;i<list.size();i++)这种形式
        System.out.println(str);
     }
 
     //第二种遍历，把链表变为数组相关的内容进行遍历
     String[] strArray=new String[list.size()];
     list.toArray(strArray);
     for(int i=0;i<strArray.length;i++) //这里也可以改写为  foreach(String str:strArray)这种形式
     {
        System.out.println(strArray[i]);
     }
     
    //第三种遍历 使用迭代器进行相关遍历
     
     Iterator<String> ite=list.iterator();
     while(ite.hasNext())//判断下一个元素之后有值
     {
         System.out.println(ite.next());
     }
 }
}
```

> Map

```
public class Test{
     public static void main(String[] args) {
      Map<String, String> map = new HashMap<String, String>();
      map.put("1", "value1");
      map.put("2", "value2");
      map.put("3", "value3");
      
      //第一种：普遍使用，二次取值
      System.out.println("通过Map.keySet遍历key和value：");
      for (String key : map.keySet()) {
       System.out.println("key= "+ key + " and value= " + map.get(key));
      }
      
      //第二种
      System.out.println("通过Map.entrySet使用iterator遍历key和value：");
      Iterator<Map.Entry<String, String>> it = map.entrySet().iterator();
      while (it.hasNext()) {
       Map.Entry<String, String> entry = it.next();
       System.out.println("key= " + entry.getKey() + " and value= " + entry.getValue());
      }
      
      //第三种：推荐，尤其是容量大时
      System.out.println("通过Map.entrySet遍历key和value");
      for (Map.Entry<String, String> entry : map.entrySet()) {
       System.out.println("key= " + entry.getKey() + " and value= " + entry.getValue());
      }
    
      //第四种
      System.out.println("通过Map.values()遍历所有的value，但不能遍历key");
      for (String v : map.values()) {
       System.out.println("value= " + v);
      }
     }
}
```

## 12.3 泛型

### 12.3.1 泛型方法

```
public class GenericMethodTest
{
   // 泛型方法 printArray                         
   public static < E > void printArray( E[] inputArray )
   {
      // 输出数组元素            
         for ( E element : inputArray ){        
            System.out.printf( "%s ", element );
         }
         System.out.println();
    }
 
    public static void main( String args[] )
    {
        // 创建不同类型数组： Integer, Double 和 Character
        Integer[] intArray = { 1, 2, 3, 4, 5 };
        Double[] doubleArray = { 1.1, 2.2, 3.3, 4.4 };
        Character[] charArray = { 'H', 'E', 'L', 'L', 'O' };
 
        System.out.println( "整型数组元素为:" );
        printArray( intArray  ); // 传递一个整型数组
 
        System.out.println( "\n双精度型数组元素为:" );
        printArray( doubleArray ); // 传递一个双精度型数组
 
        System.out.println( "\n字符型数组元素为:" );
        printArray( charArray ); // 传递一个字符型数组
    } 
}


整型数组元素为:
1 2 3 4 5 

双精度型数组元素为:
1.1 2.2 3.3 4.4 

字符型数组元素为:
H E L L O 
```

> 有界限类型

```
public class MaximumTest
{
   // 比较三个值并返回最大值
   public static <T extends Comparable<T>> T maximum(T x, T y, T z)
   {                     
      T max = x; // 假设x是初始最大值
      if ( y.compareTo( max ) > 0 ){
         max = y; //y 更大
      }
      if ( z.compareTo( max ) > 0 ){
         max = z; // 现在 z 更大           
      }
      return max; // 返回最大对象
   }
   public static void main( String args[] )
   {
      System.out.printf( "%d, %d 和 %d 中最大的数为 %d\n\n",
                   3, 4, 5, maximum( 3, 4, 5 ) );
 
      System.out.printf( "%.1f, %.1f 和 %.1f 中最大的数为 %.1f\n\n",
                   6.6, 8.8, 7.7, maximum( 6.6, 8.8, 7.7 ) );
 
      System.out.printf( "%s, %s 和 %s 中最大的数为 %s\n","pear",
         "apple", "orange", maximum( "pear", "apple", "orange" ) );
   }
}

3, 4 和 5 中最大的数为 5

6.6, 8.8 和 7.7 中最大的数为 8.8

pear, apple 和 orange 中最大的数为 pear
```

### 12.3.2 泛型类

```
public class Box<T> {
   
  private T t;
 
  public void add(T t) {
    this.t = t;
  }
 
  public T get() {
    return t;
  }
 
  public static void main(String[] args) {
    Box<Integer> integerBox = new Box<Integer>();
    Box<String> stringBox = new Box<String>();
 
    integerBox.add(new Integer(10));
    stringBox.add(new String("菜鸟教程"));
 
    System.out.printf("整型值为 :%d\n\n", integerBox.get());
    System.out.printf("字符串为 :%s\n", stringBox.get());
  }
}

整型值为 :10

字符串为 :菜鸟教程
```

> 类型通配符

```
public class GenericTest {
     
    public static void main(String[] args) {
        List<String> name = new ArrayList<String>();
        List<Integer> age = new ArrayList<Integer>();
        List<Number> number = new ArrayList<Number>();
        
        name.add("icon");
        age.add(18);
        number.add(314);
 
        getData(name);
        getData(age);
        getData(number);
       
   }
  
   // 通配符
   public static void getData(List<?> data) {
      System.out.println("data :" + data.get(0));
   }

   // 限制通配符
   public static void getUperNumber(List<? extends Number> data) {
      System.out.println("data :" + data.get(0));
   }
}
```

## 12.4 序列化

> ObjectInputStream/ObjectOutputStream 是高层次的数据流，它们包含序列化和反序列化对象的方法。

```
// 序列化一个对象，并且发送到输出流
public final void writeObject(Object x) throws IOException

// 从流中去除下一个对象，并反序列化
public final Object readObject() throws IOException, ClassNotFoundException
```

> 序列化

```
import java.io.*;
 
public class SerializeDemo
{
   public static void main(String [] args)
   {
      Employee e = new Employee();
      e.name = "Reyan Ali";
      e.address = "Phokka Kuan, Ambehta Peer";
      e.SSN = 11122333;
      e.number = 101;
      try
      {
         FileOutputStream fileOut =
         new FileOutputStream("/tmp/employee.ser");
         ObjectOutputStream out = new ObjectOutputStream(fileOut);
         out.writeObject(e);
         out.close();
         fileOut.close();
         System.out.printf("Serialized data is saved in /tmp/employee.ser");
      }catch(IOException i)
      {
          i.printStackTrace();
      }
   }
}
```

> 反序列化

```
import java.io.*;
 
public class DeserializeDemo
{
   public static void main(String [] args)
   {
      Employee e = null;
      try
      {
         FileInputStream fileIn = new FileInputStream("/tmp/employee.ser");
         ObjectInputStream in = new ObjectInputStream(fileIn);
         e = (Employee) in.readObject();
         in.close();
         fileIn.close();
      }catch(IOException i)
      {
         i.printStackTrace();
         return;
      }catch(ClassNotFoundException c)
      {
         System.out.println("Employee class not found");
         c.printStackTrace();
         return;
      }
      System.out.println("Deserialized Employee...");
      System.out.println("Name: " + e.name);
      System.out.println("Address: " + e.address);
      System.out.println("SSN: " + e.SSN);
      System.out.println("Number: " + e.number);
    }
}
```

## 12.5 网络编程

### 12.5.1 Socket 编程

> 客户端

```
// 文件名 GreetingClient.java
 
import java.net.*;
import java.io.*;
 
public class GreetingClient
{
   public static void main(String [] args)
   {
      String serverName = args[0];
      int port = Integer.parseInt(args[1]);
      try
      {
         System.out.println("连接到主机：" + serverName + " ，端口号：" + port);
         Socket client = new Socket(serverName, port);
         System.out.println("远程主机地址：" + client.getRemoteSocketAddress());
         OutputStream outToServer = client.getOutputStream();
         DataOutputStream out = new DataOutputStream(outToServer);
 
         out.writeUTF("Hello from " + client.getLocalSocketAddress());
         InputStream inFromServer = client.getInputStream();
         DataInputStream in = new DataInputStream(inFromServer);
         System.out.println("服务器响应： " + in.readUTF());
         client.close();
      }catch(IOException e)
      {
         e.printStackTrace();
      }
   }
}
```

> 服务端

```
// 文件名 GreetingServer.java
 
import java.net.*;
import java.io.*;
 
public class GreetingServer extends Thread
{
   private ServerSocket serverSocket;
   
   public GreetingServer(int port) throws IOException
   {
      serverSocket = new ServerSocket(port);
      serverSocket.setSoTimeout(10000);
   }
 
   public void run()
   {
      while(true)
      {
         try
         {
            System.out.println("等待远程连接，端口号为：" + serverSocket.getLocalPort() + "...");
            Socket server = serverSocket.accept();
            System.out.println("远程主机地址：" + server.getRemoteSocketAddress());
            DataInputStream in = new DataInputStream(server.getInputStream());
            System.out.println(in.readUTF());
            DataOutputStream out = new DataOutputStream(server.getOutputStream());
            out.writeUTF("谢谢连接我：" + server.getLocalSocketAddress() + "\nGoodbye!");
            server.close();
         }catch(SocketTimeoutException s)
         {
            System.out.println("Socket timed out!");
            break;
         }catch(IOException e)
         {
            e.printStackTrace();
            break;
         }
      }
   }
   public static void main(String [] args)
   {
      int port = Integer.parseInt(args[0]);
      try
      {
         Thread t = new GreetingServer(port);
         t.run();
      }catch(IOException e)
      {
         e.printStackTrace();
      }
   }
}
```

### 12.5.2 URL 处理

```
import java.net.*;
import java.io.*;
 
public class URLDemo
{
   public static void main(String [] args)
   {
      try
      {
         URL url = new URL("http://www.runoob.com/index.html?language=cn#j2se");
         System.out.println("URL 为：" + url.toString());
         System.out.println("协议为：" + url.getProtocol());
         System.out.println("验证信息：" + url.getAuthority());
         System.out.println("文件名及请求参数：" + url.getFile());
         System.out.println("主机名：" + url.getHost());
         System.out.println("路径：" + url.getPath());
         System.out.println("端口：" + url.getPort());
         System.out.println("默认端口：" + url.getDefaultPort());
         System.out.println("请求参数：" + url.getQuery());
         System.out.println("定位位置：" + url.getRef());
      }catch(IOException e)
      {
         e.printStackTrace();
      }
   }
}

URL 为：http://www.runoob.com/index.html?language=cn#j2se
协议为：http
验证信息：www.runoob.com
文件名及请求参数：/index.html?language=cn
主机名：www.runoob.com
路径：/index.html
端口：-1
默认端口：80
请求参数：language=cn
定位位置：j2se
```

> URLConnections 类方法

```
import java.net.*;
import java.io.*;
public class URLConnDemo
{
   public static void main(String [] args)
   {
      try
      {
         URL url = new URL("http://www.runoob.com");
         URLConnection urlConnection = url.openConnection();
         HttpURLConnection connection = null;
         if(urlConnection instanceof HttpURLConnection)
         {
            connection = (HttpURLConnection) urlConnection;
         }
         else
         {
            System.out.println("请输入 URL 地址");
            return;
         }
         BufferedReader in = new BufferedReader(
         new InputStreamReader(connection.getInputStream()));
         String urlString = "";
         String current;
         while((current = in.readLine()) != null)
         {
            urlString += current;
         }
         System.out.println(urlString);
      }catch(IOException e)
      {
         e.printStackTrace();
      }
   }
}

$ javac URLConnDemo.java 
$ java URLConnDemo
.....这里会输出菜鸟教程首页(http://www.runoob.com)的 HTML 内容.....
```

## 12.6 发送邮件

## 12.7 多线程编程

> Runnable 接口创建线程

```
class RunnableDemo implements Runnable {
   private Thread t;
   private String threadName;
   
   RunnableDemo( String name) {
      threadName = name;
      System.out.println("Creating " +  threadName );
   }
   
   public void run() {
      System.out.println("Running " +  threadName );
      try {
         for(int i = 4; i > 0; i--) {
            System.out.println("Thread: " + threadName + ", " + i);
            // 让线程睡眠一会
            Thread.sleep(50);
         }
      }catch (InterruptedException e) {
         System.out.println("Thread " +  threadName + " interrupted.");
      }
      System.out.println("Thread " +  threadName + " exiting.");
   }
   
   public void start () {
      System.out.println("Starting " +  threadName );
      if (t == null) {
         t = new Thread (this, threadName);
         t.start ();
      }
   }
}
 
public class TestThread {
 
   public static void main(String args[]) {
      RunnableDemo R1 = new RunnableDemo( "Thread-1");
      R1.start();
      
      RunnableDemo R2 = new RunnableDemo( "Thread-2");
      R2.start();
   }   
}
```

> 通过继承 Thread 来创建线程

```
class ThreadDemo extends Thread {
   private Thread t;
   private String threadName;
   
   ThreadDemo( String name) {
      threadName = name;
      System.out.println("Creating " +  threadName );
   }
   
   public void run() {
      System.out.println("Running " +  threadName );
      try {
         for(int i = 4; i > 0; i--) {
            System.out.println("Thread: " + threadName + ", " + i);
            // 让线程睡醒一会
            Thread.sleep(50);
         }
      }catch (InterruptedException e) {
         System.out.println("Thread " +  threadName + " interrupted.");
      }
      System.out.println("Thread " +  threadName + " exiting.");
   }
   
   public void start () {
      System.out.println("Starting " +  threadName );
      if (t == null) {
         t = new Thread (this, threadName);
         t.start ();
      }
   }
}
 
public class TestThread {
 
   public static void main(String args[]) {
      ThreadDemo T1 = new ThreadDemo( "Thread-1");
      T1.start();
      
      ThreadDemo T2 = new ThreadDemo( "Thread-2");
      T2.start();
   }   
}
```

> 通过 Callable 和 Future 创建线程

```
public class CallableThreadTest implements Callable<Integer> {
    public static void main(String[] args)  
    {  
        CallableThreadTest ctt = new CallableThreadTest();  
        FutureTask<Integer> ft = new FutureTask<>(ctt);  
        for(int i = 0;i < 100;i++)  
        {  
            System.out.println(Thread.currentThread().getName()+" 的循环变量i的值"+i);  
            if(i==20)  
            {  
                new Thread(ft,"有返回值的线程").start();  
            }  
        }  
        try  
        {  
            System.out.println("子线程的返回值："+ft.get());  
        } catch (InterruptedException e)  
        {  
            e.printStackTrace();  
        } catch (ExecutionException e)  
        {  
            e.printStackTrace();  
        }  
  
    }
    @Override  
    public Integer call() throws Exception  
    {  
        int i = 0;  
        for(;i<100;i++)  
        {  
            System.out.println(Thread.currentThread().getName()+" "+i);  
        }  
        return i;  
    }  
}
```

## 12.8 Applet

### 12.8.1 Applet 概述

* Java 中 Applet 类继承了 java.applet.Applet 类。
* Applet 类没有定义 main()，所以一个 Applet 程序不会调用 main() 方法。
* Applet 被设计为嵌入在一个 HTML 页面。
* 当用户浏览包含 Applet 的 HTML 页面，Applet 的代码就被下载到用户的机器上。
* 要查看一个 Applet 需要 JVM。 JVM 可以是 Web 浏览器的一个插件，或一个独立的运行时环境。
* 用户机器上的 JVM 创建一个 Applet 类的实例，并调用 Applet 生命周期过程中的各种方法。
* Applet 有 Web 浏览器强制执行的严格的安全规则，Applet 的安全机制被称为沙箱安全。
* Applet 需要的其他类可以用 Java 归档（JAR）文件的形式下载下来。

### 12.8.2 Applet 生命周期

* init: 该方法的目的是为你的 Applet 提供所需的任何初始化。在 Applet 标记内的 param 标签被处理后调用该方法。
* start: 浏览器调用 init 方法后，该方法被自动调用。每当用户从其他页面返回到包含 Applet 的页面时，则调用该方法。
* stop: 当用户从包含 Applet 的页面移除的时候，该方法自动被调用。因此，可以在相同的 Applet 中反复调用该方法。
* destroy: 此方法仅当浏览器正常关闭时调用。因为 Applet 只有在 HTML 网页上有效，所以你不应该在用户离开包含 Applet 的页面后遗漏任何资源。
* paint: 该方法在 start() 方法之后立即被调用，或者在 Applet 需要重绘在浏览器的时候调用。paint() 方法实际上继承于 java.awt。

```
import java.applet.*;
import java.awt.*;
 
public class HelloWorldApplet extends Applet
{
   public void paint (Graphics g)
   {
      g.drawString ("Hello World", 25, 50);
   }
}
```

### 12.8.3 Applet 类功能

* 每一个 Applet 都是 java.applet.Applet 类的子类，基础的 Applet 类提供了供衍生类调用的方法,以此来得到浏览器上下文的信息和服务。这些方法做了如下事情：
    * 得到 Applet 的参数
    * 得到包含 Applet 的 HTML 文件的网络位置
    * 得到 Applet 类目录的网络位置
    * 打印浏览器的状态信息
    * 获取一张图片
    * 获取一个音频片段
    * 播放一个音频片段
    * 调整此 Applet 的大小
* 除此之外，Applet 类还提供了一个接口，该接口供 Viewer 或浏览器来获取 Applet 的信息，并且来控制 Applet 的执行。Viewer 可能是：
    * 请求 Applet 作者、版本和版权的信息
    * 请求 Applet 识别的参数的描述
    * 初始化 Applet
    * 销毁 Applet
    * 开始执行 Applet
    * 结束执行 Applet
    * Applet 类提供了对这些方法的默认实现，这些方法可以在需要的时候重写。
    * "Hello，World"applet 都是按标准编写的。唯一被重写的方法是 paint 方法。

### 12.8.4 Applet 调用

> 调用代码
>     注意: 你可以参照 HTML Applet 标签来更多的了解从 HTML 中调用 applet 的方法。

```
<html>
<title>The Hello, World Applet</title>
    <hr>
        <applet code="HelloWorldApplet.class" width="320" height="120">
            If your browser was Java-enabled, a "Hello, World"
            message would appear here.
        </applet>
    <hr>
</html>
```

> Viewer 或者浏览器在文档的位置寻找编译过的 Java 代码，要指定文档的路径，得使用 <applet> 标签的 codebase 属性指定。

```
<applet codebase="http://amrood.com/applets"
code="HelloWorldApplet.class" width="320" height="120">
```

> 如果 Applet 所在一个包中而不是默认包，那么所在的包必须在 code 属性里指定，例如：

```
<applet code="mypackage.subpackage.TestApplet.class"
           width="320" height="120">
```

### 12.8.5 Applet 参数

> 设置

```
<html>
<title>Checkerboard Applet</title>
<hr>
<applet code="CheckerApplet.class" width="480" height="320">
<param name="color" value="blue">
<param name="squaresize" value="30">
</applet>
<hr>
</html>
```

> 获取

```
String squareSizeParam = getParameter ("squareSize");
```

### 12.8.6 应用程序转换成 Applet

* 将图形化的 Java 应用程序（是指，使用AWT的应用程序和使用 java 程序启动器启动的程序）转换成嵌入在web页面里的applet的几个步骤：
    * 编写一个 HTML 页面，该页面带有能加载 applet 代码的标签。
    * 编写一个 JApplet 类的子类，将该类设置为 public。否则，Applet 不能被加载。
    * 消除应用程序的 main()方法。不要为应用程序构造框架窗口，因为你的应用程序要显示在浏览器中。
    * 将应用程序中框架窗口的构造方法里的初始化代码移到 Applet 的 init() 方法中，你不必显示的构造 Applet 对象，浏览器将通过调用 init() 方法来实例化一个对象。
    * 移除对 setSize() 方法的调用，对于 Applet 来讲，大小已经通过 HTML 文件里的 width 和 height 参数设定好了。
    * 移除对 setDefaultCloseOperation() 方法的调用。Applet 不能被关闭，它随着浏览器的退出而终止。
    * 如果应用程序调用了 setTitle() 方法，消除对该方法的调用。applet 不能有标题栏。（当然你可以给通过 html 的 title 标签给网页自身命名）
    * 不要调用 setVisible(true),Applet 是自动显示的。


### 12.8.7 事件处理

Applet 类从 Container 类继承了许多事件处理方法。Container 类定义了几个方法，例如：processKeyEvent() 和processMouseEvent()，用来处理特别类型的事件，还有一个捕获所有事件的方法叫做 processEvent。
为了响应一个事件，Applet 必须重写合适的事件处理方法。

最开始运行，Applet 显示 "initializing the applet. Starting the applet."，然后你一点击矩形框，就会显示 "mouse clicked" 。

```
import java.awt.event.MouseListener;
import java.awt.event.MouseEvent;
import java.applet.Applet;
import java.awt.Graphics;
 
public class ExampleEventHandling extends Applet
                             implements MouseListener {
 
    StringBuffer strBuffer;
 
    public void init() {
         addMouseListener(this);
         strBuffer = new StringBuffer();
        addItem("initializing the apple ");
    }
 
    public void start() {
        addItem("starting the applet ");
    }
 
    public void stop() {
        addItem("stopping the applet ");
    }
 
    public void destroy() {
        addItem("unloading the applet");
    }
 
    void addItem(String word) {
        System.out.println(word);
        strBuffer.append(word);
        repaint();
    }
 
    public void paint(Graphics g) {
         //Draw a Rectangle around the applet's display area.
        g.drawRect(0, 0,
                      getWidth() - 1,
                      getHeight() - 1);
 
         //display the string inside the rectangle.
        g.drawString(strBuffer.toString(), 10, 20);
    }
 
  
    public void mouseEntered(MouseEvent event) {
    }
    public void mouseExited(MouseEvent event) {
    }
    public void mousePressed(MouseEvent event) {
    }
    public void mouseReleased(MouseEvent event) {
    }
 
    public void mouseClicked(MouseEvent event) {
         addItem("mouse clicked! ");
    }
}
```

```
<html>
    <title>Event Handling</title>
        <hr>
            <applet code="ExampleEventHandling.class"
            width="300" height="300">
        </applet>
    <hr>
</html>
```



