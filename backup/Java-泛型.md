# 泛型概述

## 基本知识

泛型：是`JDK5`中引入的特性，可以在编译阶段约束操作的数据类型，并进行检查。

泛型的格式：`<数据类型>`

注意：泛型只能支持引用数据类型。

## 好处

* 统一数据类型
* 把运行时期的问题提到了编译期间，避免了强制类型转换可能出现的异常，因为在编译阶段类型就能确定下来。

## 分类

方法中形参类型不确定时：

**泛型类**

```java
public class MyArrayList<E>{}
```

**泛型方法**

```java
public <E> get(int index){}
```

**泛型接口**

```java
public class 类名 implements 接口名 <E>{}
```

## 继承&&通配符

>  泛型不具备继承性，但数据具备

举个例子：

```java
public static void method(ArrayList<Animal> list){}
```

```java
ArrayList<Ye> list = new ArrayList();

list.add(new Ye());
list.add(new Fu());
list.add(new Zi());
```

利用`泛型数据的继承性`实现的多态

```java
public static void keepPet(ArrayList<? extends Animal> list){
    for(Animal ani:list){
        if(ani instanceof Cat c){
            c.eat();
        }else if(ani instanceof Dog d){
            d.eat();
        }
    }
}
```



`?`也表示不确定的类型，可以进行类型的限定

`? extends E`表示可以传递`E`或者`E`所有的子类类型

```java
public static void method(ArrayList<? extends Fu> list)
```



`? super E`表示可以传递`E`或者`E`所有的子类类型

```java
public static void method(ArrayList<? super Zi> list)
```

