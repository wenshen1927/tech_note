# Java编程思想--笔记

## 第1章 对象导论 & 第2章 一切都是对象

### 1、基本数据类型

- | 基本类型 | 大小            | 最小值    | 最大值         | 包装器类型 | 默认值 |
  | -------- | --------------- | --------- | -------------- | ---------- | ------ |
  | boolean  | -               | -         | -              | Boolean    | false  |
  | char     | 16-bit (2-byte) | Unicode 0 | Unicode 2^16-1 | Character  | 0      |
  | byte     | 8-bit           | -128      | +127           | Byte       | 0      |
  | short    | 16-bit(2-byte)  | -2^15     | +2^15 -1       | Short      | 0      |
  | int      | 32-bit(4-byte)  | -2^31     | +2^31-1        | Integer    | 0      |
  | long     | 64-bit          | -2^63     | +2^62-1        | Long       | 0L     |
  | fload    | 32-bit          | IEEE754   | IEEE754        | Float      | 0.0f   |
  | double   | 64-bit          | IEEE754   | IEEE754        | Double     | 0.0d   |
  | void     | -               | -         | -              | Void       |        |

引用数据类型，默认初始化为null

### 2、static关键字

- **static修饰的变量和方法称为类变量和类方法。**
- **类变量只有一份存储空间**。不需要类创建任何对象就可调用类变量和类方法。
- **static方法内不能调用非static的方法**



## 第5章 初始化与清理

> ​	忘记初始化变量和忘记内存清理是经常导致程序不安全的两个问题。因此我们要了解java的初始化机制和垃圾回收机制。

### 5.1 使用构造器初始化

- Java通过构造器来确保对象的实例化
  - 构造器名称与类名相同；
  - 调用构造器是编译器的责任
    - 创建对象时：new Rock()
    - 会为对象分配存储空间，并调用相应的构造器
  - Java提供一个无参数的默认构造器
- **初始化和创建**是捆绑在一起的

### 5.2 方法的重载

- 重载提供了语言中的"冗余"

- 区分重载：**每个重载的方法有独一无二的参数类型列表**

  - 注：参数顺序不同也可以区分两个重载的方法，但是不要这样做，会使代码难以维护
  - **不可以根据返回值来判断重载**(如下面，我只想调用方法，不关心返回值的时候，编译器不知道调用哪个方法)

- ```java
  public class ReturnValue {
      void f(){}
      int f(){}
      public static void main(String[] args) {
          f();
      }
  }
  ```



### 5.3 默认构造器

- 若没有声明构造器，编译器会给你创建一个默认的构造器

### 5.4 this关键字

- **this关键字只能在方法内部使用，表示对"调用方法的那个对象"的引用**
- 如果在方法内部调用同一个类的另一个方法，不必使用this(在静态方法里也可以吗?不可以！）
- static的方法就是没有this的方法，所以不能用this调用方法

### 5.5 清理：终结处理和垃圾回收

- 这块还是找本Java虚拟机的书看一下，这里讲的不清楚

### 5.6 & 5.7 变量初始化和构造器初始化

- 初始化顺序
  1. **static的成员变量（包括静态块）会在类（.class文件）第一次被访问时创建与初始化(先静态，后非静态)**
  2. **成员变量初始化（包括非静态块）：在堆上为该类的对象分配走狗的空间，这块存储空间会被清零，也就是将成员变量设置为默认值(成员变量初始化先于构造器调用)**
  3. **执行构造器**

```java
class Insect {
    private int i = 9;
    protected int j;

    Insect() {
        System.out.println(" i = " + i + " j = " + j);
        j = 39;
    }

    private static int x1 = printInit("static Insect.x1 initialized");

    static int printInit(String s) {
        System.out.println(s);
        return 47;
    }
}

public class Beetle extends Insect {
    private int k = printInit("Beetle.k initialized");

    public Beetle() {
        System.out.println(" k = " + k);
        System.out.println(" j = " + j);
    }

    private static int x2 = printInit("static Beetle.x2 initialized");

    public static void main(String[] args) {
        System.out.println("Beetle constructor");
        Beetle beetle = new Beetle();
    }
}
```

### 5.9 可变参数列表

- 可变参数列表在方法内会变成数组



## 第6章 访问权限控制

- Java访问权限修饰词
  - public：所有人均可访问带有public关键字的类中的成员方法及对象
  - 默认包：只有在同一包下的类才能访问
  - private：除了包含该成员的类之外，其他任何类都无法访问。
  - protected：继承访问权限
    - 1.继承过程中，父类的成员若为protected时，子类继承下来的成员访问权限必须为protected或者public。
    - 2.protected提供包的访问权限，同包下的其他类可以访问protected元素。



- 访问权限范围：public>protected>默认包>private；
  因为protected关键字在继承中的特性，使得包外某一个类继承包内的类时，仍然可以访问该包内的类，故protected>默认包
- 类的访问权限
  - 访问权限同样可以作用于类。每一个编译单元必须有一个public类，且该类的类名必须与编译单元的文件名完全一致（区分大小写）。
  - 类的访问权限只有两个：public与默认包
    