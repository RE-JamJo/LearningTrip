# java简介

2009年被oracle收购之前，将jdk源代码开源，形成了openjdk，但是，在sun开源jdk源代码的时候，其中有一部分源代码（小部分非核心功能），因为产权问题，无法开源，就被其他有同样功能的开源代码取代。

关于openjdk和jdk源代码是有关系的：包含在openjdk源代码中的绝大部分代码和oreclejdk一模一样。Jdk可以理解为openjdk的一个分支：不仅两者的代码是相同的，而且，oraclejdk还会和openjdk保持同步。同时，一旦oraclejdk发现openjdk中的一些bug，oracle在修复之后，把这些修复bug的代码同步到openjdk。

## 使用jdk8学习

- 国内绝大部分公司，使用的jdk版本仍然是jdk8
- Why？商业公司求稳，从jdk9开始每半年发布一次，分长期支持版本(至少3年)和短期支持版本(半年)
LTS：long term support长期支持版本
学习优先级：Jdk8->jdk11->jdk17

## Java语言平台版本

- JAVASE（Java platform standard edition）标准版。为开发普通桌面和商务应用程序提供的解决方案。
- JAVAME（Java platform to micro edition）小型版。为开发电子消费产品和嵌入式设备提供的解决方案。
- JAVAEE（Java platform to enterprise edition）企业版。为开发企业环境下的应用程序提供的一套解决方案。

## Java语言特点

- 跨平台
  - 通过Java语言编写的应用程序在不同的系统平台上都可以运行。Java程序是在Java虚拟机上运行，而非直接运行于操作系统。不同系统的jvm不一样，所有的jvm都能运行Java语言，所以jvm不是跨平台。

- 面向对象-解释型
- 健壮-动态
- 分布式-高效
- 多线程-结构中立（字节码）
- 开源

## JDK和JRE

- JRE（Java runtime environment）包括Java虚拟机，运行时核心类库(rt.jar)，JRE主要是给已经写好的Java程序使用，换句话说Java程序能在操作系统中运行，必须有JRE。
- JDK（Java develop kit）包含JRE，除此之外，JDK中海包含一些供开发者使用的工具，比如javac、javap等，仅仅只供开发者在开发阶段使用的工具。

## Java程序运行原理

- .java文件经javac编译得到.class字节码文件再经java运行在内存中看到结果。
