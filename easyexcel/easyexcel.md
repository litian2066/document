# EaayExcel

## 一、初识EasyExcel

### 1. Apache POI

先说`POI`，有过报表导入导出经验的同学，应该听过或者使用过。

`Apache POI`是Apache软件基金会的开源函式库，提供跨平台的`Java API`实现`Microsoft Office`格式档案读写。但是存在如下一些问题：

#### 1.1 学习使用成本较高

对POI有过深入了解的才知道原来POI还有SAX模式（Dom解析模式）。但是SAX模式相对比较复杂，excel有03和07两种版本，两个版本数据存储方式截然不同，sax解析方式也各不一样。

想要了解清楚这两种解析方式，才去写代码测试，估计两天时间时需要的。再加上即使解析完，要转换到自己业务模型还要很多繁琐的代码。总体下来感觉至少需要三天，由于代码复杂，后续维护成本巨大。

POI的SAX模式的API可以一定程度的解决一些内存溢出的问题，但是POI还是有一些缺陷，比如07版Excel解压缩以及解压后存储都是在内存中完成的，内存消耗依然很大，一个3M的Excel用POI的SAX模式解析，依然需要100M左右的内存。

#### 1.2 POI的内存消耗较大

大部分使用POI都是使用它的userModel模式。userModel的好处是上手容易使用简单，随便拷贝跑一下，剩下就是写业务转换，虽然转换也要写上百行代码，相对比较好理解。然而userModel模式最大的问题是在于非常大的内存消耗，一个几兆文件解析要用掉几百兆的内存。现在好多应用采用这种模式，之所以还正常在跑一定是并发不大，并发上来后一定会OOM或者频繁的full GC。

总体上来说，简单写法重度依赖内存你，复杂写法学习成本高。

#### 特点

1. 功能强大
2. 代码书写冗余繁杂
3. 读写大文件耗费内存较大，容易OOM

## 2. `EasyExcel`

![image-20200412221505127](/Users/litian/Library/Application Support/typora-user-images/image-20200412221505127.png)

![image-20200412221819666](/Users/litian/Library/Application Support/typora-user-images/image-20200412221819666.png)

![image-20200412222510673](/Users/litian/Library/Application Support/typora-user-images/image-20200412222510673.png)

![image-20200412222818005](/Users/litian/Library/Application Support/typora-user-images/image-20200412222818005.png)

![image-20200412223013905](/Users/litian/Library/Application Support/typora-user-images/image-20200412223013905.png)

![image-20200412223205906](/Users/litian/Library/Application Support/typora-user-images/image-20200412223205906.png)

![image-20200412225433501](/Users/litian/Library/Application Support/typora-user-images/image-20200412225433501.png)