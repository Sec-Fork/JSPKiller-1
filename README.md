# JSPKiller

![](https://img.shields.io/badge/build-passing-brightgreen)
![](https://img.shields.io/badge/ASM-9.2-blue)
![](https://img.shields.io/badge/Java-8-red)

## 简介

一个JSP Webshell检测工具

主要是基于污点分析来做，依靠ASM解析字节码，然后模拟栈帧在JVM指令执行中的变化实现数据流分析

具体的原理参考先知社区文章：https://xz.aliyun.com/t/10622

## Quick Start

目前支持以下两种检测，其他方式后续更新

1. 反射构造`Runtime.exec`的`Webshell`
2. 使用`BCEL ClassLoader`加载恶意字节码的`Webshell`（非反射方式）

命令：

`java -jar JSPKiller.jar -f 1.jsp -m rb`

- 使用-f参数指定检测`JSP`文件
- 使用-m参数指定检测模块：r表示反射型；b表示BCEL型（可多选）

提供了检测案例
- `jsp/test-1.jsp`-`jsp/test-4.jsp`用于测试反射马
- `jsp/bcel-1.jsp`-`jsp/bcel-4.jsp`用于测试BCEL马

如果发生空指针异常或编译报错，参考以下

注意：
1. `JSPKiller.jar`目录下必须有`lib.jar`文件
2. 测试的三种反射JSP马已经提供（在JSP目录下）
3. 确保配置了正确的环境变量`JAVA_HOME`
4. 确保`java`命令是`JDK`下的而不是`JRE`下的（例如环境变量`Path`中配置`C:\Program Files\Java\jdk1.8.0_131\bin`为第一个）这样做的原因是：在`JRE`环境中无法获得编译器对象（JavaCompiler）来进行动态编译，只有`JDK`有这样的功能

## 效果

![](/img/1.png)