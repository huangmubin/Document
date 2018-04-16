# 基本语法

```C++
// 单行注释
/* 
 多行注释块
 */

// 导入类库
#include <library name>
#include <iostream>

// 使用命名空间
using namespace <name space>;
using namespace std;

// 主程序
int main() {
    // 输出语句
    cout << "Hello World" << endl; // Hello World\n -- endl 表示结尾换行
    
    return 0;
}
```

# 数据类型

## 变量与常量定义

```
// 变量
<type> <value name>[= <init value>];
int i = 0;
int j;
int k, h;
```

```
// 使用 extern 进行变量或函数的声明，只是声明没有进行变量定义。可以在多个地方多次声明，但是只能定义一次。
extern <value or function name>;

extern int a, b;
extern void function();

int main() {
    int a, b;
    return 0;
}
void function() {
    ...
}
```

### 变量的作用域

* 在某个代码块中定义的变量：局部变量，系统不会自动初始化
* 函数参数的定义中声明的变量：形式参数
* 函数外部声明的变量：全局变量，系统会自动初始化

### 常量

```
#define <const value name> <const value>;
#define LENGHT 10;

const <type> <value name> = <value>;
const int LONG = 20;
```

## typedef 声明

```
typedef <old type name> <new type name>;
typedef int feet;
feet v; // == int v;
```

## 基本数据类型

* 基本数据类型
    * bool
    * char
    * int
    * float
    * double
    * void
    * wchar_t 宽字符型
* 数字类型的修饰符
    * signed
    * unsigned
    * short
    * long
* 变量限定符
    * const 不可被修改
    * volatile 表示该变量是随时可能被变化的，编译器不要对其做优化，并且每次读取都需要从内存读取
    * restrict 表明该内存具有唯一性
* 储存类
    * auto (C++11)
        * 声明变量时用于自动推断类型 auto value = 10; // int value = 10;
        * 声明泛型函数式返回值占位符
    * static 全局同享变量
    * extern 提供全局变量引用声明，函数声明
    * mutable
    * thread_local 只可以在创建的线程中访问，线程创建时创建，线程销毁时销毁

``` 
// 获取数字类型的大小

#include <iostream>
using namespace std;
 
int main()
{
   cout << "Size of char : " << sizeof(char) << endl;
   cout << "Size of int : " << sizeof(int) << endl;
   cout << "Size of short int : " << sizeof(short int) << endl;
   cout << "Size of long int : " << sizeof(long int) << endl;
   cout << "Size of float : " << sizeof(float) << endl;
   cout << "Size of double : " << sizeof(double) << endl;
   cout << "Size of wchar_t : " << sizeof(wchar_t) << endl;
   return 0;
}
```

## 枚举类型

```
enum <enum name> {
    <case name>[= const int value],
    <case name>[= const int value],
    ...
}[enum value];

enum EnumType {
    case case1, // 0
    case case2 = 3, // 3
    case case3, // 4
    case case4
};
EnumType value = case1;
```

# 运算符

## 算术运算符

```
+ - * / % ++ --
```

## 关系运算符

```
== != < <= > >= 
```

## 逻辑运算符

```
&& || !
```

## 位运算符

```
& 都为 1
| 其中一个为 1 
^ 两者不同
~ 补码
<< 左移
>> 右移

0011 & 1001 = 0001
0011 | 1001 = 1011
0011 ^ 1001 = 1010
~0011 = 1100
0011 << 1 = 0110
0011 >> 1 = 0001
```

## 赋值运算符

```
= += -= *= /= %= 
<<= >>= &= ^= |=
```

## 其他运算符

```
sizeof
<bool> ? <true> : <false>
,
. ->
Cast ()
&
*
```

## 优先级

# 判断

## if

```
if (<bool>) {
    ...
} else if (<bool>) {
    ...
} else {
    ...
}
```

## switch

```
// switch 语句中的 expression 必须是一个整型或枚举类型，或者是一个 class 类型，其中 class 有一个单一的转换函数将其转换为整型或枚举类型。
switch (<int>) {
    case <const int>: 
        ...; 
        break;
    default: 
        ...;
        break;
}
```



# 循环

## while

```
while <bool> {
    ...
}

do {
    ...
} while <bool>;
```

## for

```
for (<init>; <bool>; <step>) {
    ...
}

for (<type> &<name>: <array>) {

}

int array[5] = {0,1,2,3,4};
for (auto &x: array) {
}
for (int &x: array) {
}
```

## 循环跳出

```
break;
continue;

label: <label name>;
goto <label name>;
```

# 函数

```
// 函数声明
<return type> <function name>([<parameter list>...]);
// 函数定义
<return type> <function name>([<parameter list>...]) {
    ...
}
```

## 参数默认值

```
void function(int i = 10) {
}
function();
```

## lambda


