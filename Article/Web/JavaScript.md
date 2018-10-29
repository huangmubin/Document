# 基础语法

> 在文件头添加 'use strict' 变成严格模式

```
// 弹出提示框
alert('yo.');

// 输出命令行
console.log('yo.');
```

```
// 查看变量类型
let bag = 'Yo.';
bag = 1;
bag = true;
bag = {};
bag = [];
console.log(typeof bag);
```

## 变量

* var 的作用域是所有地方。
* let 的作用于只在于所存在的块中。

```
var name = value;
let name = value;
```

## 注释

```
// 注释内容

/*
注释内容
*/
```

## 数据类型

```
// Number 数字类型
1. 整型
2. 浮点数
3. 负数
4. NaN // Not a Number
5. Infinity // 无限大
6. 科学计数法 // 1e4 = 10000
```

```
// String 字符串类型
1. '单引号字符串';
2. "双引号字符串";
3. "Double dote's single dote."
4. "转译符号\"内容"
5. `内容`
```

```
// Boolean 布尔值
1. true
2. false
```

```
// Array 数组
1. ['a', "b", 1, 2, true, {a: b}]
2. 可以放多个类型
```

```
// Object 对象
var result = {
    key: value,
};
result.key = value;
```

## 运算符

```
+       -       *       /       %
+=      -=      *=      /=      %=
```

```
>       <       >=      <=      
```

```
==      !=      ===     !==     &&      ||
```

# 控制流

## if 

> false / 0 / '' / NaN / null / undefined 都会被认为是 false

```
var value = true;
if (value) {
    ...
} else if (value) {
    ...
} else {
    ...
}
```

## switch

```
var value = 6;
switch (value) {
    case 0, 6:
        console.log("A");
        break;
    case 1:
        console.log("B");
        break;
    case 2:
        console.log("C");
        break;
    case 3:
        console.log("D");
        break;
    default:
        console.log("E");
        break;
}
```

## for

```
for (let value = 1; value < 10; value = value + 1) {
    console.log(value)
}

var array = [1,2,3,4,5];
for (let i = 0; i < array.length; i++) {
    console.log(array[i]);
}
```

## while 

```
let value = 0;
while (value < 10) {
    console.log(value);
    value += 1;
}

do {
    console.log(value);
    value -= 1;
} while (value > 0);
```

# 函数

```
function name0() {
    console.log("普通函数");
}

function name1(value) {
    console.log(value);
    console.log("带参数的函数");
}

function name2() {
    return "带返回值的函数"
}

function name3() {
    let array = Array.prototype.slice.call(arguments);
    for (let i = 0; i < array.length; i++) {
        console.log("动态传参：" + array[i]);
    }
}


function f() {
    value = 10;
}

console.log(value);

;(function () {
    console.log("匿名函数，不会有作用域污染问题。");
})();
```

## 闭包

# Window 对象

```
alert("弹出提示框");

let value = confirm("弹出选择取消框");
console.log(value);

let value = prompt("弹出一个输入框用于输入。");
console.log(value);
```

# this



