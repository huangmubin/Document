# 基础知识

## 快捷键

* [Tab] : 自动补全
* Ctrl+d : 键盘输入结束或退出终端
* Ctrl+s : 暂定当前程序，暂停后按下任意键恢复运行
* Ctrl+z : 将当前程序放到后台运行，恢复到前台为命令fg
* Ctrl+a : 将光标移至输入行头，相当于Home键
* Ctrl+e : 将光标移至输入行末，相当于End键
* Ctrl+k : 删除从光标所在位置到行末
* Alt+Backspace : 向前删除一个单词
* Shift+PgUp : 将终端显示向上滚动
* Shift+PgDn : 将终端显示向下滚动

## 通配符

通配符是一种特殊语句，主要有星号（*）和问号（?），用来对对字符串进行模糊匹配（比如文件名，参数名）。当查找文件夹时，可以使用它来代替一个或多个真正字符；当不知道真正字符或者懒得输入完整名字时，常常使用通配符代替一个或多个真正的字符。

* * : 匹配 0 或多个字符
* ? : 匹配任意一个字符
* [list] : 匹配 list 中的任意单一字符
* [!list] : 匹配 除list 中的任意单一字符以外的字符
* [c1-c2] : 匹配 c1-c2 中的任意单一字符 如：[0-9] [a-z]
* {string1,string2,...} : 匹配 sring1 或 string2 (或更多)其一字符串
* {c1..c2} : 匹配 c1-c2 中全部字符 如{1..10}

## man 手册

```
:$ man <command_name>
```

所有的手册页遵循一个常见的布局，其为通过简单的 ASCII 文本展示而优化，而这种情况下可能没有任何形式的高亮或字体控制。一般包括以下部分内容：

> NAME（名称）
> 该命令或函数的名称，接着是一行简介。

> SYNOPSIS（概要）
> 对于命令，正式的描述它如何运行，以及需要什么样的命令行参数。对于函数，介绍函数所需的参数，以及哪个头文件包含该函数的定义。

> DESCRIPTION（说明）
> 命令或函数功能的文本描述。

> EXAMPLES（示例）
> 常用的一些示例。

> SEE ALSO（参见）
> 相关命令或函数的列表。

也可能存在其他部分内容，但这些部分没有得到跨手册页的标准化。常见的例子包括：OPTIONS（选项），EXIT STATUS（退出状态），ENVIRONMENT（环境），BUGS（程序漏洞），FILES（文件），AUTHOR（作者），REPORTING BUGS（已知漏洞），HISTORY（历史）和COPYRIGHT（版权）。

通常 man 手册中的内容很多，你可能不太容易找到你想要的结果，不过幸运的是你可以在 man 中使用搜索，/<你要搜索的关键字>，查找到后你可以使用n键切换到下一个关键字所在处，shift+n为上一个关键字所在处。使用Space(空格键)翻页，Enter(回车键)向下滚动一行，或者使用j,k（vim编辑器的移动键）进行向前向后滚动一行。按下h键为显示使用帮助(因为man使用less作为阅读器，实为less工具的帮助)，按下q退出。

想要获得更详细的帮助，你还可以使用info命令，不过通常使用man就足够了。如果你知道某个命令的作用，只是想快速查看一些它的某个具体参数的作用，那么你可以使用--help参数，大部分命令都会带有这个参数，如：`:$ ls --help`

# 用户及文件权限管理

## 用户管理

```
$ sudo adduser <new_username> // 添加用户
$ su -l <username>            // 切换用户
$ exit                        // 退出当前用户
$ groups <username>           // 获取当前用户组信息
$ sudo deluser <username> --remove-home // 删除用户
```

### who

```
$ who am i     // 打印当前用户
$ who -a       // 打印能打印的全部
$ who -d       // 打印死掉的进程
$ who -m       // 同am i,mom likes
$ who -q       // 打印当前登录用户数及用户名
$ who -u       // 打印当前登录用户登录信息
$ who -r       // 打印运行等级
```

## 文件类型以及权限

```
> 文件详细信息输出解析
drwxr-xr-x    12     MyronOffice  staff      408      10 24 10:47  Blogs
文件类型和权限  链接数  所有者         所属用户组  文件大小  最后修改日期   文件名
```

* 文件类型和权限
    * 文件类型(d)
        * d  目录
        * l  软链接
        * b  块设备
        * c  字符设备
        * s  socket
        * p  管道
        * -  普通文件
   * 所有者权限(rwx) + 当前用户组权限(r-x) + 其他用户组权限(r-x)
        * r  read
        * w  write
        * x  运行

### chown chmod

```
$ sudo chown <new_username> <filename> // 变更文件所有者

文件权限变更
表示要更改哪个部分的权限
g : group
o : others
u : user
+ : 增加权限
- : 减少权限 

修改某个文件的权限，减少 group 跟 others 的读写权限
$ chmod go-rw <filename>
```

# 文件及文件夹操作

## ls 查看目录

```
$ ls    // 获取文件目录
$ ls -l // 获取文件详细信息
$ ls -a // 获取全部文件
$ ls -s // 获取文件大小
$ ls -S // 按文件大小排序
```

## cd 移动位置

```
$ cd <folder name> // 移动到某个文件夹
$ cd <full path>   // 移动到特定路径
$ cd ..            // 移动到上一个文件夹
```

## mkdir 创建文件夹

```
$ mkdir <folder name> // 创建某个文件夹
```

## touch 新建文件

```
$ touch <filename>
```

## vi 适用 vim 编辑文件

```
$ vi <file name> 打开当前目录的某个文件，如果不存在则创建
```

### vi 常用基本指令

```
:i  // 输入模式
:wq // 保存并退出
:q  // 退出但是不保存
```

## more 直接将文件内容在终端进行输出

```
$ more <file name> // 直接将文件内容在终端进行输出
```

## rm 删除文件

```
// 删除某个文件(文件夹无效)
   $ rm <file> 
// 强行删除某个文件夹以及其中的内容(-r 遍历 -f 不提示)
   $ rm -rf <file or folder> 
```

## scp 复制到远程服务器

```
// 将本地某个文件<file name>复制到服务<server address>上的某个路径<server file path>之下
   $ scp <file name> root@<server address>:<server file path>
// 复制文件夹
   $ scp -r <file name> root@<server address>:<server file path>
```

# 进程管理

## jobs 查看当前后台任务

```
$ jobs 
```

## ps -ef  查看所有后台进程

```
$ ps -ef 
```

## & 启动某个程序到后台

```
$ ./<program> &
$ nohup ./<program> &
```

#  远程服务器操作

## 登录 阿里云 服务器

```
$ ssh root@<address>
```

## 退出登录

```
$ exit
```

