>LaTeX 语法知识
>
>在 NWeb 中需要开启 MathJax 才可查看
>NWeb -> `Preferences` -> `Themes` -> `Enable MathJax(LaTeX)`
>
>create: 201801140800 30
>complete: 201801141100 60
>

# 其他

## 格式

* `{}` 符号用于块划分
    * `\{\}` 才可显示 { }


## 如何插入公式

* 在行中插入公式

    `$数学公式$` 
    $a_n=10$

* 独立块公式
    
    `$$数学公式$$`
    $$a_n = 10$$

    
## 参考资料

[MathJax Chinese Doc 2.0 documentation](http://mathjax-chinese-doc.readthedocs.io/en/latest/start.html)
[360doc](http://www.360doc.com/content/14/0930/23/9482_413578190.shtml)

# 特殊格式

## 上下标


$a^n = a^{n+1}$
$a_n = a_{n+1}$

```
$a^n = a^{n+1}$
$a_n = a_{n+1}$
```

## 分数

$\frac{a}{b}$ or $a \over b$

```
$\frac{a}{b}$ or $a \over b$
```

## 开方

$\sqrt{2} = \sqrt[2]{2}$

```
$\sqrt{2} = \sqrt[2]{2}$
```

# 省略号

$0 \ldots 10 = 0 \cdots 10$

```
$0 \ldots 10 = 0 \cdots 10$
```

## 矢量

$\vec{a} + \vec{b}$

```
\vec{a} + \vec{b}
```

# 运算符

## 普通运算符

$+ , - , \times , \div , \pm$
$\bigodot , \bigotimes , \bigoplus$

```
+ , - , \times , \div , \pm
\bigodot , \bigotimes , \bigoplus
```

### 累加，累乘 运算符

$\sum , \prod , \coprod$

```
\sum , \prod , \coprod
```

## 关系运算符

$\leq , \geq , \neq , \approx , \equiv$
$\not= , \not>$
$\because , \therefore , \forall , \exists$

```
\leq , \geq , \neq , \approx , \equiv
$\not= , \not>$
$\because , \therefore , \forall , \exists$e
```

## 集合运算符

$\emptyset , \in , \notin , \subset , \supset , \not\subset , \not\supset , \subseteq , \supseteq$
$\bigcap , \bigcup , \bigvee , \bigwedge , \biguplus , \bigsqcup$

```
$\emptyset , \in , \notin , \subset , \supset , \not\subset , \not\supset , \subseteq , \supseteq$
$\bigcap , \bigcup , \bigvee , \bigwedge , \biguplus , \bigsqcup$
```

## 对数运算符

$\log , \lg , \ln$

```
\log , \lg , \ln
```

## 三角运算符

$\bot , \angle , 30^\circ$
$\sin , \cos , \tan , \cot , \sec , \csc$

```
$\bot , \angle , 30^\circ$
$\sin , \cos , \tan , \cot , \sec , \csc$
```

## 微积分运算符

$\prime , \int , \iint , \iiint , \iiiint$
$\oint , \lim , \infty , \nabla$

```
$\prime , \int , \iint , \iiint , \iiiint$
$\oint , \lim , \infty , \nabla$
```

# 特殊符号

## 未分类符号

$\mid , \nmid , \cdot , \circ , \ast$

## 箭头符号

$\uparrow , \downarrow , \Uparrow , \Downarrow$
$\rightarrow , \leftarrow , \Rightarrow , \Leftarrow$
$\longrightarrow, \longleftarrow$

```
$\uparrow , \downarrow , \Uparrow , \Downarrow$
$\rightarrow , \leftarrow , \Rightarrow , \Leftarrow$
$\longrightarrow, \longleftarrow$
```

## 盖帽符号

$\hat{y} , \check{y} , \breve{y}$

```
$\hat{y} , \check{y} , \breve{y}$
```

## 连线符号

$\overline{a+b+c}$

$\underline{a+b+c}$

$\overbrace{a+b+c}_{20.0}^{10.0}$

$\underbrace{a+b+c}_{20.0}^{10.0}$

$H(n) = \begin{cases} 0& \text{(n=0 时)} \\ H(n-1)+1+H(n-1)& \text{(n=1,2,3 \cdots 时)} \end{cases}$

```
$\overline{a+b+c}$

$\underline{a+b+c}$

$\overbrace{a+b+c}_{20.0}^{10.0}$

$\underbrace{a+b+c}_{20.0}^{10.0}$

$H(n) = \begin{cases} 0& \text{(n=0 时)} \\ H(n-1)+1+H(n-1)& \text{(n=1,2,3 \cdots 时)} \end{cases}$
$<first> = \begin{cases} <cases0>& \text{<cases0 text>} \\ <cases1>& \text{cases1 text} <...> \end{cases}}$

```

## 希腊字母

$\alpha , A , \beta , B , \gamma$ 
$\Gamma , \delta , \Delta , \epsilon , E$
$\varepsilon , \zeta , Z , \eta , H$
$\theta , \Theta , \vartheta , \iota , I$
$\kappa , K , \lambda , \Lambda , \mu$
$M , \nu , N , \xi , \Xi$
$o , O , \pi , \Pi , \varpi$
$\rho , P , \varrho , \sigma , \Sigma$
$\varsigma , \tau , T , \upsilon, \Upsilon$
$\phi , \Phi , \varphi , \chi, X$
$\psi , \Psi , \omega , \Omega$

```
$\alpha , A , \beta , B , \gamma$ 
$\Gamma , \delta , \Delta , \epsilon , E$
$\varepsilon , \zeta , Z , \eta , H$
$\theta , \Theta , \vartheta , \iota , I$
$\kappa , K , \lambda , \Lambda , \mu$
$M , \nu , N , \xi , \Xi$
$o , O , \pi , \Pi , \varpi$
$\rho , P , \varrho , \sigma , \Sigma$
$\varsigma , \tau , T , \upsilon, \Upsilon$
$\phi , \Phi , \varphi , \chi, X$
$\psi , \Psi , \omega , \Omega$
```


