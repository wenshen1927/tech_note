#《Java Core》第3章笔记



## 3.1 简单Java程序



3.3.4 Unicode和char类型建议程序中不要用char，最好用字符串。

3.4.1 变量初始化之后，必须对其显示初始化后再调用，否则报错

3.4.2 常量

常量是被final修饰的变量，只能被赋值一次，且不能再更改。

类常量：被 static final 修饰的变量，通常希望常量被类中多个方法共享，或者被public修饰，可以被其他类共享。

注：const是保留关键字，目前没有用

变量的明明规范：

3.5 运算符：注意/ 

整数/0会抛异常，而浮点数/0 会产生Double.INFINITY 或NaN，不会抛异常。

3.5.1 数学函数

注意floorMod的用法

3.5.2 数值类型转换 

如图所示，自动类型转换：6个实箭头无精度损失，3个虚箭头有精度损失(为什么？)

<img src="/Users/zhangyanan/Library/Application Support/typora-user-images/image-20190628144143369.png" style="width:500px">

3.5.3 强制类型转换

可能存在精度损失。如 double x = 9.99 ; int y = (int) x;此时x = 9；也就是去除了小数后面的位数。

如果需要四舍五入，用Math.round(x) =

3.5.7 位运算符

& (and)  

| (or) 

 ^ (xor) ~ (not)

掩码技术：

```
int n = 24;
System.out.println(Integer.toBinaryString(n));
int forthBitFromRight = (n & 0b1000)/ 0b1000 ;
System.out.println(forthBitFromRight);
```

移位运算：

\<<左移

\>>右移：用符号位填充高位

\>>>右移：用0来填充高位

3.5.8 运算符优先级

关注优先级和结核性

3.5.9 枚举类型

枚举类型和枚举类的写法



3.6.4 检测字符串相等

务必用.equals()，绝不可以用==。

```java
String greet = "Hello";
String g1 = "Hello";
System.out.println(greet == g1);//true
```

3.6.5 空串与Null串

若判断一个字符串既不为空，也不为null，应该先判断null，再判断是否为空。

```java
if(str != null && str.length() != 0)
```

3.6.6 码点与代码单元

- Char： 在java中是采用UTF-16编码的，也就是说，Char是代表一个字符单元。
- 代码单元：UTF-8中是用8个字节（byte）表示的，UTF-16中使用16个字节表示的等等。
- 代码点：对应各种真正字符（char不是真正的字符，是代码单元）的Unicode编码。

一个代码点可能对应一对代码单元，如辅助字符，但是大多数是一个代码点对应一个字符。

也正是因为以上原因，在Java中，不赞成使用Char类型，因为它并不能代表一个真正的字符，而只是代码单元，而操作中，我们往往想得到的是真正的字符（码点），而不是代码单元char。

当然，一般我们很少遇到辅助字符（由两个代码单元组成），但还是有必要了解一下。