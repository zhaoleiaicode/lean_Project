
# 一、Java8 新特性概览

Oracle 于 2014 发布了 Java8（jdk1.8），诸多原因使它成为目前市场上使用最多的 jdk 版本。

**java8新增的主要特性列表如下：**

## 1、函数式编程(lambda表达式)

> **面向对象编程是对数据进行抽象；函数式编程是对行为进行抽象。**

- Lambda 表达式的特点。
- Lambda 表达式使用和Stream下的接口。
- 函数接口定义和使用，四大内置函数接口Consumer，Function，Supplier, Predicate。
- Comparator排序为例贯穿所有知识点。

**lambda表达式详解:**

### (1) 什么是lambda？

我们知道，对于一个Java变量，我们可以赋给其一个**“值”**。
![](https://github.com/zlrobot-start/lean_Project/blob/main/z_jdk/images/jdk8/001.drawio.png)
如果你想把**“一块代码”**赋给一个Java变量，应该怎么做呢？

比如，我想把右边那块代码，赋给一个叫做aBlockOfCode的Java变量：

![](/home/10313969@zte.intra/Desktop/JDK新特性/JDK-Images/002.drawio.png)

在Java 8之前，这个是做不到的。但Java 8问世之后，利用Lambda特性，就可以做到了。

![](/home/10313969@zte.intra/Desktop/JDK新特性/JDK-Images/003.drawio.png)

当然，这个并不是一个很简洁的写法。所以，为了使这个赋值操作更加elegant, 我们可以移除一些没用的声明。

![](/home/10313969@zte.intra/Desktop/JDK新特性/JDK-Images/004.drawio.png)

这样，我们就成功的非常优雅的把“一块代码”赋给了一个变量。**而“这块代码”，或者说“这个被赋给一个变量的函数”，就是一个[Lambda表达式](https://zhida.zhihu.com/search?content_id=88998507&content_type=Answer&match_order=1&q=Lambda表达式&zhida_source=entity)**。

**但是这里仍然有一个问题，就是变量aBlockOfCode的类型应该是什么？**

**所有的Lambda的类型都是一个接口，而Lambda表达式本身，也就是”那段代码“，需要是这个接口的实现。**这是我认为理解Lambda的一个关键所在，简而言之就是，**Lambda表达式本身就是一个接口的实现**。直接这样说可能还是有点让人困扰，我们继续看看例子。我们给上面的aBlockOfCode加上一个类型：

![](/home/10313969@zte.intra/Desktop/JDK新特性/JDK-Images/005.drawio.png)

这种只有**一个接口函数需要被实现的接口类型，我们叫它”[函数式接口](https://zhida.zhihu.com/search?content_id=88998507&content_type=Answer&match_order=1&q=函数式接口&zhida_source=entity)“。**为了避免后来的人在这个接口中增加接口函数导致其有多个接口函数需要被实现，变成"非函数接口”，我们可以在这个上面加上一个声明@FunctionalInterface, 这样别人就无法在里面添加新的接口函数了：

![](/home/10313969@zte.intra/Desktop/JDK新特性/JDK-Images/006.drawio.png)

这样，我们就得到了一个完整的Lambda表达式声明：

![](/home/10313969@zte.intra/Desktop/JDK新特性/JDK-Images/007.drawio.png)



### (2) lambda表达式的作用？



# 二、Java 17 新特性概览

Java 17 在 2021 年 9 月 14 日正式发布，是一个长期支持（LTS）版本。下面这张图是 Oracle 官方给出的 Oracle JDK 支持的时间线。可以看得到，Java17 最多可以支持到 2029 年 9 月份。

![img](https://oss.javaguide.cn/github/javaguide/java/new-features/4c1611fad59449edbbd6e233690e9fa7.png)

Java 17 将是继 Java 8 以来最重要的长期支持（LTS）版本，是 Java 社区八年努力的成果。Spring 6.x 和 Spring Boot 3.x 最低支持的就是 Java 17。

**这次更新共带来 14 个新特性**：
