# JAVA容器

Java容器类类库的用途是“保持对象”，并将其划分为两个不同的概念。

### 分类

1. Collection.一个独立元素的队列。这些元素都服从一条或多条规则，List必须按照插入的顺序保存元素，Set保证元素都是不重复的,Queue按照排队规则来确定对象的顺序。

![FrameworkHierarchy - Java Collections - Edureka](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2017/05/Collection-framework-hierarchy.png)

2. Map. 以键值对的形式来存储值。

### 迭代器

任何容器类都要有插入和取回的功能，毕竟持有事物是容器最基本的功能。以List容器为例，add()可以添加元素，get()方法可以取回元素。

对容器进行遍历是我们经常用到的操作，如果针对不同Collection的实现，比如List , set都有遍历。如何重用这部分代码。于是迭代器被提出来了，我们可以通过Iterator写出更加通用的代码。

```java
 public static void main(String[] args) {
        List<String> list = new ArrayList<String>(Arrays.asList("A", "B", "C"));
        Iterator it = list.iterator();
        while (it.hasNext()) {
            System.out.println(it.next());
        }
    }
```

ForEach的实现方式就是通过迭代器来实现的。

```java
public static void main(String[] args) {
        List<String> list = new ArrayList<String>(Arrays.asList("A", "B", "C"));
        for (Object aList : list) {
            System.out.println(aList);
        }
    }
```

### List 

List是在平时代码中用的最多的一种集合。List接口在Collection的基础上增加了很多方法。有两种类型的List, ArrayList 和 LinkedList。他们的底层实现不同，ArrayList主要通过数组实现，LinkedList主要通过双向链表实现。如果对于List的查询操作较多，可以考虑用ArrayList,对类别的插入和删除操作多的话，应该选择LinkedList。

### Map

Map 的实现有HashMap, TreeMap, LinkedHashMap等。

| Type              | Description                                                  |
| :---------------- | ------------------------------------------------------------ |
| HashMap           | Map基于散列表的实现。插入和查询键值对的开销是固定的。可以通过构造器设置容量和负载因子，以调整容器的性能。 |
| TreeMap           | 基于红黑树的实现。查看键 或 键值对 时，它们会被排序。        |
| LinkedHashMap     | 类似于HashMap，取得“键值对”的顺序是其插入顺序。只比HashMap慢一点，在迭代器迭代的时候更快，因为是由链表实现的。 |
| WeakHashMap       | 弱键映射，允许释放映射所指向的对象。                         |
| ConcurrentHashMap | 线程安全的Map                                                |
| IdentityHashMap   | 使用==代替equals()对键进行比较的散列映射。                   |

### Set

| Type           | Description                                                  |
| -------------- | ------------------------------------------------------------ |
| Set(interface) | 存入set的元素都是唯一的，因为set不保存重复元素。加入set的元素必须定义equals方法以确保对象的唯一性。set 与 collection有完全一样的接口,不保证维护元素的次序 |
| HashSet*       | 为快速查找而设计的Set. 存入HashSet的元素必须定义hashcode     |
| TreeSet        | 保持次序的set。底层为树结构。元素必须试下Comparable接口      |
| LinkedHashSet  | 具有HashSet的查询速度，且内部使用链表维护元素的顺序(插入的次序)。在使用迭代器遍历的时候，输出是按照插入次序输出的。 |

