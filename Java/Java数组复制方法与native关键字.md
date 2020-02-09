
数组复制有几个方法：

1、for循环逐一复制：思路清楚但是代码不简洁

2、System.arraycopy()；这是效率最高的数组复制方式。
观察System.arraycopy()源码：
可以看到是native方法：native关键字说明其修饰的方法是一个原生态方法，方法对应的实现不是在当前文件，而是在用其他语言（如C和C++）实现的文件中。 可以将native方法比作Java程序同Ｃ程序的接口。

3、Arrays.copyOf():效率比System.arraycopy要差一点，因为它源码本质上也是调用System.arraycopy。

4.clone()方法，返回的是Object[]，需要强制转换。 一般用clone效率是最差的，

都没有做过实验，待验证。
