# 泛型	

## 为什么需要泛型

**1、减少人工类型转换的次数**

**2、编译期检查，加强[类型安全](https://zh.wikipedia.org/wiki/类型安全)**

**3、解耦类和方法与所使用的类型之间的关系，让类或方法更通用一点**

例子1：

```java
public static void main(String[] args) {        
    // 在一个容器里，我们可以放不同类型的数据，但是如果我们想规定这个容器只能存某一种类型的对象，却没有办法        
    List list1 =new ArrayList();        
    list1.add(1);        
    list1.add("a");        
    list1.add(1.2);        
    System.out.println(list1);        
    // 如上面的list1，可以存入多种数据类型。但是我们在取出的时候，想要知道集合元素的确切类型，却很麻烦。        
    for (int i = 0; i < list1.size(); i++) {            
        Object obj = list1.get(i);            
        if (obj instanceof Integer){                
            System.out.println(obj + " : Integer");            
        }else if (obj instanceof String){                
            System.out.println(obj + " : String");            
        }else if (obj instanceof Double){                
            System.out.println(obj + " : Double");            
        }        
    }        
    // 泛型就是在编译期加入对类型参数的检查        
    List<String> list2 = new ArrayList<>();
    // list2.add(1); // 编译错误        
    list2.add("String"); 
  	List<Integer> list3 = new ArrayList<>();
  	list3.add(1);
}
```

例子2：

```java
public class ArrayList {
    private Object[] array;
    public void add(Object e){}
    public void remove(int index){}
    public Object get(int index){}
}
class StringArrayList {
    String[] array;
    public void add(String e){}
    public void remove(int index){}
    public String get(int index){}
}
```

```java
public class TestArrayList {
    public static void main(String[] args) {
        ArrayList list = new ArrayList();
        list.add("Hello");
        String o = (String)list.get(0);
        list.add(new Integer(122));
        // 编译期不会报错，运行期会报错：ClassCastException
        String o1 =(String) list.get(1);
      	// 在没有泛型的时候，如果希望list.get()不用转型，那就必须用StringArrayList
    }
}
```

## 什么是泛型

> **泛型程序设计**（generic programming）是[程序设计语言](https://zh.wikipedia.org/wiki/程序设计语言)的一种风格或[范式](https://zh.wikipedia.org/wiki/编程范型)。泛型允许程序员在[强类型程序设计语言](https://zh.wikipedia.org/wiki/強類型程式語言)中编写代码时使用一些以后才指定的[类型](https://zh.wikipedia.org/wiki/类型)，在[实例化](https://zh.wikipedia.org/wiki/实例)时作为参数指明这些类型。各种程序设计语言和其编译器、运行环境对泛型的支持均不一样。[Ada](https://zh.wikipedia.org/wiki/Ada)、[Delphi](https://zh.wikipedia.org/wiki/Delphi)、[Eiffel](https://zh.wikipedia.org/wiki/Eiffel)、[Java](https://zh.wikipedia.org/wiki/Java)、[C#](https://zh.wikipedia.org/wiki/C♯)、[F#](https://zh.wikipedia.org/wiki/F)、[Swift](https://zh.wikipedia.org/wiki/Swift_(程式語言)) 和 [Visual Basic .NET](https://zh.wikipedia.org/wiki/Visual_Basic_.NET) 称之为泛型（generics）；[ML](https://zh.wikipedia.org/wiki/ML语言)、[Scala](https://zh.wikipedia.org/wiki/Scala) 和 [Haskell](https://zh.wikipedia.org/wiki/Haskell) 称之为[参数多态](https://zh.wikipedia.org/wiki/参数多态)（parametric polymorphism）；[C++](https://zh.wikipedia.org/wiki/C%2B%2B) 和 [D](https://zh.wikipedia.org/wiki/D語言)称之为[模板](https://zh.wikipedia.org/wiki/模板_(C%2B%2B))。具有广泛影响的1994年版的《Design Patterns》一书称之为参数化类型（parameterized type）
>
> ​																																							 ------维基百科

理解：

泛型就是将**类型参数化**的一种方式，它能够提高类和方法的表达能力，**解耦类和方法与所使用的类型之间的关系**。

> 泛型，即“参数化类型”。一提到参数，最熟悉的就是定义方法时有形参，然后 调用此方法时传递实参。那么参数化类型怎么理解呢?顾名思义，就是将类型由 原来的具体的类型参数化，类似于方法中的变量参数，此时类型也定义成参数形式(可以称之为类型形参)，然后在使用/调用时传入具体的类型(类型实参)。
>
> 泛型的本质是为了参数化类型(在不创建新的类型的情况下，通过泛型指定的不同类型来控制形参具体限制的类型)。也就是说在泛型使用过程中，操作的数据类型被指定为一个参数，这种参数类型可以用在类、接口和方法中，分别被称为泛型类、泛型接口、泛型方法。                            
>
> —— 《Java编程思想》



## 泛型的继承关系

例子3：

```java
public class ArrayList<T> implements List<T> {
    private T[] array;
    public void add(T e){}
    public void remove(int index){}
    public T get(int index){}
}
```

jdk中，`ArrayList<T>`实现了`List<T>`接口：`List<String> list = new ArrayList<String>()` ,可以向上转型。

**但是，不能把`ArrayList<Integer>` 向上转型为`ArrayList<Number>`或`List<Number>`，`ArrayList<Integer>`和`ArrayList<Number>`没有继承关系。**

**类是可以继承的，泛型不可以。**

## 使用泛型

```java
// 可以省略后面的Number，编译器可以自动推断类型；
List<Number> list = new ArrayList<>();
```

使用的时候，把泛型参数T替换为具体的类型，不写具体的类型默认Object.

### 泛型类

```java
/** 此处T可以随便写为任意标识，常见的如T、E、K、V等形式的参数常用于表示泛型*/
public class Generic<T> {
    /** key这个成员变量的类型为T，key的类型由外部传入*/
    private T key;

    public void setKey(T key){
        this.key = key;
    }
    public T getKey(){
        return this.key;
    }  
    /** 在类中声明的泛型，在整个类里都可以使用，除了静态的部分，因为泛型必须是实例化的时候声明*/
    /** 静态区域的代码在编译期就已经确定，只与类相关*/
    class A <E> {
        T t;
    }
    /** 类里面的方法或类中再次声明的同名泛型是允许的，并且该泛型会覆盖掉外部类的同名泛型*/
    class B <T> {
        T t;
    }
    /** 静态内部类也可以使用泛型，实例化时赋予泛型实际类型*/
    static class C <T> {
        T t;
    } 

    public static void main(String[] args) {
        // 实例化类的时候，指定泛型的具体类型
        Generic<String> g = new Generic<>();
        g.setKey("hello");
        String key = g.getKey();
        System.out.println(key);
      	// 编译报错，不能使用泛型T，因为T属于实例，不属于类，不能在static方法里用类的泛型
        //        T t = null;
    }
    
    /**这里的静态方法里的T，和类上声明的T没有关系*/
    public static <T> T getKey(T t){
        return t;
    }
}
```

### 泛型接口

```java
/**
 * 未传入泛型实参时，与泛型类的定义相同，在声明类的时候，需将泛型的声明也一起加到类中
 * 即:class FruitGenerator<T> implements Generator<T>{
 * 如果不声明泛型，如:class FruitGenerator implements Generator<T>，编译器会报错:"Unknown
	class" 
*/
public interface  Generator<T>{
    public T next();
}
class FruitGenerator<T> implements Generator<T>{
    @Override
    public T next() {
        return null;
	} 
}
```



```java
/**
 * 传入泛型实参时:
 * 定义一个生产器实现这个接口,虽然我们只创建了一个泛型接口Generator<T>
 * 但是我们可以为T传入无数个实参，形成无数种类型的Generator接口。
 * 在实现类实现泛型接口时，如已将泛型类型传入实参类型，则所有使用泛型的地方都要替换成传入的实参类型 
 * 即:Generator<T>，public T next();中的的T都要替换成传入的String类型。
*/

public class FruitGenerator implements Generator<String> {
  	private String[] fruits = new String[]{"Apple", "Banana", "Pear"};
  	@Override
    public String next() {
       Random rand = new Random();
        return fruits[rand.nextInt(3)];
   }
}
```

### 泛型方法

1、泛型方法的定义和使用&类型推断：

```java
public class GenericMethods<E> {
    /**
      * 泛型方法的基本介绍
      * @param tClass 传入的泛型实参
      * @return T 返回值为T类型
      * 说明:
      		1)public 与 返回值中间<T>非常重要，可以理解为声明此方法为泛型方法。 
      		2)只有声明了<T>的方法才是泛型方法，泛型类中的使用了泛型的成员方法并不是泛型方法。 
      		3)<T>表明该方法将使用泛型类型T，此时才可以在方法中使用泛型类型T。 
      		4)与泛型类的定义一样，此处T可以随便写为任意标识，常见的如T、E、K、V等形式的参数
      * * * * */
    public <T> void f(T t) {
        System.out.println(t.getClass().getSimpleName());
    }
    public <T, K, V> void f1(T t, K k, V v) {
        System.out.println(t.getClass().getSimpleName());
        System.out.println(k.getClass().getSimpleName());
        System.out.println(v.getClass().getSimpleName());
    }
    public static void main(String[] args) {
        GenericMethods gm = new GenericMethods();
        /**在调用泛型方法的时候，通常不指定参数类型，而是像调用普通方法一样，编译器会做类型参数推断*/
        /**如果传入基本数据类型，会自动打包成包装类*/
        gm.f(" ");
        gm.f(new Integer(12));
        gm.f(1);
        gm.f(1.1);
        gm.f('c');
        gm.f(gm);
        System.out.println(" ========  ");
        gm.f1("",2,gm);
    }
}
```

2、泛型类，是在实例化类的时候指明泛型的具体类型;泛型方法，是在调用方法的时候指明泛型的具体类型 。

3、泛型方法所在的类可以是泛型类，也可以不是泛型类。

> 无论何时，只要你能做到，就应该尽量使用泛型方法。
>
> ——java编程思想

4、static方法无法访问泛型类的参数类型。

```java
class StaticGenerator<T> {
    /**
     * 如果在类中定义使用泛型的静态方法，需要添加额外的泛型声明(将这个方法定义成泛型方法) 
     * 即使静态方法要使用泛型类中已经声明过的泛型也不可以。
     * 如:public static void show(T t){..},此时编译器会提示错误信息:
     * "StaticGenerator cannot be refrenced from static context"
     */
    public static <T> void show(T t) {
    }
}
```

5、泛型与可变参数

```java
public class GenericVarargs<E> {
  	private E key;
  	/**使用类泛型的方法*/
    private E getKey(E key){
      return this.key;
    }
  	/** 泛型方法 */
    public static <T> List<T> getList(T... args) {
        List<T> list = new ArrayList<>(16);
        for (T t :
                args) {
            list.add(t);
        }
        return list;
    }

   	public static void main(String[] args) {
        List<Object> list = getList("a", 1, new GenericVarargs());
        System.out.println(list);

        // 作用相当于Arrays.asList（）
        List<String> list1 = getList("a", "b", "c");
        System.out.println(list1);
        // List<T> list1 = getList("a", "b", "c", 1); 
        
        String[] str = {"a", "b", "c"};
        List<String> list2 = getList(str);
        System.out.println(list2);
    }
}
```



## 泛型的擦除

```java
public class ErasedTypeEquivalence {    
    public static void main(String[] args) {        
        Class<? extends ArrayList> c1 = new ArrayList<String>(1).getClass();        
        Class<? extends ArrayList> c2 = new ArrayList<Integer>(1).getClass();        			System.out.println(c1 == c2);    
    }
}
```

**Tips**:可以用javap -c <类名>  反编译类，发现泛型类和普通类在边界处的操作是一样的：

get对象的时候，都是进行一次类型检查和类型转换；

set对象的时候，都没有传入具体的类型，都是声名为Object

```java
public class SimpleHolder {
    private Object obj;
    public Object getObj() {
        return obj;
    }
    public void setObj(Object obj) {
        this.obj = obj;
    }
    public static void main(String[] args) {
        SimpleHolder holder = new SimpleHolder();
        holder.setObj("Item");
        String obj = (String)holder.getObj();
    }
}

public class GeneticHolder<T> {
    private T obj;
    public T getObj() {
        return obj;
    }
    public void setObj(T obj) {
        this.obj = obj;
    }
    public static void main(String[] args) {
        GeneticHolder<String> holder = new GeneticHolder<>();
        holder.setObj("Item");
        String obj = holder.getObj();
    }
}
```

Java的泛型是用**擦除**实现的，即**在运行时，泛型的具体类型是无法知道的**。运行时，`List<Integer>` 和 `List<String>`都会变成原生类 `List`.



#### 为什么要泛型擦除

如果java从一开始设计的时候就有泛型的特性，那么实现的方式将不会是擦除，而是具体化类型。也就是说，在运行期，我们能够得到泛型的具体类型。

但是由于Java设计之初没有考虑这一特性，在Java5引入泛型的时候，就要**考虑兼容之前的版本，最后选择擦除的方式。**

这样在代码的运行期，不会对其他未使用泛型的类库产生影响。试想，如果Java5之后，加入了运行期泛型检查，那么比如我需要在新的代码里增加对旧代码的泛型类型检查，肯定是没办法检查出来的。

所以，要想实现迁移兼容性，就使它 `不具备探测其他类库是否使用了泛型的能力`。Java的泛型擦除是一个解决历史遗留问题的折中手段。

## 泛型擦除的补偿

已知泛型信息在运行期会被擦除，那么如果想在运行期能够拿到泛型的类型信息，怎么办？

## 泛型边界

extend关键字

```java
interface HasColor { 
    Color getColor();
}
class Dimension {
    public int x, y, z;
}
class Colored<T extends HasColor> {
    T item;
    Colored(T item) {
        this.item = item;
    }
    // 1、这里的泛型参数T,由于限定了其边界，所以可以用t的实例来调用方法
    Color color() {
        return this.item.getColor();
    }
}
// 2、这里编译错误，必须类在前，接口在后
// class ColoredDimention<T extends HasColor&Dimension>{ }
// 3、多重边界
class ColoredDimention<T extends Dimension & HasColor> {
    /**4、这里的泛型实例其实就是一个Dimension和HasColor的子类实例对象*/
    T item;
    ColoredDimention(T item) {
        this.item = item;
    }
    T getItem() {
        return item;
    }
    Color color() {
        return item.getColor();
    }
    int getX() {
        return item.x;
    }
    int getY() {
        return item.y;
    }
    int getZ() {
        return item.z;
    }
}

interface Weight {int weight();}

//5、泛型对象的边界只能继承一个类和多个接口
class Solid<T extends Dimension&HasColor&Weight>{
    T item;
    Solid(T item){
        this.item = item;
    }
    T getItem(){
        return item;
    }
    Color color(){
        return item.getColor();
    }
    int getX(){
        return item.x;
    }
    int weight(){
        return item.weight();
    }
}
class Bounded extends Dimension implements HasColor,Weight{
    @Override
    public  Color getColor() {
        return null;
    }
    public <V extends HasColor> void getColor(V item){
//        V value = new V();// 6、泛型对象没有默认构造器，所以不能new出来
        Color color = item.getColor();
    }
    @Override
    public int weight() {
        return 0;
    }
}
class Bounded1 extends Dimension implements HasColor{
    @Override
    public Color getColor() {
        return null;
    }
}
public class BasicBound {
    public static void main(String[] args) {
        Solid<Bounded> solid = new Solid<>(new Bounded());
        solid.color();
        solid.getX();
        solid.weight();
        Bounded item = solid.getItem();
        // 7、Bounded1 就不行，因为它并没有完全符合Solid里泛型的继承规则，少实现了一个接口Weight，他们具有不同的继承结构
//        Solid<Bounded1> solid1 = new Solid<Bounded1>();
        // 8、用通配符就可以
        Solid<? extends Bounded> solid1 = new Solid<>(new Bounded());
    }
}
```



## 泛型通配符

想要在两个类型之间建立某种类型的向上转型的关系，这就需要通配符

```java
package _15_._15_10_wildcard;
import com.sun.tools.corba.se.idl.constExpr.Or;
import java.util.ArrayList;
import java.util.List;
/**
 * @author zhangyn
 * @description 数组对持有的对象类型在编译期没有检查的机制，只有在运行期才能检查出来数组持有对象的类型
 * 容器类加上泛型则可以在编译期检查类型，所以尽量使用容器类
 * @date 2020-01-08 21:56
 */
public class CovariantArrays {
    public static void main(String[] args) {
      	// 1、编译错误，编译期就知道这个List持有的类型
//    List<Fruit> flist = new ArrayList<Apple>();
        // 2、编译没有错误，运行时可能出错
        Fruit[] fruits = new Apple[10];
        fruits[0] = new Apple();
      	fruits[0] = new Jonathan();
        // 抛出异常ArrayStoreException，因为运行时会检查fruits的实际类型是Apple
        fruits[0] = new Fruit();
        // 抛出异常ArrayStoreException
        fruits[0] = new Orange();
      	
      	// 3、?  extends Fruit
        List<? extends Fruit> flist = new ArrayList<Apple>();
        // 全部编译错误，不能向flist里添加任何对象
//        flist.add(new Apple());
//        flist.add(new Orange());
//        flist.add(new Object());
        flist.add(null);
        // 但是我们知道get出来的对象至少是一个Fruit对象
        Fruit fruit = flist.get(0);
      	
      	// 4、? super Fruit
      	List<? super Fruit> list1= new  ArrayList<>();
        list1.add(new Apple());
        list1.add(new Orange());
        Object object = list1.get(0);
        Fruit object1 = list1.get(1);
    }
}
class Fruit {
}
class Apple extends Fruit {
}
class Jonathan extends Apple {
}
class Orange extends Fruit {
}
```

### <? extends Fruit>

![image-20200113001527604](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20200113001527604.png)

### 

1、在add的时候，list可以是一个Fruit的list，也可以是Apple的list，还可以是Orange的list。

 编译器无法确定list的具体类型，所以不能add。

2、在取的时候，至少知道这个容器里的对象是个Fruit类型，所以可以get。

同理`List<? super Fruit> list1= new  ArrayList<>();`:

### <? super Fruit>

![image-20200113002931830](/Users/zhangyanan/Library/Application Support/typora-user-images/image-20200113002931830.png)



1、在add的时候是安全的，因为add的Apple，或者Orange都是Fruit的子类；

2、get是不安全的，因为不能确定list持有的是Fruit还是Object，如果是Object类型，那么

`Fruit f = list.get(0);`object会强转为Fruit，会转型失败。所以编译器会在编译期让这种泛型不可以做get操作。

### PECS原则

最后看一下什么是PECS（Producer Extends Consumer Super）原则，已经很好理解了：

- 频繁往外读取内容的，适合用上界Extends。
- 经常往里插入的，适合用下界Super。

##                                                                                                                                                                                                                                                          

Collections copy方法体现出super 和 extends 



参考：

通配符和边界：<https://blog.csdn.net/liuhui12345/article/details/100051796>

泛型通配符?与extends/super<https://how2j.cn/k/generic/generic-wildcard/376.html#nowhere>