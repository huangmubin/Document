# Java Web 学习笔记

Web 应用程序：提供浏览器访问的程序，即 Web 应用。一个 Web 应用由多个静态 web 资源组成，包括 html, css, js, Jsp, java 程序，jar 包，配置文件等等。

Tomcat 是一种 Web 服务器。

# 0. Mac 上的 Tomcat 安装

1. 下载 Tomcat， http://tomcat.apache.org/download-70.cgi , 下载 zip(pgp, md5)
2. 解压后将文件夹放置到任意目录，如 /usr/local/
3. 在终端中添加运行权限 $ cd /usr/local/apache-tomcat/bin; sudo chmod 755 *.sh
4. 运行启动脚本 $ ./startup.sh
5. 能打开 http://localhost:8080/ 即为成功。

# 1. Tomcat 服务器配置

Tomcat 的所有配置都放在 ~/conf 文件夹中，server.xml 是配置的核心文件。

## 1.1 端口配置

默认 8080 端口，但是可以自行更改，更改之后需要重启服务器。重启后，访问服务器需要用新的端口地址。

```
<Connector port="8080" protocol="HTTP/1.1"
        connectionTimeout="20000"
        redirectPort="8443" />
```

## 1.2 虚拟目录映射路径

即 `http://localhost:8080/` 所对应的文件夹目录

### 1.2.1 在 server.xml 文件的 host 元素中配置路径

```
<Host name="localhost"  appBase="webapps"
      unpackWARs="true" autoDeploy="true">

  <!-- SingleSignOn valve, share authentication between web applications
       Documentation at: /docs/config/valve.html -->
  <!--
  <Valve className="org.apache.catalina.authenticator.SingleSignOn" />
  -->

  <!-- Access log processes all example.
       Documentation at: /docs/config/valve.html
       Note: The pattern used is equivalent to using pattern="common" -->
  <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
         prefix="localhost_access_log." suffix=".txt"
         pattern="%h %l %u %t &quot;%r&quot; %s %b" />

  <!-- 
  新添加的映射路径
  path 是访问路径，如这里，访问这个文件夹的路径就是 http://localhost:8080/JavaWebApp
  docBase 是该文件夹在硬盘上的路径。
  -->

  <Context path="/JavaWebApp" docBase="/Users/myron/Downloads/Javaweb_app"

</Host>
```

### 1.2.2 自动映射

将 web 应用放在 `~/tomcat/webapps` 目录之下。

### 1.2.3 虚拟目录映射

在 `~/tomcat/conf/Catalina/localhost` 下添加文件 `<路径名称>.xml`，并在该文件中添加路径映射 `<Context docBase="<真实路径>">`

比如 `a.xml` 的访问路径就是 `http://localhost:8080/a/~`

## 1.3 虚拟主机配置

# 2. JavaWeb 应用的组成结构

```
JavaWebApp (根目录：html, jsp, css, js, 等外界可以直接访问的文件)
    /WEB-INF (配置文件目录，外界无法直接访问)
        /classes (Java 类目录)
        /lib (Java 类运行所需要的 jar 包)
        /web.xml (web 应用的配置文件，必须要有，内容有格式要求。)
```

* web.xml 标准格式

```
<?xml version="1.0" encoding="ISO-8859-1"?>

<web-app xmlns="http://java.sun.com/xml/ns/javaee"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
                      http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
  version="3.0"
  metadata-complete="true">

  <display-name>Welcome to Tomcat</display-name>
  <description>
     Welcome to Tomcat
  </description>

</web-app>
```


## 2.1 打包 JavaWeb 应用

> 在 Java 中，使用 jar 命令来将 JavaWeb 应用打包成为一个 war 包。
> 例如将 JavaWebDemo 打包，则是：
> $: jar -cvf JavaWebDemo.war JavaWebDemo
> 打包好的 JavaWebDemo.war 只需要放置在 ~/Tomcat/webapps 目录下，即可自动解压访问。

```
huangmubindeMacBook-Pro:~ myron$ jar
用法: jar {ctxui}[vfmn0PMe] [jar-file] [manifest-file] [entry-point] [-C dir] files ...
选项:
    -c  创建新档案
    -t  列出档案目录
    -x  从档案中提取指定的 (或所有) 文件
    -u  更新现有档案
    -v  在标准输出中生成详细输出
    -f  指定档案文件名
    -m  包含指定清单文件中的清单信息
    -n  创建新档案后执行 Pack200 规范化
    -e  为捆绑到可执行 jar 文件的独立应用程序
        指定应用程序入口点
    -0  仅存储; 不使用任何 ZIP 压缩
    -P  保留文件名中的前导 '/' (绝对路径) 和 ".." (父目录) 组件
    -M  不创建条目的清单文件
    -i  为指定的 jar 文件生成索引信息
    -C  更改为指定的目录并包含以下文件
如果任何文件为目录, 则对其进行递归处理。
清单文件名, 档案文件名和入口点名称的指定顺序
与 'm', 'f' 和 'e' 标记的指定顺序相同。

示例 1: 将两个类文件归档到一个名为 classes.jar 的档案中: 
       jar cvf classes.jar Foo.class Bar.class 
示例 2: 使用现有的清单文件 'mymanifest' 并
           将 foo/ 目录中的所有文件归档到 'classes.jar' 中: 
       jar cvfm classes.jar mymanifest -C foo/ .
```

## 2.2 手动构建最基础的 JavaWeb app

> javaWebApp 为该应用名称
> 访问路径为 localhost:8080/javaWebApp/Work1/

```
$ cd ~/tomcat/webapps
$ mkdir javaWebApp
$ cd javaWebApp
$ mkdir WEB-INF
$ cd WEB-INF
$ mkdir classes
$ vi web.xml

<?xml version="1.0" encoding="ISO-8859-1"?>

<web-app xmlns="http://java.sun.com/xml/ns/javaee"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
                      http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
  version="3.0"
  metadata-complete="true">

  <servlet>
    <servlet-name>Work1</servlet-name>
    <servlet-class>com.myron.Work1</servlet-class>
  </servlet>

  <servlet-mapping>
    <servlet-name>Work1</servlet-name>
    <url-pattern>/Work1</url-pattern>
  </servlet-mapping>
  
</web-app>
// :wq

$ cd classes
$ vi Work1.java

package com.myron;

import java.io.*;
import javax.servlet.*;

public class Work1 extends GenericServlet {

	public void service(ServletRequest req, ServletResponse res)
		throws ServletException, java.io.IOException 
	{
		OutputStream out = res.getOutputStream();
		out.write("hello servlet!!!".getBytes());
	}

}
// :wq

$ javac -cp ../../../../lib/servlet.jar -d . Work1.java
```

# 3. 加密

## 3.1 对称加密

加密跟解密都使用同一个秘钥。常用的有 DES, IDEA, RC2, RC4, SKIPJACK, RC5, AES 等。

## 3.2 非对称加密

利用私有秘钥(private key)进行加密，利用公开秘钥(public key)进行解密。

# 4. https 连接器

浏览器与服务器交互


