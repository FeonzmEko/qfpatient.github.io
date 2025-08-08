# 继承-Inheritance

1. 所谓继承，便是子类去继承父类的方法，省去重复代码编写，提高代码质量
2. 重写
   * 重写方法名称，形参列表必须与父类保持一致
   * 重写时，访问权限子类必须大于等于父类
   * 重写时，返回值类型小于等于父类
   * 建议：重写的方法尽量和父类保持一致
   * 只有被添加到虚方法表中的方法才能被重写

# 子类调用父类构造

使用关键字`super`来调用父类的构造函数来进行构造

```java
public class Father{
    String name;
    int age;
    public Father(){}
    public Father(String name,int age){
        this.name = name;
        this.age = age;
    }
}
```

```java
public class Son extends Father{
    public Son(){
        super(); // 调用父类无参构造
    }
    public Son(String name,int age){
        super(name,age);
    }
}
```

# 多态-Polymorphism

1. 什么是多态？

   同类型的对象，表现出的不同形态

2. 多态的表现形式

   ```java
   Father f = new Son();
   ```

3. 多态的前提

   * 有继承关系
   * 有父类引用指向子类对象
   * 有方法重写

4. 多态调用成员的特点

   * 变量调用：编译看左边，运行也看左边
   * 方法调用：编译看左边，运行看右边

   ```java
   package demo2;
   
   public class Test {
       public static void main(String[] args) {
           // 创建对象：多态方式
           // Fu f = new Zi();
           Animal a = new Dog();
           // 变量调用：编译看左边，运行也看左边
           // 编译看左边：javac编译代码时，会看左边父类有没有这个变量，有则编译成功，否则失败
           // 运行也看左边：java运行代码时，获取左边父类变量的值
           System.out.println(a.name);
   
           // 方法调用：编译看左边，运行看右边
           a.show();
       }
   }
   
   class Animal{
       String name = "Animal";
   
       public void show(){
           System.out.println("Animal --- show方法");
       }
   }
   
   class Dog extends Animal{
       String name = "Dog";
   
       @Override
       public void show(){
           System.out.println("Dog --- show方法");
       }
   }
   
   class Cat extends Animal{
       String name = "Cat";
   
       @Override
       public void show(){
           System.out.println("Cat --- show方法");
       }
   }
   ```

5. 多态的优势：在方法中，使用父类型作为参数，可以接受所有子类对象

6. 多态的弊端：不能使用子类的特有方法

   ```java
   Fu f = new Zi();
   f.method(); // method()是子类Zi的特有方法，而多态是基于override即方法重写，所以会报错
   
   // 解决方案：
   if(a instanceof Zi1){
       Zi1 d = (Zi1)a;
       d.method();
   }else if(a instanceof Zi2){
       Zi2 d = (Zi2)a;
       d.method();
   }
   
   // java14 新特性
   if(a instanceof Zi1 d){
       d.method1();
   }else if(a instanceof d){
       d.method2();
   }
   ```

# 包和final

## 包

包就是文件夹。用来管理不同功能的java类，方便后期代码维护。

* 命名规则：公司域名反写 + 包的作用，需要全部英文小写，见名知意。eg：**com.itheima.com.domain**

使用其他类的规则

* 使用同一个包中的类时，不需要导包。
* 使用java.lang包中的类时，不需要导包。
* 其他情况都需要导包
* 如果同时使用两个包中的同名类，则需要用全类名。

## final

方法：最终方法，不能被重写。

```java
public final void eat(String something){
        System.out.println("动物正在吃" + something);
}
```

类：最终类，不能被继承。

```java
final class Fu{
}
```

变量：叫做常量，只能被赋值一次。

```java
final int a = 10;
```

> final修改基本数据类型：记录的值不能改变
>
> final修改引用数据类型：记录的地址值不能改变，内部的属性值可以改变
>
> 常量的命名规范：
>
> * 单个单词：全部大写
> * 多个单词：全部大写，单词之间用下划线隔开

## 权限修饰符

| 修饰符      | 同一个类中 | 同一个包中其他类 | 不同包下的子类 | 不同包下的无关类 |
| ----------- | ---------- | ---------------- | -------------- | ---------------- |
| `private`   | `√`        |                  |                |                  |
| 留空        | `√`        | `√`              |                |                  |
| `protected` | `√`        | `√`              | `√`            |                  |
| `public`    | `√`        | `√`              | `√`            | `√`              |

> 使用规则：
>
> 实际开发中，一般只用`private`和`public`
>
> * 成员变量私有
> * 方法公开
>
> <p><span style="color: red;">特例：如果方法中的代码是抽取其他方法中的共性代码，一般也私有。</span></p>

数据初始化，且只想执行一次，使用`静态代码块`方法

```java
static ArrayList<User> list = new ArrayList<>();

static{
    list.add(/something/);
}
```

# 抽象类和抽象方法

* 抽象方法：将`共性`的行为（`方法`）抽取到父类之后，由于每一个子类执行的内容是不一样的，所以，在父类中不能确定`具体的方法体`。
* 抽象类：如果一个类中存在抽象方法，那么该类`必须`声明为抽象类

