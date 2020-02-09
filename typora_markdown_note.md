

# typora简介与markdown基础语法回顾

自动生成目录语法  [toc]	 

[TOC]

# 1、typora：markdown 编写利器



typora号称是读写一体的markdown编写工具。确实好用啊！

三个特性：

- 无注意力分散
- 无缝衔接的实时展示
- What you see is what you mean

# 2、markdown笔记

## 2.1 image 

快捷键 command + ^ + i

静态图片

![mario](/Users/zhangyanan/Pictures/seeyou.jpg)

   

动态图片：

![Alt text](https://box.kancloud.cn/2015-07-16_55a776534461a.gif)







语法：

```
![GitHub set up](http://zh.mweb.im/asset/img/set-up-git.gif)
格式: ![Alt Text](url)
```



Q:如何调整图片大小和位置呢？

只能用<img>标签了

<img src="http://zh.mweb.im/asset/img/set-up-git.gif" width="200px">



<img src="http://zh.mweb.im/asset/img/set-up-git.gif" style = "height=200px">

制定大小比例：

<img src="http://zh.mweb.im/asset/img/set-up-git.gif" style="zoom:80%">

## 2.2 list

```
1. 项目一 有序列表 `数字 + . + 空格键`
2. 项目二 
3. 项目三
    1. 项目三的子项目一 有序列表 `TAB + 数字 + . + 空格键`
    2. 项目三的子项目二
```

无序列表：+、-、*

- list1(- 或 + 或 *)
  - list2	 (tab)
- List3 (shift + tab)

有序列表：1. 2. ...

1. 第一个
2. 第二个

Task List (任务列表)：

```java
- [] task 1 - + 空格 + [ ]
```



- [ ] 任务一
- [x] 任务二



## 2.3 link

本文link跳转(锚)

[markdown笔记](# 2、markdown笔记)

其他链接语法

```
email <example@example.com>
[GitHub](http://github.com)
自动生成连接  <http://www.github.com/>
```

email <example@example.com>
[GitHub](http://github.com) 文字的超链接
自动生成连接  <http://www.github.com/>

快捷键 command + K

## 2.4强调

```
*这些文字会生成`<em>`*
_这些文字会生成`<u>`_

**这些文字会生成`<strong>`**
__这些文字会生成`<strong>`__

~~删除线~~

水平分割线：
---
***

<u>下划线</u> markdown没有原生的下划线语法 快捷键command + u

高亮 shift + command +h
```

这是正常的

==高亮==

*斜体的强调*

_另一种斜体_

**加粗强调**

也可以**command+B**加粗

~~删除线~~

<u>下划线</u>





---

## 2.5注释

<!--这是注释-->

快捷键 ^+-

## 2.6块引用

> 块引用：这是一段引用

> “焚诗书，坑术士”  			——《史记》



## 2.7代码

~~~
​~~~代码块
shift + command + `代码行
~~~

~~~java
System.out.println("hello world!")
~~~

`code`



## 2.8table

```
table 语法
|Item|Qty|Price|| return
```



| Item | Qty  | Price |      |
| ---- | ---- | ----- | ---- |
|      |      |       |      |
|      |      |       |      |
| 👅    |      |       |      |

## 2.9脚注

~~~
这是一个脚注：[^sample_footnote]
~~~



这是一个脚注：[^1]



## 2.10数学

## 2.11顺序图和流程图

~~~sequence

~~~

~~~flow

~~~



# summary

多查看快捷键，多使用快捷键，会迅速掌握这套书写语法啦！





























