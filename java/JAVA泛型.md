# JAVA泛型

Java 泛型的出现最开始是为了解决集合中的类型不安全问题。在泛型出现之前，当我们用集合的时候，集合所存储的类型就是Object.

```java
List list = new ArrayList();
list.add(1);
list.add("string");
list.add(new Object());
```

看起来这样很方便，想放什么到集合中就可以放，但是这让程序员不得不对集合中类型进行类型判断。比如在一个狗的集合中突然出现了一只猫，如果你没有对这个对象进行判断那么很有可能出问题。当JAVA5引入泛型之后，那么狗的集合就只能包含狗，如果你要在集合中添加一只猫，那么在编译阶段就会报错。

```java
List<Dog> dogs = new ArrayList<Integer>();
dogs.add(new Cat());//will compile fail
```

另外泛型能够让程序写得更加泛化。

### 使用泛型

#### JAVA generic class

```java
public class GenericsType<T>{
    private T t;
    
    public void set(T t){
        this.t = t;
    }
    
    public T get(){
        return t;
    }
    public static void main(String[] args){
        GenericsType<String> s = new GenericsType<String>();
        s.set("1232");
   		s.set(123);//will compile error
    }
}
```

#### JAVA generic interface

```java
public interface Comparable<T>{
    public int comare(T t);
}
```

#### JAVA generic type

JAVA 泛型命名规范：

- E- Element 在集合框架中使用较多
- k -key 在Map中使用较多
- V -value 在Map中使用较多
- T -Type

#### JAVA generic method

```java
public class GenericsMethods{
    public static <T> boolean isEqual(GenericsType<T> g1, GenericsType<T> g2){
        return g1.get().equal(g2.get());
    }
}
```

#### JAVA generics Bounded Type Parameters

```java
public static <T extends Comparable<T>> int compare(T t1,T t2){
    return t1.compareTo(t2);
}
```

#### JAVA generics and Inheritance

如果B是A的subclass,那么B的对象可以复制给A的句柄。但是这在泛型当中行不通。

```
public class GenericsInheritance {
    public static void main(String[] args){
        String a = "abc";
        Object o = a;//works because a is-a object.
        MyClass<String> myclass1 = new MyClass<String>();
        MyClass<Object> myclass2 = new MyClass<Object>();
        myclass1 = myclass2;//compilation error
    } 
}
```

#### Java gnerics upper bounded wildcard

让我们先来看一个例子。我想求一个Number 列表和。

```java
public static double sum(List<Number> list){
    double sum = 0;
    for(Number n: list){
        sum += n.doubleValue();
    }
}
```

上面这段代码只能针对List<Number>生效，存在一些局限性。比如我现在相对Integer和Double的列表进行求和，那么上面这段代码是不可用的。我们需要引入extends和通配符。

```java
public static double sum(List<T extends Number> list){
    double sum = 0;
    for(Number n: list){
        sum += n.doubleValue();
    }
}
```

上面这段代码中的list不能够add 任何对象，除了null.

#### Java generics lower bounded wildcard

加入现在我们想在方法中给List<Integer>添加一个Integer，我们需要用到? with super, 这时候这个list 同时具有了能够添加Number和Object的能力。

#### Java generics type erasure 

泛型主要是用来做类型检查的，只会在编译期间起效果，并不会在运行时用到。所以JAVA编译器会用到类型擦除来移除掉这些类型检查的代码在字节码中。