```java
public abstract class Person {
    public abstract void work();
}
```

抽象类和抽象方法的注意事项：

* 抽象类不能实例化
* 抽象类不一定有抽象方法，有抽象方法的类一定是抽象类
* 可以有构造方法
* 抽象类的子类
  * 要么是抽象类
  * 要么重写抽象类中的所有抽象方法

# 接口

接口是一种规则，是对行为的抽象

## 接口的定义和使用

* 接口用关键字`interface`来定义

  ```java
  public interface 接口名 {}
  ```

  

* 接口不能实例化

* 接口和类之间是实现关系，通过`implements`关键字表示

  ```java
  public class 类名 implements 接口名 {}
  ```

* 接口的子类（实现类）

  * 要么是抽象类
  * 要么重写接口中所有的抽象方法

注意：

* 接口和类的实现关系，可以单实现，也可以多实现

  ```java
  public class 类名 implements 接口名1，接口名2 {}
  ```

  

* 实现类还可以在一个继承类的同时实现多个接口

  ```java
  public class 类名 extends 父类 implements 接口名1，接口名2 {}
  ```

## 接口中成员的特点

* 成员变量

  * 只能是常量
  * 默认修饰符：`public static final`

* 无构造方法

* 成员方法

  * 只能是抽象方法
  * 默认修饰符：`public abstract`

  
  
  ### JDK7以前：接口只能定义抽象方法
  
  ### JDK8的新特性：
  
  1. 接口中可以定义有方法体的方法
  
  * 允许在接口中定义默认方法，需要使用关键字`default`修饰
    * 作用：解决接口升级的问题
  * 接口中默认方法的定义格式：
    * 格式：`public default 返回值类型 方法名(参数列表){}`
    * 范例：`public default void show(){}`
  * 接口中默认方法的注意事项：
    * 默认方法不是抽象方法，所以不强制被重写，但是如果要重写，重写的时候去掉`default`关键字
    * `public`可以省略，`default`不可以省略
    * 如果实现了多个接口，多个接口中存在相同名字的默认方法，子类就必须对该方法进行重写
  
  2. 新增的方法
  
  * 允许在接口中定义静态方法，需要用`static`修饰
  * 接口中静态方法的定义格式
    * 格式：`public static 返回值类型 方法名(参数列表){}`
    * 范例：`public static void show(){}`
  * 接口中静态方法的注意事项：
    * 静态方法只能通过接口名调用，不能通过实现类或对象名调用
    * `public`可以省略，`static`不能省略
  
  
  
  ### JDK9的新特性：接口中可以定义私有方法
  
  接口中私有方法的定义格式：
  
  * 默认方法
    * 格式：`private 返回值类型 方法名（参数列表）{}`
    * 范例：`private void show（）{}`
  * 静态方法
    * 格式：`private static 返回值类型 方法名（参数列表）{}`
    * 范例：`private static void show（）{}`

## 接口和类之间的关系

* 类和类的关系
  * 继承关系，只能单继承，不能多继承，但可以多层继承
* 类和接口的关系
  * 实现关系，可以单实现，也可以多实现，还可以在继承一个类的同时实现多个接口
* 接口和接口的关系
  * 继承关系，可以单继承，也可以多继承

# 内部类

## 什么是内部类？

在一个类的里面，在定义一个类。

eg：在A类的内部定义B类，B类就被称为内部类。

## 为什么要学习内部类？

> 需求：写一个javabean类描述汽车
>
> 属性：品牌，车龄，颜色，发动机品牌及使用年限

```java
public class Car{
    String carBand;
    int carAge;
    String color;
    class Engine{
        String engineBand;
        int engineAge;
    }
}
```

* 内部类表示的事物是外部类的一部分
* 内部类单独出现没有意义
* 内部类的访问特点
  * 内部类可以直接访问外部类的成员，包括私有
  * 外部类要访问内部类的成员，必须创建对象

## 内部类的分类

* 成员内部类，静态内部类，局部内部类（了解即可）
* 匿名内部类

## 获取内部类对象的两种方式

* 内部类被private修饰时：

  ```java
  public class Outer {
      String name;
  
      private class Inner{
          static int a = 10;
      }
  
      public Inner getInstance(){
          return new Inner();
      }
  }
  ```

* 内部类不被private修饰时

  ```java
  Outer.Inner oi = new Outer().new Inner();
  ```

## 匿名内部类

### 什么是匿名内部类

隐藏了名字的内部类，可以写在成员位置或者局部位置

### 格式

```java
new 类名或接口名(){
    重写方法;
};
```

### 格式的细节

包含了继承或实现，方法重写和创建对象

整体就是一个类的子类对象或者接口的实现类对象

### 使用场景

当方法的参数是接口或者类时，

以接口为例，可以传递这个接口的实现类对象，

如果实现类只要使用一次，就可以使用匿名内部类简化代码

```java
// Swim接口的实现类的对象
Swim swimmer = new Swim(){
      @Override
        public void swim() {
            System.out.println("Override.swim");
         }
 };
```

