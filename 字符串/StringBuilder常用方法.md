 

> **在写算法题时，我们会常常用到StringBuilder这个类，下面我在这里一次性总结这个类的常用方法~方便回顾复习 其中包括了 `增 、 删 、查 、改、 反转`等操作**  
> 要是觉得有帮助，不妨给我来个一键三连哦~❤️
> 
> * * *
> 
> 🍡其 他 系 列 文 章🍡  
> 🚀🚀🚀  
> 🍕 [✨**JavaWeb学习笔记01**](https://blog.csdn.net/weixin_61263533/article/details/128473650?spm=1001.2014.3001.5501) `BS架构 Maven Tomcat Servlet`
> 
> 🍔 [✨**JavaWeb学习笔记02**](https://blog.csdn.net/weixin_61263533/article/details/128539516?spm=1001.2014.3001.5501) `request和response`
> 
> 🍟 [✨**JavaWeb学习笔记03**](https://blog.csdn.net/weixin_61263533/article/details/128539488?spm=1001.2014.3001.5501) `JSP MVC`  
> 🌭 [✨**JavaWeb学习笔记04**](https://blog.csdn.net/weixin_61263533/article/details/128593152?spm=1001.2014.3001.5501) **`待完善`**

### 文章目录

- [一、StringBuilder和String的转换](#一stringbuilder和string的转换)
- [二、StringBuilder的常用方法](#二stringbuilder的常用方法)
  - [1.字符串拼接 append()](#1字符串拼接-append)
  - [2.指定位置删除 delete(int a,int b)](#2指定位置删除-deleteint-aint-b)
  - [3.查找字符串 indexOf(String str)](#3查找字符串-indexofstring-str)
  - [4.改（替换字符串） replace(int i,int j,String str)](#4改替换字符串-replaceint-iint-jstring-str)
  - [5.插入数据 insert(int i,String str)](#5插入数据-insertint-istring-str)
  - [6.字符串反转 reverse](#6字符串反转-reverse)
  - [7.获取字符 charAt(int i)](#7获取字符-charatint-i)
  - [8.获取字符串 substring](#8获取字符串-substring)
- [总结](#总结)

* * *

* * *

一、StringBuilder和String的转换
=========================

String转StringBuilder

    String a = new String("123");
    StringBuilder s = new StringBuilder(a);
    

StringBuilder转String

    String s2 = s.toString(s);
    

二、StringBuilder的常用方法
====================

1.字符串拼接 append()
----------------

代码如下：

    StringBuilder s = new StringBuilder("hzy ");
    //直接调用append();
    s.append("aaa ");
    //也可以如下拼接
    s.append("bbb ").append("ccc ");
    
    System.out.println(s);
    

输出结果如下

    hzy aaa bbb ccc 
    

2.指定位置删除 delete(int a,int b)
----------------------------

（1）删除字符串  
代码如下：

    StringBuilder s = new StringBuilder("0123456789");
    		s.delete(0,3);//从0位置开始，到3结束（左闭右开，不包括3）
    		System.out.println(s);
    

输出结果如下

    3456789
    

（2）删除对应位置数据 deleteCharAt(index)  
代码如下：

    StringBuilder s = new StringBuilder("0123456789");
    		s.deleteCharAt(3);
    		System.out.println(s);
    

输出结果如下

    012456789
    

* * *

3.查找字符串 indexOf(String str)
---------------------------

PS:_**注意函数里面参数必须是String类型，Stringbuilder的都不行**_  
(1)

int indexOf(String str)，输出第一个匹配的索引。  
int indexOf(String str, int fromIndex)，从指定的索引处开始，输出第一个匹配的索引。  
(若找不到则输出-1)  
代码如下：

    StringBuilder s = new StringBuilder("0123456789");
    		int t1 = s.indexOf("789");//找789，返回索引
    		int t2 = s.indexOf("777");
    		System.out.println(t1);
    		System.out.println(t2);
    

输出结果如下

    7
    -1
    

(2)  
int lastIndexOf(String str)，输出最后一个匹配的索引。  
int lastIndexOf(String str, int fromIndex)，从指定的索引处开始，输出最后一个匹配的索引。  
(若找不到则输出-1)  
代码如下：

    StringBuilder s = new StringBuilder("aabbbbaa");
    		int t1 = s.lastIndexOf("aa");//从后往前找
    		System.out.println(t1);
    

输出结果如下

    6
    

* * *

4.改（替换字符串） replace(int i,int j,String str)
------------------------------------------

代码如下：

    		StringBuilder s = new StringBuilder("0123456789");
    		s.replace(3, 5, "aaaaa");
    		System.out.println(s);
    

输出结果如下

    012aaaaa56789
    

* * *

5.插入数据 insert(int i,String str)
-------------------------------

代码如下：

    StringBuilder s = new StringBuilder("0123456789");
    		s.insert(5, "aaaaa");
    		System.out.println(s);
    

输出结果如下

    01234aaaaa56789
    

* * *

6.字符串反转 reverse
---------------

代码如下：

    StringBuilder s = new StringBuilder("0123456789");
    		s.reverse();
    		System.out.println(s);
    

输出结果如下

    9876543210
    

* * *

7.获取字符 charAt(int i)
--------------------

代码如下：

    StringBuilder s = new StringBuilder("0123456789");
    		System.out.println(s.charAt(3));
    

输出结果如下

    3
    

* * *

8.获取字符串 substring
-----------------

(1)从某个位置开始到最后  
(2)从某个位置开始到某个位置结束  
代码如下：

    StringBuilder s = new StringBuilder("0123456789");
    		System.out.println(s.substring(5));
    		System.out.println(s.substring(5,8));
    

输出结果如下

    56789
    567
    

* * *

[点击返回顶部](#aaa)

总结
==

为什么要用StringBuilder进行字符串操作而不是String呢，因为StringBuilder的修改会比String节省不少内存空间  
以上就是StringBuilder的一些常用的方法，未完待更新