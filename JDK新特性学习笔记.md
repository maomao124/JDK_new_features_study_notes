[toc]

---







# JDK8

## Lambda表达式

### 传统写法

```java
package mao;

/**
 * Project name(项目名称)：JDK8-Lambda
 * Package(包名): mao
 * Class(类名): Test1
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/19
 * Time(创建时间)： 16:55
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test1
{
    public static void main(String[] args)
    {
        new Thread(new Runnable()
        {
            @Override
            public void run()
            {
                System.out.println("线程运行");
            }
        }).start();
    }
}

```





### Lambda表达式写法

```java
package mao;

/**
 * Project name(项目名称)：JDK8-Lambda
 * Package(包名): mao
 * Class(类名): Test2
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/19
 * Time(创建时间)： 16:59
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test2
{
    public static void main(String[] args)
    {
        new Thread(() -> System.out.println("线程运行")).start();
    }
}

```





### 分析

对于Runnable接口的匿名内部类用法，可以分析出几点内容：

* Thread 类需要 Runnable 接口作为参数，其中的抽象 run 方法是用来指定线程任务内容的核心
* 为了指定 run 的方法体，需要Runnable 接口的实现类
* 为了省去定义一个 Runnable实现类的麻烦，使用匿名内部类
* 必须覆盖重写抽象run方法，所以方法名称、方法参数、方法返回值不得不再写一遍，且不能写错



Lambda是一个匿名函数，可以理解为一段可以传递的代码



Lambda语法和传统语法执行效果是完全一样的，可以在JDK 8或更高的编译级别下通过。从代码的语义中可以看出：我们 启动了一个线程，而线程任务的内容以一种更加简洁的形式被指定

我们只需要将要执行的代码放到一个Lambda表达式中，不需要定义类，不需要创建对象





### 优点

* 简化匿名内部类的使用

* 语法更加简单





### 标准格式

```sh
(参数类型 参数名称) -> {
    代码体;
 }
```



格式：

* (参数类型 参数名称)：参数列表
* {代码体;}：方法体
* -> ：箭头，分隔参数列表和方法体





### 有返回值的Lambda

#### 传统写法

使用传统的代码对ArrayList集合进行排序



实体类：

```java
package mao;

import java.util.StringJoiner;

/**
 * Project name(项目名称)：JDK8-Lambda
 * Package(包名): mao
 * Class(类名): Student
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/20
 * Time(创建时间)： 16:38
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Student
{
    private Long id;
    private String name;
    private int age;

    public Long getId()
    {
        return id;
    }

    public Student setId(Long id)
    {
        this.id = id;
        return this;
    }

    public String getName()
    {
        return name;
    }

    public Student setName(String name)
    {
        this.name = name;
        return this;
    }

    public int getAge()
    {
        return age;
    }

    public Student setAge(int age)
    {
        this.age = age;
        return this;
    }

    @Override
    public String toString()
    {
        return new StringJoiner(", ", Student.class.getSimpleName() + "[", "]")
                .add("id=" + id)
                .add("name='" + name + "'")
                .add("age=" + age)
                .toString();
    }
}
```





传统写法：

```java
package mao;

import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

/**
 * Project name(项目名称)：JDK8-Lambda
 * Package(包名): mao
 * Class(类名): Test3
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/20
 * Time(创建时间)： 16:40
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test3
{
    public static void main(String[] args)
    {
        List<Student> studentList = new ArrayList<>(4);
        studentList.add(new Student()
                .setId(1L)
                .setName("测试1")
                .setAge(13));
        studentList.add(new Student()
                .setId(2L)
                .setName("测试2")
                .setAge(12));
        studentList.add(new Student()
                .setId(3L)
                .setName("测试3")
                .setAge(19));
        studentList.add(new Student()
                .setId(4L)
                .setName("测试4")
                .setAge(8));
        studentList.sort(new Comparator<Student>()
        {
            @Override
            public int compare(Student o1, Student o2)
            {
                return o1.getAge() - o2.getAge();
            }
        });
        System.out.println(studentList);
    }
}
```



```sh
[Student[id=4, name='测试4', age=8], Student[id=2, name='测试2', age=12], Student[id=1, name='测试1', age=13], Student[id=3, name='测试3', age=19]]
```







#### Lambda写法

```java
package mao;

import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

/**
 * Project name(项目名称)：JDK8-Lambda
 * Package(包名): mao
 * Class(类名): Test4
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/20
 * Time(创建时间)： 16:45
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test4
{
    public static void main(String[] args)
    {
        List<Student> studentList = new ArrayList<>(4);
        studentList.add(new Student()
                .setId(1L)
                .setName("测试1")
                .setAge(13));
        studentList.add(new Student()
                .setId(2L)
                .setName("测试2")
                .setAge(12));
        studentList.add(new Student()
                .setId(3L)
                .setName("测试3")
                .setAge(19));
        studentList.add(new Student()
                .setId(4L)
                .setName("测试4")
                .setAge(8));
        studentList.sort((o1, o2) -> o1.getAge() - o2.getAge());
        System.out.println(studentList);
    }
}
```



```sh
[Student[id=4, name='测试4', age=8], Student[id=2, name='测试2', age=12], Student[id=1, name='测试1', age=13], Student[id=3, name='测试3', age=19]]
```







### 实现原理

匿名内部类在编译的时候会一个class文件

Lambda在程序运行的时候形成一个类





### Lambda省略格式

在Lambda标准格式的基础上，使用省略写法的规则为：

* 小括号内参数的类型可以省略
* 如果小括号内有且仅有一个参数，则小括号可以省略
* 如果大括号内有且仅有一个语句，可以同时省略大括号、return关键字及语句分号





### 前提条件

Lambda的语法非常简洁，但是Lambda表达式不是随便使用的，使用时有几个条件：

* 方法的参数或局部变量类型必须为接口才能使用Lambda
* 接口中有且仅有一个抽象方法





### 函数式接口

函数式接口在Java中是指：有且仅有一个抽象方法的接口

函数式接口，即适用于函数式编程场景的接口。而Java中的函数式编程体现就是Lambda

函数式接口就是可以 适用于Lambda使用的接口。只有确保接口中有且仅有一个抽象方法，Java中的Lambda才能顺利地进行推导



**@FunctionalInterface注解**：一旦使用该注解来定义接口，编译器将会强制检查该接口是否确实有且仅有一个抽象方法，否则将会报错。不过，即 使不使用该注解，只要满足函数式接口的定义，这仍然是一个函数式接口，使用起来都一样



```java
package mao;

@FunctionalInterface
public interface MyFunctionalInterface
{
    void run();
}
```



![image-20231020165818306](img/JDK新特性学习笔记/image-20231020165818306.png)



![image-20231020165839398](img/JDK新特性学习笔记/image-20231020165839398.png)









### 对比

Lambda和匿名内部类在使用上的区别：

* 所需的类型不一样
  * 匿名内部类，需要的类型可以是类、抽象类、接口
  * Lambda表达式，需要的类型必须是接口
* 抽象方法的数量不一样
  * 匿名内部类所需的接口中抽象方法的数量随意
  * Lambda表达式所需的接口只能有一个抽象方法
* 实现原理不同
  * 匿名内部类是在编译后会形成class
  * Lambda表达式是在程序运行的时候动态生成class







## 接口默认方法

### 概述

JDK 8以前的接口：

```
interface 接口名 {
    静态常量;
    抽象方法;
}
```



JDK 8对接口的增强，接口还可以有默认方法和静态方法



```
interface 接口名 {
    静态常量;
    抽象方法;
    默认方法;
    静态方法;
}
```



### 背景

在JDK 8以前接口中只能有抽象方法。存在以下问题：

```java
package mao;

public interface MyFunctionalInterface
{
    void run();
}

class Test5 implements MyFunctionalInterface
{

    @Override
    public void run()
    {

    }
}

class Test6 implements MyFunctionalInterface
{

    @Override
    public void run()
    {

    }
}

```



如果给接口新增抽象方法，所有实现类都必须重写这个抽象方法。不利于接口的扩展

```java
package mao;

public interface MyFunctionalInterface
{
    void run();

    void run2();
}

class Test5 implements MyFunctionalInterface
{

    @Override
    public void run()
    {

    }

    @Override
    public void run2()
    {
        
    }
}

class Test6 implements MyFunctionalInterface
{

    @Override
    public void run()
    {

    }
}

```



![image-20231020171710008](img/JDK新特性学习笔记/image-20231020171710008.png)





因此，在JDK 8时为接口新增了默认方法



### 定义格式

```
interface 接口名 { 
    修饰符 default 返回值类型 方法名() { 
        代码; 
    } 
} 
```





### 使用

* 方式一：实现类直接调用接口默认方法
* 方式二：实现类重写接口默认方法



#### 方式一

```java
package mao;

/**
 * Project name(项目名称)：JDK8-Lambda
 * Package(包名): mao
 * Interface(接口名): MyFunctionalInterface2
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/20
 * Time(创建时间)： 17:22
 * Version(版本): 1.0
 * Description(描述)： 接口默认方法-实现类直接调用接口默认方法
 */

public interface MyFunctionalInterface2
{
    void run();

    default void run2()
    {
        System.out.println("执行MyFunctionalInterface2.run2");
    }

}

class Test7 implements MyFunctionalInterface2
{

    @Override
    public void run()
    {

    }

    public static void main(String[] args)
    {
        Test7 test7=new Test7();
        test7.run2();
    }
}
```





#### 方式二

```java
package mao;

/**
 * Project name(项目名称)：JDK8-Lambda
 * Package(包名): mao
 * Interface(接口名): MyFunctionalInterface3
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/20
 * Time(创建时间)： 17:29
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public interface MyFunctionalInterface3
{
    void run();

    default void run2()
    {
        System.out.println("执行MyFunctionalInterface3.run2");
    }
}


class Test8 implements MyFunctionalInterface3
{

    @Override
    public void run()
    {

    }

    @Override
    public void run2()
    {
        System.out.println("执行Test8.run2");
    }

    public static void main(String[] args)
    {
        Test8 test8 = new Test8();
        test8.run2();
    }
}
```



```sh
执行Test8.run2
```







## 接口静态方法

### 定义格式

```
interface 接口名 {
    修饰符 static 返回值类型 方法名() {
        代码;
    }
}
```





### 使用

接口名.静态方法名()

```java
package mao;

/**
 * Project name(项目名称)：JDK8-Lambda
 * Package(包名): mao
 * Interface(接口名): MyFunctionalInterface4
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/20
 * Time(创建时间)： 17:52
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public interface MyFunctionalInterface4
{
    static void run3()
    {
        System.out.println("MyFunctionalInterface4静态方法run3");
    }
}

class Test9 implements MyFunctionalInterface4
{
    public static void main(String[] args)
    {
        MyFunctionalInterface4.run3();
    }
}
```





### 默认方法和静态方法的区别

* 默认方法通过实例调用，静态方法通过接口名调用
*  默认方法可以被继承，实现类可以直接使用接口默认方法，也可以重写接口默认方法
* 静态方法不能被继承，实现类不能重写接口静态方法，只能使用接口名调用









## 常用内置函数式接口

### 概述

使用Lambda表达式的前提是需要有函数式接口，而Lambda使用时不关心接口名，抽象方法名，只关心抽 象方法的参数列表和返回值类型。因此为了让我们使用Lambda方便，JDK提供了大量常用的函数式接口



它们主要在 java.util.function包

![image-20231020181009725](img/JDK新特性学习笔记/image-20231020181009725.png)





常用接口：

* Supplier接口
* Consumer接口
* Function接口
* Predicate接口







### Supplier接口

对应的Lambda表达式需要“对外提供”一个符合泛型类型的对象数据

供给型接口，通过Supplier接口中的get方法可以得到一个值，无参有返回的接口

```java
/*
 * Copyright (c) 2012, 2013, Oracle and/or its affiliates. All rights reserved.
 * DO NOT ALTER OR REMOVE COPYRIGHT NOTICES OR THIS FILE HEADER.
 *
 * This code is free software; you can redistribute it and/or modify it
 * under the terms of the GNU General Public License version 2 only, as
 * published by the Free Software Foundation.  Oracle designates this
 * particular file as subject to the "Classpath" exception as provided
 * by Oracle in the LICENSE file that accompanied this code.
 *
 * This code is distributed in the hope that it will be useful, but WITHOUT
 * ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or
 * FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License
 * version 2 for more details (a copy is included in the LICENSE file that
 * accompanied this code).
 *
 * You should have received a copy of the GNU General Public License version
 * 2 along with this work; if not, write to the Free Software Foundation,
 * Inc., 51 Franklin St, Fifth Floor, Boston, MA 02110-1301 USA.
 *
 * Please contact Oracle, 500 Oracle Parkway, Redwood Shores, CA 94065 USA
 * or visit www.oracle.com if you need additional information or have any
 * questions.
 */
package java.util.function;

/**
 * Represents a supplier of results.
 *
 * <p>There is no requirement that a new or distinct result be returned each
 * time the supplier is invoked.
 *
 * <p>This is a <a href="package-summary.html">functional interface</a>
 * whose functional method is {@link #get()}.
 *
 * @param <T> the type of results supplied by this supplier
 *
 * @since 1.8
 */
@FunctionalInterface
public interface Supplier<T> {

    /**
     * Gets a result.
     *
     * @return a result
     */
    T get();
}
```





使用Lambda表达式返回数组元素最大值

```java
package mao;

import java.util.Arrays;
import java.util.function.Supplier;

/**
 * Project name(项目名称)：JDK8_FunctionalInterface
 * Package(包名): mao
 * Class(类名): Test1
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/20
 * Time(创建时间)： 18:03
 * Version(版本): 1.0
 * Description(描述)： Supplier
 */

public class Test1
{
    public static void main(String[] args)
    {
        printMax(() ->
        {
            int[] arr = {10, 20, 100, 30, 40, 50};
            Arrays.sort(arr);
            return arr[arr.length - 1];
        });
    }

    private static void printMax(Supplier<Integer> supplier)
    {
        int max = supplier.get();
        System.out.println("max = " + max);
    }
}
```





### Consumer接口

消费一个数据，其数据类型由泛型参数决定

```java
/*
 * Copyright (c) 2010, 2013, Oracle and/or its affiliates. All rights reserved.
 * DO NOT ALTER OR REMOVE COPYRIGHT NOTICES OR THIS FILE HEADER.
 *
 * This code is free software; you can redistribute it and/or modify it
 * under the terms of the GNU General Public License version 2 only, as
 * published by the Free Software Foundation.  Oracle designates this
 * particular file as subject to the "Classpath" exception as provided
 * by Oracle in the LICENSE file that accompanied this code.
 *
 * This code is distributed in the hope that it will be useful, but WITHOUT
 * ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or
 * FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License
 * version 2 for more details (a copy is included in the LICENSE file that
 * accompanied this code).
 *
 * You should have received a copy of the GNU General Public License version
 * 2 along with this work; if not, write to the Free Software Foundation,
 * Inc., 51 Franklin St, Fifth Floor, Boston, MA 02110-1301 USA.
 *
 * Please contact Oracle, 500 Oracle Parkway, Redwood Shores, CA 94065 USA
 * or visit www.oracle.com if you need additional information or have any
 * questions.
 */
package java.util.function;

import java.util.Objects;

/**
 * Represents an operation that accepts a single input argument and returns no
 * result. Unlike most other functional interfaces, {@code Consumer} is expected
 * to operate via side-effects.
 *
 * <p>This is a <a href="package-summary.html">functional interface</a>
 * whose functional method is {@link #accept(Object)}.
 *
 * @param <T> the type of the input to the operation
 *
 * @since 1.8
 */
@FunctionalInterface
public interface Consumer<T> {

    /**
     * Performs this operation on the given argument.
     *
     * @param t the input argument
     */
    void accept(T t);

    /**
     * Returns a composed {@code Consumer} that performs, in sequence, this
     * operation followed by the {@code after} operation. If performing either
     * operation throws an exception, it is relayed to the caller of the
     * composed operation.  If performing this operation throws an exception,
     * the {@code after} operation will not be performed.
     *
     * @param after the operation to perform after this operation
     * @return a composed {@code Consumer} that performs in sequence this
     * operation followed by the {@code after} operation
     * @throws NullPointerException if {@code after} is null
     */
    default Consumer<T> andThen(Consumer<? super T> after) {
        Objects.requireNonNull(after);
        return (T t) -> { accept(t); after.accept(t); };
    }
}
```



使用Lambda表达式将一个字符串转成大写和小写的字符串

```java
package mao;

import java.util.Locale;
import java.util.function.Consumer;

/**
 * Project name(项目名称)：JDK8_FunctionalInterface
 * Package(包名): mao
 * Class(类名): Test2
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/20
 * Time(创建时间)： 18:29
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test2
{
    public static void main(String[] args)
    {
        test(s -> System.out.println(s.toUpperCase(Locale.ROOT)));
    }

    private static void test(Consumer<String> consumer)
    {
        consumer.accept("hello");
    }
}

```





**andThen**：如果一个方法的参数和返回值全都是 Consumer 类型，那么就可以实现效果：消费一个数据的时候，首先做一个操作，然后再做一个操作，实现组合

```java
package mao;

import java.util.Locale;
import java.util.function.Consumer;

/**
 * Project name(项目名称)：JDK8_FunctionalInterface
 * Package(包名): mao
 * Class(类名): Test3
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/20
 * Time(创建时间)： 18:35
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test3
{
    public static void main(String[] args)
    {
        test(s -> System.out.println(s.toUpperCase(Locale.ROOT)),
                s -> System.out.println(s.length()));
    }

    private static void test(Consumer<String> consumer1,Consumer<String> consumer2)
    {
        //consumer1.accept("hello");
        //consumer2.accept("world");
        consumer2.andThen(consumer1).accept("world");
        consumer1.andThen(consumer2).accept("world");
    }
}

```



```sh
5
WORLD
WORLD
5
```







### Function接口

Function接口用来根据一个类型的数据得到另一个类型的数据，前者称为前置条件，后者称为后置条件。有参数有返回值

```java
/*
 * Copyright (c) 2010, 2013, Oracle and/or its affiliates. All rights reserved.
 * DO NOT ALTER OR REMOVE COPYRIGHT NOTICES OR THIS FILE HEADER.
 *
 * This code is free software; you can redistribute it and/or modify it
 * under the terms of the GNU General Public License version 2 only, as
 * published by the Free Software Foundation.  Oracle designates this
 * particular file as subject to the "Classpath" exception as provided
 * by Oracle in the LICENSE file that accompanied this code.
 *
 * This code is distributed in the hope that it will be useful, but WITHOUT
 * ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or
 * FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License
 * version 2 for more details (a copy is included in the LICENSE file that
 * accompanied this code).
 *
 * You should have received a copy of the GNU General Public License version
 * 2 along with this work; if not, write to the Free Software Foundation,
 * Inc., 51 Franklin St, Fifth Floor, Boston, MA 02110-1301 USA.
 *
 * Please contact Oracle, 500 Oracle Parkway, Redwood Shores, CA 94065 USA
 * or visit www.oracle.com if you need additional information or have any
 * questions.
 */
package java.util.function;

import java.util.Objects;

/**
 * Represents a function that accepts one argument and produces a result.
 *
 * <p>This is a <a href="package-summary.html">functional interface</a>
 * whose functional method is {@link #apply(Object)}.
 *
 * @param <T> the type of the input to the function
 * @param <R> the type of the result of the function
 *
 * @since 1.8
 */
@FunctionalInterface
public interface Function<T, R> {

    /**
     * Applies this function to the given argument.
     *
     * @param t the function argument
     * @return the function result
     */
    R apply(T t);

    /**
     * Returns a composed function that first applies the {@code before}
     * function to its input, and then applies this function to the result.
     * If evaluation of either function throws an exception, it is relayed to
     * the caller of the composed function.
     *
     * @param <V> the type of input to the {@code before} function, and to the
     *           composed function
     * @param before the function to apply before this function is applied
     * @return a composed function that first applies the {@code before}
     * function and then applies this function
     * @throws NullPointerException if before is null
     *
     * @see #andThen(Function)
     */
    default <V> Function<V, R> compose(Function<? super V, ? extends T> before) {
        Objects.requireNonNull(before);
        return (V v) -> apply(before.apply(v));
    }

    /**
     * Returns a composed function that first applies this function to
     * its input, and then applies the {@code after} function to the result.
     * If evaluation of either function throws an exception, it is relayed to
     * the caller of the composed function.
     *
     * @param <V> the type of output of the {@code after} function, and of the
     *           composed function
     * @param after the function to apply after this function is applied
     * @return a composed function that first applies this function and then
     * applies the {@code after} function
     * @throws NullPointerException if after is null
     *
     * @see #compose(Function)
     */
    default <V> Function<T, V> andThen(Function<? super R, ? extends V> after) {
        Objects.requireNonNull(after);
        return (T t) -> after.apply(apply(t));
    }

    /**
     * Returns a function that always returns its input argument.
     *
     * @param <T> the type of the input and output objects to the function
     * @return a function that always returns its input argument
     */
    static <T> Function<T, T> identity() {
        return t -> t;
    }
}
```





使用Lambda表达式将字符串转成数字

```java
package mao;

import java.util.function.Function;

/**
 * Project name(项目名称)：JDK8_FunctionalInterface
 * Package(包名): mao
 * Class(类名): Test4
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/20
 * Time(创建时间)： 18:42
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test4
{
    public static void main(String[] args)
    {
        test(s -> Integer.parseInt(s));
    }

    private static void test(Function<String, Integer> function)
    {
        Integer integer = function.apply("112");
        System.out.println(integer);
    }
}
```





### Predicate接口

有时候我们需要对某种类型的数据进行判断，从而得到一个boolean值结果。这时可以使用Predicate接口

```java
/*
 * Copyright (c) 2010, 2013, Oracle and/or its affiliates. All rights reserved.
 * DO NOT ALTER OR REMOVE COPYRIGHT NOTICES OR THIS FILE HEADER.
 *
 * This code is free software; you can redistribute it and/or modify it
 * under the terms of the GNU General Public License version 2 only, as
 * published by the Free Software Foundation.  Oracle designates this
 * particular file as subject to the "Classpath" exception as provided
 * by Oracle in the LICENSE file that accompanied this code.
 *
 * This code is distributed in the hope that it will be useful, but WITHOUT
 * ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or
 * FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License
 * version 2 for more details (a copy is included in the LICENSE file that
 * accompanied this code).
 *
 * You should have received a copy of the GNU General Public License version
 * 2 along with this work; if not, write to the Free Software Foundation,
 * Inc., 51 Franklin St, Fifth Floor, Boston, MA 02110-1301 USA.
 *
 * Please contact Oracle, 500 Oracle Parkway, Redwood Shores, CA 94065 USA
 * or visit www.oracle.com if you need additional information or have any
 * questions.
 */
package java.util.function;

import java.util.Objects;

/**
 * Represents a predicate (boolean-valued function) of one argument.
 *
 * <p>This is a <a href="package-summary.html">functional interface</a>
 * whose functional method is {@link #test(Object)}.
 *
 * @param <T> the type of the input to the predicate
 *
 * @since 1.8
 */
@FunctionalInterface
public interface Predicate<T> {

    /**
     * Evaluates this predicate on the given argument.
     *
     * @param t the input argument
     * @return {@code true} if the input argument matches the predicate,
     * otherwise {@code false}
     */
    boolean test(T t);

    /**
     * Returns a composed predicate that represents a short-circuiting logical
     * AND of this predicate and another.  When evaluating the composed
     * predicate, if this predicate is {@code false}, then the {@code other}
     * predicate is not evaluated.
     *
     * <p>Any exceptions thrown during evaluation of either predicate are relayed
     * to the caller; if evaluation of this predicate throws an exception, the
     * {@code other} predicate will not be evaluated.
     *
     * @param other a predicate that will be logically-ANDed with this
     *              predicate
     * @return a composed predicate that represents the short-circuiting logical
     * AND of this predicate and the {@code other} predicate
     * @throws NullPointerException if other is null
     */
    default Predicate<T> and(Predicate<? super T> other) {
        Objects.requireNonNull(other);
        return (t) -> test(t) && other.test(t);
    }

    /**
     * Returns a predicate that represents the logical negation of this
     * predicate.
     *
     * @return a predicate that represents the logical negation of this
     * predicate
     */
    default Predicate<T> negate() {
        return (t) -> !test(t);
    }

    /**
     * Returns a composed predicate that represents a short-circuiting logical
     * OR of this predicate and another.  When evaluating the composed
     * predicate, if this predicate is {@code true}, then the {@code other}
     * predicate is not evaluated.
     *
     * <p>Any exceptions thrown during evaluation of either predicate are relayed
     * to the caller; if evaluation of this predicate throws an exception, the
     * {@code other} predicate will not be evaluated.
     *
     * @param other a predicate that will be logically-ORed with this
     *              predicate
     * @return a composed predicate that represents the short-circuiting logical
     * OR of this predicate and the {@code other} predicate
     * @throws NullPointerException if other is null
     */
    default Predicate<T> or(Predicate<? super T> other) {
        Objects.requireNonNull(other);
        return (t) -> test(t) || other.test(t);
    }

    /**
     * Returns a predicate that tests if two arguments are equal according
     * to {@link Objects#equals(Object, Object)}.
     *
     * @param <T> the type of arguments to the predicate
     * @param targetRef the object reference with which to compare for equality,
     *               which may be {@code null}
     * @return a predicate that tests if two arguments are equal according
     * to {@link Objects#equals(Object, Object)}
     */
    static <T> Predicate<T> isEqual(Object targetRef) {
        return (null == targetRef)
                ? Objects::isNull
                : object -> targetRef.equals(object);
    }
}
```





```java
package mao;

import java.util.function.Predicate;

/**
 * Project name(项目名称)：JDK8_FunctionalInterface
 * Package(包名): mao
 * Class(类名): Test5
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/20
 * Time(创建时间)： 18:54
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test5
{
    public static void main(String[] args)
    {
        test(s -> s.equals("hello"));
        test(s -> s.contains("c"));
    }

    private static void test(Predicate<String> predicate)
    {
        boolean b = predicate.test("hello");
        System.out.println(b);
    }
}
```





默认方法and、or、negate：既然是条件判断，就会存在与、或、非三种常见的逻辑关系。其中将两个Predicate条件使用“与”逻辑连接起来实现“并且”的效果时，可以使用default方法and，or、negate同理。









## 方法引用

### 传统写法

```java
package mao;

import java.util.ArrayList;
import java.util.List;
import java.util.function.Consumer;

/**
 * Project name(项目名称)：JDK8_method_reference
 * Package(包名): mao
 * Class(类名): Test1
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/23
 * Time(创建时间)： 15:30
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test1
{
    public static void main(String[] args)
    {
        List<Student> studentList = new ArrayList<>(4);
        studentList.add(new Student()
                .setId(1L)
                .setName("测试1")
                .setAge(13));
        studentList.add(new Student()
                .setId(2L)
                .setName("测试2")
                .setAge(12));
        studentList.add(new Student()
                .setId(3L)
                .setName("测试3")
                .setAge(19));
        studentList.add(new Student()
                .setId(4L)
                .setName("测试4")
                .setAge(8));
        studentList.sort((o1, o2) -> o1.getAge() - o2.getAge());
        System.out.println(studentList);
    }

}
```







### 方法引用

```java
package mao;

import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

/**
 * Project name(项目名称)：JDK8_method_reference
 * Package(包名): mao
 * Class(类名): Test2
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/23
 * Time(创建时间)： 15:40
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test2
{
    public static void main(String[] args)
    {
        List<Student> studentList = new ArrayList<>(4);
        studentList.add(new Student()
                .setId(1L)
                .setName("测试1")
                .setAge(13));
        studentList.add(new Student()
                .setId(2L)
                .setName("测试2")
                .setAge(12));
        studentList.add(new Student()
                .setId(3L)
                .setName("测试3")
                .setAge(19));
        studentList.add(new Student()
                .setId(4L)
                .setName("测试4")
                .setAge(8));
        studentList.sort(Comparator.comparingInt(Student::getAge));
        System.out.println(studentList);
    }
}
```



也可以更改成：

```java
package mao;

import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

/**
 * Project name(项目名称)：JDK8_method_reference
 * Package(包名): mao
 * Class(类名): Test3
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/23
 * Time(创建时间)： 15:41
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test3
{
    public static void main(String[] args)
    {
        List<Student> studentList = new ArrayList<>(4);
        studentList.add(new Student()
                .setId(1L)
                .setName("测试1")
                .setAge(13));
        studentList.add(new Student()
                .setId(2L)
                .setName("测试2")
                .setAge(12));
        studentList.add(new Student()
                .setId(3L)
                .setName("测试3")
                .setAge(19));
        studentList.add(new Student()
                .setId(4L)
                .setName("测试4")
                .setAge(8));
        studentList.sort(Test3::compare);
        System.out.println(studentList);
    }

    private static int compare(Student o1, Student o2)
    {
        return o1.getAge() - o2.getAge();
    }
}
```





双冒号::写法，这被称为**方法引用**





### 格式

* 符号表示 : **::**
* 符号说明 : 双冒号为方法引用运算符，而它所在的表达式被称为方法引用
* 应用场景 : 如果Lambda所要实现的方案 , 已经有其他方法存在相同方案，那么则可以使用方法引用





### 引用方式

有以下几种形式：

* **instanceName::methodName**  ：对象::方法名
* **ClassName::staticMethodName**  ：类名::静态方法
* **ClassName::methodName**  ： 类名::普通方法
* **ClassName::new**  ： 类名::new 调用的构造器
* **TypeName[]::new**  ： String[]::new 调用数组的构造器







### 对象名::方法名

```java
package mao;

import java.util.Date;
import java.util.function.Supplier;

/**
 * Project name(项目名称)：JDK8_method_reference
 * Package(包名): mao
 * Class(类名): Test4
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/23
 * Time(创建时间)： 15:48
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test4
{
    public static void main(String[] args)
    {
        Date now = new Date();
        Supplier<Long> supplier = now::getTime;
        System.out.println(supplier.get());
    }
}
```



* 被引用的方法，参数要和接口中抽象方法的参数一样
* 当接口抽象方法有返回值时，被引用的方法也必须有返回值





### 类名::静态方法

```java
package mao;

import java.util.Date;
import java.util.function.Supplier;

/**
 * Project name(项目名称)：JDK8_method_reference
 * Package(包名): mao
 * Class(类名): Test5
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/23
 * Time(创建时间)： 15:53
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test5
{
    public static void main(String[] args)
    {
        Supplier<Long> supplier = System::currentTimeMillis;
        System.out.println(supplier.get());
    }
}
```





### 类名::普通方法

类名只能调用静态方法，类名引用实例方法是有前提的，实际上是拿第一个参数作为方法的调用者

```java
package mao;

import java.util.function.BiFunction;
import java.util.function.Function;

/**
 * Project name(项目名称)：JDK8_method_reference
 * Package(包名): mao
 * Class(类名): Test6
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/23
 * Time(创建时间)： 15:56
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test6
{
    public static void main(String[] args)
    {
        Function<String, Integer> f1 = (s) ->
        {
            return s.length();
        };
        System.out.println(f1.apply("abc"));
        Function<String, Integer> f2 = String::length;
        System.out.println(f2.apply("abc"));
        BiFunction<String, Integer, String> bif = String::substring;
        String hello = bif.apply("hello", 2);
        System.out.println("hello = " + hello);
    }
}
```







### 类名::new引用构造器

```java
package mao;

import java.util.function.Supplier;

/**
 * Project name(项目名称)：JDK8_method_reference
 * Package(包名): mao
 * Class(类名): Test7
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/23
 * Time(创建时间)： 15:59
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test7
{
    public static void main(String[] args)
    {
        Supplier<Test7> supplier = Test7::new;
        supplier.get().hello();
    }

    public void hello()
    {
        System.out.println("hello!");
    }
}
```





### 数组::new引用数组构造器

```java
package mao;

import java.util.Arrays;
import java.util.function.Function;

/**
 * Project name(项目名称)：JDK8_method_reference
 * Package(包名): mao
 * Class(类名): Test8
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/23
 * Time(创建时间)： 16:03
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test8
{
    public static void main(String[] args)
    {
        Function<Integer, String[]> fun = (len) ->
        {
            return new String[len];
        };
        String[] arr1 = fun.apply(10);
        System.out.println(Arrays.toString(arr1) + ", " + arr1.length);
        Function<Integer, String[]> fun2 = String[]::new;
        String[] arr2 = fun.apply(5);
        System.out.println(Arrays.toString(arr2) + ", " + arr2.length);
    }
}
```









## Stream流

### 概述

Stream流式思想类似于工厂车间的“**生产流水线**”，Stream流不是一种数据结构，不保存数据，而是对数据进行加工处理。Stream可以看作是流水线上的一个工序。在流水线上，通过多个工序让一个原材料加工成一个商品

Stream API能让我们快速完成许多复杂的操作，如筛选、切片、映射、查找、去除重复，统计，匹配和归约





### 集合处理数据的弊端

当我们需要对集合中的元素进行操作的时候，除了必需的添加、删除、获取外，最典型的就是集合遍历。我们来体验集合操作数据的弊端



需求如下：

* 一个 ArrayList集合中存储有以下数据:张无忌,周芷若,赵敏,张强,张三丰
* 拿到所有姓张的
* 拿到名字长度为3个字的
* 打印这些数据



```java
package mao;

import java.util.ArrayList;
import java.util.Collections;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test1
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/23
 * Time(创建时间)： 18:31
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test1
{
    public static void main(String[] args)
    {
        ArrayList<String> list = new ArrayList<>();
        Collections.addAll(list, "张无忌", "周芷若", "赵敏", "张强", "张三丰");
        //拿到所有姓张的
        ArrayList<String> zhangList = new ArrayList<>();
        for (String name : list)
        {
            if (name.startsWith("张"))
            {
                zhangList.add(name);
            }
        }

        //拿到名字长度为3个字的
        ArrayList<String> threeList = new ArrayList<>();
        for (String name : zhangList)
        {
            if (name.length() == 3)
            {
                threeList.add(name);
            }
        }
        //打印这些数据
        for (String name : threeList)
        {
            System.out.println(name);
        }
    }
}

```





### Stream写法

```java
package mao;

import java.util.ArrayList;
import java.util.Collections;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test2
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/25
 * Time(创建时间)： 15:24
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test2
{
    public static void main(String[] args)
    {
        ArrayList<String> list = new ArrayList<>();
        Collections.addAll(list, "张无忌", "周芷若", "赵敏", "张强", "张三丰");
        list.stream()
                .filter(s -> s.startsWith("张"))
                .filter(s -> s.length() == 3)
                .forEach(System.out::println);
    }
}
```







### 获取Stream流

两种方式：

* **方式1** : 根据Collection获取流
* **方式2** : Stream中的静态方法of获取流





#### 方式1

java.util.Collection 接口中加入了default方法stream 用来获取流，所以其所有实现类均可获取流

Map接口不是Collection的子接口，所以获取对应的流需要分key、value或entry等情况

```java
public interface Collection<E> extends Iterable<E> {
    /**
     * Returns a sequential {@code Stream} with this collection as its source.
     *
     * <p>This method should be overridden when the {@link #spliterator()}
     * method cannot return a spliterator that is {@code IMMUTABLE},
     * {@code CONCURRENT}, or <em>late-binding</em>. (See {@link #spliterator()}
     * for details.)
     *
     * @implSpec
     * The default implementation creates a sequential {@code Stream} from the
     * collection's {@code Spliterator}.
     *
     * @return a sequential {@code Stream} over the elements in this collection
     * @since 1.8
     */
    default Stream<E> stream() {
        return StreamSupport.stream(spliterator(), false);
    }
}
```





```java
package mao;

import java.util.*;
import java.util.stream.Stream;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test3
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/25
 * Time(创建时间)： 15:34
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test3
{
    public static void main(String[] args)
    {
        List<String> list = new ArrayList<>();
        Stream<String> stream = list.stream();
        List<Long> longList = new LinkedList<>();
        Stream<Long> longStream = longList.stream();
        Set<String> stringSet = new HashSet<>();
        Stream<String> stringStream = stringSet.stream();
        //Map接口不是Collection的子接口，所以获取对应的流需要分key、value或entry等情况
        Map<String, Long> map = new HashMap<>();
        Stream<String> stream1 = map.keySet().stream();
        Stream<Long> stream2 = map.values().stream();
        Stream<Map.Entry<String, Long>> stream3 = map.entrySet().stream();
    }
}
```







#### 方式2

由于数组对象不可能添加默认方法，所以Stream接口中提供了静态方法of

```java
public interface Stream<T> extends BaseStream<T, Stream<T>> {
    /**
     * Returns a sequential {@code Stream} containing a single element.
     *
     * @param t the single element
     * @param <T> the type of stream elements
     * @return a singleton sequential stream
     */
    public static<T> Stream<T> of(T t) {
        return StreamSupport.stream(new Streams.StreamBuilderImpl<>(t), false);
    }

    /**
     * Returns a sequential ordered stream whose elements are the specified values.
     *
     * @param <T> the type of stream elements
     * @param values the elements of the new stream
     * @return the new stream
     */
    @SafeVarargs
    @SuppressWarnings("varargs") // Creating a stream from an array is safe
    public static<T> Stream<T> of(T... values) {
        return Arrays.stream(values);
    }
}
```



```java
package mao;

import java.util.stream.Stream;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test4
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/25
 * Time(创建时间)： 15:40
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test4
{
    public static void main(String[] args)
    {
        Stream<String> stringStream = Stream.of("1", "2", "3");
    }
}
```







### Stream常用方法

* count：统计个数
* forEach：逐一处理
* filter：过滤
* limit：取用前几个
* skip：跳过前几个
* map：映射
* concat：组合





### forEach方法

forEach 用来遍历流中的数据

```java

    /**
     * Performs an action for each element of this stream.
     *
     * <p>This is a <a href="package-summary.html#StreamOps">terminal
     * operation</a>.
     *
     * <p>The behavior of this operation is explicitly nondeterministic.
     * For parallel stream pipelines, this operation does <em>not</em>
     * guarantee to respect the encounter order of the stream, as doing so
     * would sacrifice the benefit of parallelism.  For any given element, the
     * action may be performed at whatever time and in whatever thread the
     * library chooses.  If the action accesses shared state, it is
     * responsible for providing the required synchronization.
     *
     * @param action a <a href="package-summary.html#NonInterference">
     *               non-interfering</a> action to perform on the elements
     */
    void forEach(Consumer<? super T> action);
```



该方法接收一个Consumer接口函数，会将每一个流元素交给该函数进行处理



```java
package mao;

import java.util.ArrayList;
import java.util.List;
import java.util.function.Consumer;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test5
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/25
 * Time(创建时间)： 15:49
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test5
{
    public static void main(String[] args)
    {
        List<String> list=new ArrayList<>(5);
        list.add("1");
        list.add("2");
        list.add("3");
        list.add("4");
        list.add("5");
        list.stream().forEach(System.out::println);
        //list.forEach(System.out::println);

        list.stream().forEach(new Consumer<String>()
        {
            @Override
            public void accept(String s)
            {
                System.out.println(s);
            }
        });
    }
}

```





### count方法

统计其中的元素个数

```java
    /**
     * Returns the count of elements in this stream.  This is a special case of
     * a <a href="package-summary.html#Reduction">reduction</a> and is
     * equivalent to:
     * <pre>{@code
     *     return mapToLong(e -> 1L).sum();
     * }</pre>
     *
     * <p>This is a <a href="package-summary.html#StreamOps">terminal operation</a>.
     *
     * @return the count of elements in this stream
     */
    long count();
```



该方法返回一个long值代表元素个数

```java
package mao;

import java.util.ArrayList;
import java.util.List;
import java.util.stream.Stream;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test6
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/25
 * Time(创建时间)： 15:55
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test6
{
    public static void main(String[] args)
    {
        List<String> list = new ArrayList<>(5);
        list.add("1");
        list.add("2");
        list.add("3");
        list.add("4");
        list.add("5");
        System.out.println(list.stream().count());
        System.out.println(list.size());
        list.add("6");
        System.out.println(list.stream().count());
        System.out.println(list.size());
        Stream<String> stream = list.stream();
        list.add("7");
        System.out.println(stream.count());
    }
}
```



```sh
5
5
6
6
7
```







### filter方法

filter用于过滤数据，返回符合过滤条件的数据，可以通过filter方法将一个流转换成另一个子集流

```java

    /**
     * Returns a stream consisting of the elements of this stream that match
     * the given predicate.
     *
     * <p>This is an <a href="package-summary.html#StreamOps">intermediate
     * operation</a>.
     *
     * @param predicate a <a href="package-summary.html#NonInterference">non-interfering</a>,
     *                  <a href="package-summary.html#Statelessness">stateless</a>
     *                  predicate to apply to each element to determine if it
     *                  should be included
     * @return the new stream
     */
    Stream<T> filter(Predicate<? super T> predicate);
```



```java
package mao;

import java.util.ArrayList;
import java.util.List;
import java.util.function.Predicate;
import java.util.stream.Stream;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test7
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/25
 * Time(创建时间)： 16:01
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test7
{
    public static void main(String[] args)
    {
        List<String> list = new ArrayList<>(5);
        list.add("1");
        list.add("2");
        list.add("3");
        list.add("4");
        list.add("5");
        //只要2和5
        Stream<String> stream = list.stream().filter(new Predicate<String>()
        {
            @Override
            public boolean test(String s)
            {
                if (s.equals("2") || s.equals("5"))
                {
                    return true;
                }
                return false;
            }
        });
        stream.forEach(System.out::println);
    }
}
```



```sh
2
5
```



```java
package mao;

import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test8
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/25
 * Time(创建时间)： 16:04
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test8
{
    public static void main(String[] args)
    {
        List<String> list = new ArrayList<>();
        List<String> collect = list.stream().filter(s -> s.length() >= 3)
                .filter(s -> s.length() <= 10)
                .filter(s -> s.endsWith("]"))
                .filter(s -> s.startsWith("["))
                .collect(Collectors.toList());
    }
}
```





### limit方法

limit 方法可以对流进行截取，只取用前n个

```java
/**
 * Returns a stream consisting of the elements of this stream, truncated
 * to be no longer than {@code maxSize} in length.
 *
 * <p>This is a <a href="package-summary.html#StreamOps">short-circuiting
 * stateful intermediate operation</a>.
 *
 * @apiNote
 * While {@code limit()} is generally a cheap operation on sequential
 * stream pipelines, it can be quite expensive on ordered parallel pipelines,
 * especially for large values of {@code maxSize}, since {@code limit(n)}
 * is constrained to return not just any <em>n</em> elements, but the
 * <em>first n</em> elements in the encounter order.  Using an unordered
 * stream source (such as {@link #generate(Supplier)}) or removing the
 * ordering constraint with {@link #unordered()} may result in significant
 * speedups of {@code limit()} in parallel pipelines, if the semantics of
 * your situation permit.  If consistency with encounter order is required,
 * and you are experiencing poor performance or memory utilization with
 * {@code limit()} in parallel pipelines, switching to sequential execution
 * with {@link #sequential()} may improve performance.
 *
 * @param maxSize the number of elements the stream should be limited to
 * @return the new stream
 * @throws IllegalArgumentException if {@code maxSize} is negative
 */
Stream<T> limit(long maxSize);
```





```java
package mao;

import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test9
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/25
 * Time(创建时间)： 16:09
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test9
{
    public static void main(String[] args)
    {
        List<Integer> list = new ArrayList<>(100);
        for (int i = 0; i < 100; i++)
        {
            list.add(i);
        }
        System.out.println(list.stream().limit(5).collect(Collectors.toList()));
        System.out.println(list.stream().limit(10).collect(Collectors.toList()));
        System.out.println(list.stream().limit(20).collect(Collectors.toList()));
        System.out.println(list.stream().limit(1).collect(Collectors.toList()));
        System.out.println(list.stream().limit(0).collect(Collectors.toList()));
        System.out.println(list.stream().limit(300).collect(Collectors.toList()));
    }
}
```



```sh
[0, 1, 2, 3, 4]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19]
[0]
[]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99]
```





### skip方法

如果希望跳过前几个元素，可以使用此方法获取一个截取之后的新流

```java
    /**
     * Returns a stream consisting of the remaining elements of this stream
     * after discarding the first {@code n} elements of the stream.
     * If this stream contains fewer than {@code n} elements then an
     * empty stream will be returned.
     *
     * <p>This is a <a href="package-summary.html#StreamOps">stateful
     * intermediate operation</a>.
     *
     * @apiNote
     * While {@code skip()} is generally a cheap operation on sequential
     * stream pipelines, it can be quite expensive on ordered parallel pipelines,
     * especially for large values of {@code n}, since {@code skip(n)}
     * is constrained to skip not just any <em>n</em> elements, but the
     * <em>first n</em> elements in the encounter order.  Using an unordered
     * stream source (such as {@link #generate(Supplier)}) or removing the
     * ordering constraint with {@link #unordered()} may result in significant
     * speedups of {@code skip()} in parallel pipelines, if the semantics of
     * your situation permit.  If consistency with encounter order is required,
     * and you are experiencing poor performance or memory utilization with
     * {@code skip()} in parallel pipelines, switching to sequential execution
     * with {@link #sequential()} may improve performance.
     *
     * @param n the number of leading elements to skip
     * @return the new stream
     * @throws IllegalArgumentException if {@code n} is negative
     */
    Stream<T> skip(long n);
```



```java
package mao;

import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test10
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/25
 * Time(创建时间)： 16:13
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test10
{
    public static void main(String[] args)
    {
        List<Integer> list = new ArrayList<>(100);
        for (int i = 0; i < 100; i++)
        {
            list.add(i);
        }
        System.out.println(list.stream().skip(80).collect(Collectors.toList()));
        System.out.println(list.stream().skip(95).collect(Collectors.toList()));
        System.out.println(list.stream().skip(100).collect(Collectors.toList()));
        System.out.println(list.stream().skip(99).collect(Collectors.toList()));
        System.out.println(list.stream().skip(101).collect(Collectors.toList()));
        System.out.println(list.stream().skip(0).collect(Collectors.toList()));
    }
}
```



```sh
[80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99]
[95, 96, 97, 98, 99]
[]
[99]
[]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99]
```







### map方法

如果需要将流中的元素映射到另一个流中，可以使用 map 方法

```java
/**
     * Returns a stream consisting of the results of applying the given
     * function to the elements of this stream.
     *
     * <p>This is an <a href="package-summary.html#StreamOps">intermediate
     * operation</a>.
     *
     * @param <R> The element type of the new stream
     * @param mapper a <a href="package-summary.html#NonInterference">non-interfering</a>,
     *               <a href="package-summary.html#Statelessness">stateless</a>
     *               function to apply to each element
     * @return the new stream
     */
    <R> Stream<R> map(Function<? super T, ? extends R> mapper);
```



可以将当前流中的T类型数据转换为另一种R类型的流



```java
package mao;

import java.util.ArrayList;
import java.util.List;
import java.util.Map;
import java.util.function.Consumer;
import java.util.function.Function;
import java.util.stream.Collectors;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test11
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/26
 * Time(创建时间)： 10:33
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test11
{
    public static void main(String[] args)
    {
        List<String> list = new ArrayList<>();
        list.add("3");
        list.add("2");
        list.add("9");
        List<Long> longList = list.stream().map(new Function<String, Long>()
        {
            @Override
            public Long apply(String s)
            {
                return Long.parseLong(s);
            }
        }).collect(Collectors.toList());
        System.out.println(longList);
        list.stream().map(Long::parseLong).forEach(System.out::println);
    }
}
```



```sh
[3, 2, 9]
3
2
9
```





### sorted方法

如果需要将数据排序，可以使用sorted方法

```java
    /**
     * Returns a stream consisting of the elements of this stream, sorted
     * according to natural order.  If the elements of this stream are not
     * {@code Comparable}, a {@code java.lang.ClassCastException} may be thrown
     * when the terminal operation is executed.
     *
     * <p>For ordered streams, the sort is stable.  For unordered streams, no
     * stability guarantees are made.
     *
     * <p>This is a <a href="package-summary.html#StreamOps">stateful
     * intermediate operation</a>.
     *
     * @return the new stream
     */
    Stream<T> sorted();

    /**
     * Returns a stream consisting of the elements of this stream, sorted
     * according to the provided {@code Comparator}.
     *
     * <p>For ordered streams, the sort is stable.  For unordered streams, no
     * stability guarantees are made.
     *
     * <p>This is a <a href="package-summary.html#StreamOps">stateful
     * intermediate operation</a>.
     *
     * @param comparator a <a href="package-summary.html#NonInterference">non-interfering</a>,
     *                   <a href="package-summary.html#Statelessness">stateless</a>
     *                   {@code Comparator} to be used to compare stream elements
     * @return the new stream
     */
    Stream<T> sorted(Comparator<? super T> comparator);
```





```java
package mao;

import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;
import java.util.stream.Collectors;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test12
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/26
 * Time(创建时间)： 10:42
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test12
{
    public static void main(String[] args)
    {
        List<String> list = new ArrayList<>();
        list.add("3");
        list.add("2");
        list.add("9");
        list.add("4");
        System.out.println(list.stream().sorted().collect(Collectors.toList()));
        System.out.println(list.stream().sorted(new Comparator<String>()
        {
            @Override
            public int compare(String o1, String o2)
            {
                return o2.compareTo(o1);
            }
        }).collect(Collectors.toList()));
        System.out.println(list.stream().sorted(Comparator.reverseOrder()).collect(Collectors.toList()));
    }
}
```



```sh
[2, 3, 4, 9]
[9, 4, 3, 2]
[9, 4, 3, 2]
```





### distinct方法

如果需要去除重复数据，可以使用 distinct 方法

```java
    /**
     * Returns a stream consisting of the distinct elements (according to
     * {@link Object#equals(Object)}) of this stream.
     *
     * <p>For ordered streams, the selection of distinct elements is stable
     * (for duplicated elements, the element appearing first in the encounter
     * order is preserved.)  For unordered streams, no stability guarantees
     * are made.
     *
     * <p>This is a <a href="package-summary.html#StreamOps">stateful
     * intermediate operation</a>.
     *
     * @apiNote
     * Preserving stability for {@code distinct()} in parallel pipelines is
     * relatively expensive (requires that the operation act as a full barrier,
     * with substantial buffering overhead), and stability is often not needed.
     * Using an unordered stream source (such as {@link #generate(Supplier)})
     * or removing the ordering constraint with {@link #unordered()} may result
     * in significantly more efficient execution for {@code distinct()} in parallel
     * pipelines, if the semantics of your situation permit.  If consistency
     * with encounter order is required, and you are experiencing poor performance
     * or memory utilization with {@code distinct()} in parallel pipelines,
     * switching to sequential execution with {@link #sequential()} may improve
     * performance.
     *
     * @return the new stream
     */
    Stream<T> distinct();
```





```java
package mao;

import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test13
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/26
 * Time(创建时间)： 10:47
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test13
{
    public static void main(String[] args)
    {
        List<String> list = new ArrayList<>();
        list.add("3");
        list.add("2");
        list.add("9");
        list.add("9");
        list.add("2");
        System.out.println(list.stream().distinct().collect(Collectors.toList()));
    }
}
```



```sh
[3, 2, 9]
```





自定义类型是根据对象的hashCode和equals来去除重复元素的





### match方法

如果需要判断数据是否匹配指定的条件，可以使用 Match 相关方法

```java
/**
     * Returns whether any elements of this stream match the provided
     * predicate.  May not evaluate the predicate on all elements if not
     * necessary for determining the result.  If the stream is empty then
     * {@code false} is returned and the predicate is not evaluated.
     *
     * <p>This is a <a href="package-summary.html#StreamOps">short-circuiting
     * terminal operation</a>.
     *
     * @apiNote
     * This method evaluates the <em>existential quantification</em> of the
     * predicate over the elements of the stream (for some x P(x)).
     *
     * @param predicate a <a href="package-summary.html#NonInterference">non-interfering</a>,
     *                  <a href="package-summary.html#Statelessness">stateless</a>
     *                  predicate to apply to elements of this stream
     * @return {@code true} if any elements of the stream match the provided
     * predicate, otherwise {@code false}
     */
    boolean anyMatch(Predicate<? super T> predicate);

    /**
     * Returns whether all elements of this stream match the provided predicate.
     * May not evaluate the predicate on all elements if not necessary for
     * determining the result.  If the stream is empty then {@code true} is
     * returned and the predicate is not evaluated.
     *
     * <p>This is a <a href="package-summary.html#StreamOps">short-circuiting
     * terminal operation</a>.
     *
     * @apiNote
     * This method evaluates the <em>universal quantification</em> of the
     * predicate over the elements of the stream (for all x P(x)).  If the
     * stream is empty, the quantification is said to be <em>vacuously
     * satisfied</em> and is always {@code true} (regardless of P(x)).
     *
     * @param predicate a <a href="package-summary.html#NonInterference">non-interfering</a>,
     *                  <a href="package-summary.html#Statelessness">stateless</a>
     *                  predicate to apply to elements of this stream
     * @return {@code true} if either all elements of the stream match the
     * provided predicate or the stream is empty, otherwise {@code false}
     */
    boolean allMatch(Predicate<? super T> predicate);

    /**
     * Returns whether no elements of this stream match the provided predicate.
     * May not evaluate the predicate on all elements if not necessary for
     * determining the result.  If the stream is empty then {@code true} is
     * returned and the predicate is not evaluated.
     *
     * <p>This is a <a href="package-summary.html#StreamOps">short-circuiting
     * terminal operation</a>.
     *
     * @apiNote
     * This method evaluates the <em>universal quantification</em> of the
     * negated predicate over the elements of the stream (for all x ~P(x)).  If
     * the stream is empty, the quantification is said to be vacuously satisfied
     * and is always {@code true}, regardless of P(x).
     *
     * @param predicate a <a href="package-summary.html#NonInterference">non-interfering</a>,
     *                  <a href="package-summary.html#Statelessness">stateless</a>
     *                  predicate to apply to elements of this stream
     * @return {@code true} if either no elements of the stream match the
     * provided predicate or the stream is empty, otherwise {@code false}
     */
    boolean noneMatch(Predicate<? super T> predicate);
```



* allMatch: 元素是否全部满足条件
* anyMatch: 元素是否任意有一个满足条件
* noneMatch: 元素是否全部不满足条件



```java
package mao;

import java.util.ArrayList;
import java.util.List;
import java.util.function.Predicate;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test14
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/26
 * Time(创建时间)： 11:45
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test14
{
    public static void main(String[] args)
    {
        List<Integer> list = new ArrayList<>(100);
        for (int i = 0; i < 100; i++)
        {
            list.add(i);
        }
        System.out.println(list.stream().allMatch(new Predicate<Integer>()
        {
            @Override
            public boolean test(Integer integer)
            {
                return integer > 20;
            }
        }));
        System.out.println(list.stream().allMatch(integer -> integer > -2));
        System.out.println(list.stream().anyMatch(integer -> integer > 60));
        System.out.println(list.stream().anyMatch(integer -> integer > -3));
        System.out.println(list.stream().anyMatch(integer -> integer > 120));
        System.out.println(list.stream().noneMatch(integer -> integer > 60));
        System.out.println(list.stream().noneMatch(integer -> integer > -3));
        System.out.println(list.stream().noneMatch(integer -> integer > 120));
    }
}
```



```sh
false
true
true
true
false
false
false
true
```





### find方法

如果需要找到某些数据，可以使用 find方法

```java

    /**
     * Returns an {@link Optional} describing the first element of this stream,
     * or an empty {@code Optional} if the stream is empty.  If the stream has
     * no encounter order, then any element may be returned.
     *
     * <p>This is a <a href="package-summary.html#StreamOps">short-circuiting
     * terminal operation</a>.
     *
     * @return an {@code Optional} describing the first element of this stream,
     * or an empty {@code Optional} if the stream is empty
     * @throws NullPointerException if the element selected is null
     */
    Optional<T> findFirst();

    /**
     * Returns an {@link Optional} describing some element of the stream, or an
     * empty {@code Optional} if the stream is empty.
     *
     * <p>This is a <a href="package-summary.html#StreamOps">short-circuiting
     * terminal operation</a>.
     *
     * <p>The behavior of this operation is explicitly nondeterministic; it is
     * free to select any element in the stream.  This is to allow for maximal
     * performance in parallel operations; the cost is that multiple invocations
     * on the same source may not return the same result.  (If a stable result
     * is desired, use {@link #findFirst()} instead.)
     *
     * @return an {@code Optional} describing some element of this stream, or an
     * empty {@code Optional} if the stream is empty
     * @throws NullPointerException if the element selected is null
     * @see #findFirst()
     */
    Optional<T> findAny();
```





### max和min方法

如果需要获取最大和最小值，可以使用 max 和min 方法

```java

    /**
     * Returns the minimum element of this stream according to the provided
     * {@code Comparator}.  This is a special case of a
     * <a href="package-summary.html#Reduction">reduction</a>.
     *
     * <p>This is a <a href="package-summary.html#StreamOps">terminal operation</a>.
     *
     * @param comparator a <a href="package-summary.html#NonInterference">non-interfering</a>,
     *                   <a href="package-summary.html#Statelessness">stateless</a>
     *                   {@code Comparator} to compare elements of this stream
     * @return an {@code Optional} describing the minimum element of this stream,
     * or an empty {@code Optional} if the stream is empty
     * @throws NullPointerException if the minimum element is null
     */
    Optional<T> min(Comparator<? super T> comparator);

    /**
     * Returns the maximum element of this stream according to the provided
     * {@code Comparator}.  This is a special case of a
     * <a href="package-summary.html#Reduction">reduction</a>.
     *
     * <p>This is a <a href="package-summary.html#StreamOps">terminal
     * operation</a>.
     *
     * @param comparator a <a href="package-summary.html#NonInterference">non-interfering</a>,
     *                   <a href="package-summary.html#Statelessness">stateless</a>
     *                   {@code Comparator} to compare elements of this stream
     * @return an {@code Optional} describing the maximum element of this stream,
     * or an empty {@code Optional} if the stream is empty
     * @throws NullPointerException if the maximum element is null
     */
    Optional<T> max(Comparator<? super T> comparator);
```



```java
package mao;

import java.util.*;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test16
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/26
 * Time(创建时间)： 12:02
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test16
{
    public static void main(String[] args)
    {
        List<Integer> list = new ArrayList<>(100);
        for (int i = 1000; i < 1100; i++)
        {
            list.add(i);
        }
        Collections.shuffle(list);
        System.out.println(list);
        System.out.println(list.stream().max(new Comparator<Integer>()
        {
            @Override
            public int compare(Integer o1, Integer o2)
            {
                return o1-o2;
            }
        }).get());
        System.out.println(list.stream().min(new Comparator<Integer>()
        {
            @Override
            public int compare(Integer o1, Integer o2)
            {
                return o1-o2;
            }
        }).get());
    }
}
```



```sh
[1046, 1052, 1042, 1036, 1099, 1041, 1027, 1007, 1092, 1047, 1093, 1040, 1054, 1075, 1003, 1016, 1008, 1070, 1051, 1056, 1095, 1065, 1029, 1096, 1017, 1067, 1073, 1038, 1055, 1000, 1062, 1071, 1044, 1066, 1002, 1085, 1079, 1020, 1048, 1053, 1023, 1068, 1082, 1035, 1022, 1045, 1012, 1034, 1050, 1074, 1009, 1043, 1057, 1024, 1059, 1086, 1049, 1037, 1089, 1063, 1013, 1077, 1090, 1058, 1001, 1033, 1097, 1010, 1011, 1069, 1061, 1088, 1026, 1018, 1091, 1094, 1028, 1014, 1019, 1084, 1031, 1004, 1083, 1006, 1081, 1025, 1030, 1064, 1039, 1060, 1072, 1098, 1015, 1005, 1078, 1032, 1080, 1021, 1087, 1076]
1099
1000
```







### reduce方法

如果需要将所有数据归纳得到一个数据，可以使用reduce方法

```java

    /**
     * Performs a <a href="package-summary.html#Reduction">reduction</a> on the
     * elements of this stream, using the provided identity value and an
     * <a href="package-summary.html#Associativity">associative</a>
     * accumulation function, and returns the reduced value.  This is equivalent
     * to:
     * <pre>{@code
     *     T result = identity;
     *     for (T element : this stream)
     *         result = accumulator.apply(result, element)
     *     return result;
     * }</pre>
     *
     * but is not constrained to execute sequentially.
     *
     * <p>The {@code identity} value must be an identity for the accumulator
     * function. This means that for all {@code t},
     * {@code accumulator.apply(identity, t)} is equal to {@code t}.
     * The {@code accumulator} function must be an
     * <a href="package-summary.html#Associativity">associative</a> function.
     *
     * <p>This is a <a href="package-summary.html#StreamOps">terminal
     * operation</a>.
     *
     * @apiNote Sum, min, max, average, and string concatenation are all special
     * cases of reduction. Summing a stream of numbers can be expressed as:
     *
     * <pre>{@code
     *     Integer sum = integers.reduce(0, (a, b) -> a+b);
     * }</pre>
     *
     * or:
     *
     * <pre>{@code
     *     Integer sum = integers.reduce(0, Integer::sum);
     * }</pre>
     *
     * <p>While this may seem a more roundabout way to perform an aggregation
     * compared to simply mutating a running total in a loop, reduction
     * operations parallelize more gracefully, without needing additional
     * synchronization and with greatly reduced risk of data races.
     *
     * @param identity the identity value for the accumulating function
     * @param accumulator an <a href="package-summary.html#Associativity">associative</a>,
     *                    <a href="package-summary.html#NonInterference">non-interfering</a>,
     *                    <a href="package-summary.html#Statelessness">stateless</a>
     *                    function for combining two values
     * @return the result of the reduction
     */
    T reduce(T identity, BinaryOperator<T> accumulator);

    /**
     * Performs a <a href="package-summary.html#Reduction">reduction</a> on the
     * elements of this stream, using an
     * <a href="package-summary.html#Associativity">associative</a> accumulation
     * function, and returns an {@code Optional} describing the reduced value,
     * if any. This is equivalent to:
     * <pre>{@code
     *     boolean foundAny = false;
     *     T result = null;
     *     for (T element : this stream) {
     *         if (!foundAny) {
     *             foundAny = true;
     *             result = element;
     *         }
     *         else
     *             result = accumulator.apply(result, element);
     *     }
     *     return foundAny ? Optional.of(result) : Optional.empty();
     * }</pre>
     *
     * but is not constrained to execute sequentially.
     *
     * <p>The {@code accumulator} function must be an
     * <a href="package-summary.html#Associativity">associative</a> function.
     *
     * <p>This is a <a href="package-summary.html#StreamOps">terminal
     * operation</a>.
     *
     * @param accumulator an <a href="package-summary.html#Associativity">associative</a>,
     *                    <a href="package-summary.html#NonInterference">non-interfering</a>,
     *                    <a href="package-summary.html#Statelessness">stateless</a>
     *                    function for combining two values
     * @return an {@link Optional} describing the result of the reduction
     * @throws NullPointerException if the result of the reduction is null
     * @see #reduce(Object, BinaryOperator)
     * @see #min(Comparator)
     * @see #max(Comparator)
     */
    Optional<T> reduce(BinaryOperator<T> accumulator);

    /**
     * Performs a <a href="package-summary.html#Reduction">reduction</a> on the
     * elements of this stream, using the provided identity, accumulation and
     * combining functions.  This is equivalent to:
     * <pre>{@code
     *     U result = identity;
     *     for (T element : this stream)
     *         result = accumulator.apply(result, element)
     *     return result;
     * }</pre>
     *
     * but is not constrained to execute sequentially.
     *
     * <p>The {@code identity} value must be an identity for the combiner
     * function.  This means that for all {@code u}, {@code combiner(identity, u)}
     * is equal to {@code u}.  Additionally, the {@code combiner} function
     * must be compatible with the {@code accumulator} function; for all
     * {@code u} and {@code t}, the following must hold:
     * <pre>{@code
     *     combiner.apply(u, accumulator.apply(identity, t)) == accumulator.apply(u, t)
     * }</pre>
     *
     * <p>This is a <a href="package-summary.html#StreamOps">terminal
     * operation</a>.
     *
     * @apiNote Many reductions using this form can be represented more simply
     * by an explicit combination of {@code map} and {@code reduce} operations.
     * The {@code accumulator} function acts as a fused mapper and accumulator,
     * which can sometimes be more efficient than separate mapping and reduction,
     * such as when knowing the previously reduced value allows you to avoid
     * some computation.
     *
     * @param <U> The type of the result
     * @param identity the identity value for the combiner function
     * @param accumulator an <a href="package-summary.html#Associativity">associative</a>,
     *                    <a href="package-summary.html#NonInterference">non-interfering</a>,
     *                    <a href="package-summary.html#Statelessness">stateless</a>
     *                    function for incorporating an additional element into a result
     * @param combiner an <a href="package-summary.html#Associativity">associative</a>,
     *                    <a href="package-summary.html#NonInterference">non-interfering</a>,
     *                    <a href="package-summary.html#Statelessness">stateless</a>
     *                    function for combining two values, which must be
     *                    compatible with the accumulator function
     * @return the result of the reduction
     * @see #reduce(BinaryOperator)
     * @see #reduce(Object, BinaryOperator)
     */
    <U> U reduce(U identity,
                 BiFunction<U, ? super T, U> accumulator,
                 BinaryOperator<U> combiner);
```





```java
package mao;

import java.util.function.BinaryOperator;
import java.util.stream.Stream;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test17
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/26
 * Time(创建时间)： 16:26
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test17
{
    public static void main(String[] args)
    {
        int reduce = Stream.of(4, 5, 3, 9)
                .reduce(0, (a, b) ->
                {
                    System.out.println("a = " + a + ", b = " + b);
                    return a + b;
                });
        int reduce2 = Stream.of(4, 5, 3, 9)
                .reduce(0, Integer::sum);
        int max = Stream.of(4, 5, 3, 9)
                .reduce(0, (x, y) -> x > y ? x : y);
        System.out.println(reduce);
        System.out.println(reduce2);
        System.out.println(max);
    }
}
```



```sh
a = 0, b = 4
a = 4, b = 5
a = 9, b = 3
a = 12, b = 9
21
21
9
```







### mapToInt方法

如果需要将Stream中的Integer类型数据转成int类型，可以使用mapToInt方法

```java

    /**
     * Returns an {@code IntStream} consisting of the results of applying the
     * given function to the elements of this stream.
     *
     * <p>This is an <a href="package-summary.html#StreamOps">
     *     intermediate operation</a>.
     *
     * @param mapper a <a href="package-summary.html#NonInterference">non-interfering</a>,
     *               <a href="package-summary.html#Statelessness">stateless</a>
     *               function to apply to each element
     * @return the new stream
     */
    IntStream mapToInt(ToIntFunction<? super T> mapper);
```



```java
package mao;

import java.util.ArrayList;
import java.util.List;
import java.util.function.IntConsumer;
import java.util.function.ToIntFunction;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test18
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/26
 * Time(创建时间)： 16:35
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test18
{
    public static void main(String[] args)
    {
        List<Integer> list = new ArrayList<>();
        for (int i = 1000; i < 1005; i++)
        {
            list.add(i);
        }
        list.stream().mapToInt(new ToIntFunction<Integer>()
        {
            @Override
            public int applyAsInt(Integer value)
            {
                return value;
            }
        }).forEach(new IntConsumer()
        {
            @Override
            public void accept(int value)
            {
                System.out.println(value);
            }
        });
        list.stream().mapToInt(value -> value).forEach(System.out::println);
    }
}
```



```sh
1000
1001
1002
1003
1004
1000
1001
1002
1003
1004
```





### concat方法

如果有两个流，希望合并成为一个流，那么可以使用Stream接口的静态方法concat

```java

    /**
     * Creates a lazily concatenated stream whose elements are all the
     * elements of the first stream followed by all the elements of the
     * second stream.  The resulting stream is ordered if both
     * of the input streams are ordered, and parallel if either of the input
     * streams is parallel.  When the resulting stream is closed, the close
     * handlers for both input streams are invoked.
     *
     * @implNote
     * Use caution when constructing streams from repeated concatenation.
     * Accessing an element of a deeply concatenated stream can result in deep
     * call chains, or even {@code StackOverflowException}.
     *
     * @param <T> The type of stream elements
     * @param a the first stream
     * @param b the second stream
     * @return the concatenation of the two input streams
     */
    public static <T> Stream<T> concat(Stream<? extends T> a, Stream<? extends T> b) {
        Objects.requireNonNull(a);
        Objects.requireNonNull(b);

        @SuppressWarnings("unchecked")
        Spliterator<T> split = new Streams.ConcatSpliterator.OfRef<>(
                (Spliterator<T>) a.spliterator(), (Spliterator<T>) b.spliterator());
        Stream<T> stream = StreamSupport.stream(split, a.isParallel() || b.isParallel());
        return stream.onClose(Streams.composedClose(a, b));
    }
```



```java
package mao;

import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.Stream;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test19
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/26
 * Time(创建时间)： 16:50
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test19
{
    public static void main(String[] args)
    {
        List<Integer> list1 = new ArrayList<>();
        for (int i = 1000; i < 1005; i++)
        {
            list1.add(i);
        }
        List<Integer> list2 = new ArrayList<>();
        for (int i = 2000; i < 2005; i++)
        {
            list2.add(i);
        }
        Stream<Integer> stream = Stream.concat(list1.stream(), list2.stream());
        System.out.println(stream.collect(Collectors.toList()));
    }
}
```



```sh
[1000, 1001, 1002, 1003, 1004, 2000, 2001, 2002, 2003, 2004]
```







### Stream流中的结果到集合中

Stream流提供collect方法，其参数需要一个java.util.stream.Collector接口对象来指定收集到哪 种集合中。java.util.stream.Collectors类提供一些方法，可以作为Collector接口的实例

* public static  Collector> toList()：转换为List集合
* public static  Collector> toSet()：转换为Set集合



```java
    /**
     * Performs a <a href="package-summary.html#MutableReduction">mutable
     * reduction</a> operation on the elements of this stream.  A mutable
     * reduction is one in which the reduced value is a mutable result container,
     * such as an {@code ArrayList}, and elements are incorporated by updating
     * the state of the result rather than by replacing the result.  This
     * produces a result equivalent to:
     * <pre>{@code
     *     R result = supplier.get();
     *     for (T element : this stream)
     *         accumulator.accept(result, element);
     *     return result;
     * }</pre>
     *
     * <p>Like {@link #reduce(Object, BinaryOperator)}, {@code collect} operations
     * can be parallelized without requiring additional synchronization.
     *
     * <p>This is a <a href="package-summary.html#StreamOps">terminal
     * operation</a>.
     *
     * @apiNote There are many existing classes in the JDK whose signatures are
     * well-suited for use with method references as arguments to {@code collect()}.
     * For example, the following will accumulate strings into an {@code ArrayList}:
     * <pre>{@code
     *     List<String> asList = stringStream.collect(ArrayList::new, ArrayList::add,
     *                                                ArrayList::addAll);
     * }</pre>
     *
     * <p>The following will take a stream of strings and concatenates them into a
     * single string:
     * <pre>{@code
     *     String concat = stringStream.collect(StringBuilder::new, StringBuilder::append,
     *                                          StringBuilder::append)
     *                                 .toString();
     * }</pre>
     *
     * @param <R> type of the result
     * @param supplier a function that creates a new result container. For a
     *                 parallel execution, this function may be called
     *                 multiple times and must return a fresh value each time.
     * @param accumulator an <a href="package-summary.html#Associativity">associative</a>,
     *                    <a href="package-summary.html#NonInterference">non-interfering</a>,
     *                    <a href="package-summary.html#Statelessness">stateless</a>
     *                    function for incorporating an additional element into a result
     * @param combiner an <a href="package-summary.html#Associativity">associative</a>,
     *                    <a href="package-summary.html#NonInterference">non-interfering</a>,
     *                    <a href="package-summary.html#Statelessness">stateless</a>
     *                    function for combining two values, which must be
     *                    compatible with the accumulator function
     * @return the result of the reduction
     */
    <R> R collect(Supplier<R> supplier,
                  BiConsumer<R, ? super T> accumulator,
                  BiConsumer<R, R> combiner);

    /**
     * Performs a <a href="package-summary.html#MutableReduction">mutable
     * reduction</a> operation on the elements of this stream using a
     * {@code Collector}.  A {@code Collector}
     * encapsulates the functions used as arguments to
     * {@link #collect(Supplier, BiConsumer, BiConsumer)}, allowing for reuse of
     * collection strategies and composition of collect operations such as
     * multiple-level grouping or partitioning.
     *
     * <p>If the stream is parallel, and the {@code Collector}
     * is {@link Collector.Characteristics#CONCURRENT concurrent}, and
     * either the stream is unordered or the collector is
     * {@link Collector.Characteristics#UNORDERED unordered},
     * then a concurrent reduction will be performed (see {@link Collector} for
     * details on concurrent reduction.)
     *
     * <p>This is a <a href="package-summary.html#StreamOps">terminal
     * operation</a>.
     *
     * <p>When executed in parallel, multiple intermediate results may be
     * instantiated, populated, and merged so as to maintain isolation of
     * mutable data structures.  Therefore, even when executed in parallel
     * with non-thread-safe data structures (such as {@code ArrayList}), no
     * additional synchronization is needed for a parallel reduction.
     *
     * @apiNote
     * The following will accumulate strings into an ArrayList:
     * <pre>{@code
     *     List<String> asList = stringStream.collect(Collectors.toList());
     * }</pre>
     *
     * <p>The following will classify {@code Person} objects by city:
     * <pre>{@code
     *     Map<String, List<Person>> peopleByCity
     *         = personStream.collect(Collectors.groupingBy(Person::getCity));
     * }</pre>
     *
     * <p>The following will classify {@code Person} objects by state and city,
     * cascading two {@code Collector}s together:
     * <pre>{@code
     *     Map<String, Map<String, List<Person>>> peopleByStateAndCity
     *         = personStream.collect(Collectors.groupingBy(Person::getState,
     *                                                      Collectors.groupingBy(Person::getCity)));
     * }</pre>
     *
     * @param <R> the type of the result
     * @param <A> the intermediate accumulation type of the {@code Collector}
     * @param collector the {@code Collector} describing the reduction
     * @return the result of the reduction
     * @see #collect(Supplier, BiConsumer, BiConsumer)
     * @see Collectors
     */
    <R, A> R collect(Collector<? super T, A, R> collector);
```



```java
package mao;

import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import java.util.Set;
import java.util.stream.Collectors;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test20
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/26
 * Time(创建时间)： 17:02
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test20
{
    public static void main(String[] args)
    {
        List<Integer> list = new ArrayList<>();
        for (int i = 1000; i < 1010; i++)
        {
            list.add(i);
        }
        Collections.shuffle(list);
        System.out.println(list);
        List<Integer> collect = list.stream().collect(Collectors.toList());
        System.out.println(collect);
        Set<Integer> collect1 = list.stream().collect(Collectors.toSet());
        System.out.println(collect1);
    }
}
```



```sh
[1009, 1004, 1007, 1001, 1000, 1003, 1002, 1008, 1006, 1005]
[1009, 1004, 1007, 1001, 1000, 1003, 1002, 1008, 1006, 1005]
[1008, 1009, 1000, 1001, 1002, 1003, 1004, 1005, 1006, 1007]
```







### Stream流中的结果到数组中

Stream提供toArray方法来将结果放到一个数组中，返回值类型是Object[]的

```java

    /**
     * Returns an array containing the elements of this stream.
     *
     * <p>This is a <a href="package-summary.html#StreamOps">terminal
     * operation</a>.
     *
     * @return an array containing the elements of this stream
     */
    Object[] toArray();
```



```java
package mao;

import java.util.ArrayList;
import java.util.List;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test21
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/26
 * Time(创建时间)： 17:06
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test21
{
    public static void main(String[] args)
    {
        List<Integer> list = new ArrayList<>();
        for (int i = 1000; i < 1010; i++)
        {
            list.add(i);
        }
        Object[] array = list.stream().toArray();
        System.out.println(array);
        for (Object o : array)
        {
            System.out.print(o + ",");
        }
    }
}
```



```sh
[Ljava.lang.Object;@7ba4f24f
1000,1001,1002,1003,1004,1005,1006,1007,1008,1009,
```





### 对流中数据进行聚合计算

当我们使用Stream流处理数据后，可以像数据库的聚合函数一样对某个字段进行操作。比如获取最大值，获取最小 值，求总和，平均值，统计数量

```java
package mao;

import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;
import java.util.function.ToIntFunction;
import java.util.stream.Collectors;
import java.util.stream.Stream;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test22
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/26
 * Time(创建时间)： 17:09
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test22
{
    public static void main(String[] args)
    {
        List<Integer> list = new ArrayList<>();
        for (int i = 1000; i < 1010; i++)
        {
            list.add(i);
        }
        // 获取最大值
        Integer integer = list.stream().collect(Collectors.maxBy(new Comparator<Integer>()
        {
            @Override
            public int compare(Integer o1, Integer o2)
            {
                return o1 - o2;
            }
        })).get();
        System.out.println(integer);

        // 获取最小值
        integer = list.stream().collect(Collectors.minBy(new Comparator<Integer>()
        {
            @Override
            public int compare(Integer o1, Integer o2)
            {
                return o1 - o2;
            }
        })).get();
        System.out.println(integer);

        // 求总和
        integer = list.stream().collect(Collectors.summingInt(new ToIntFunction<Integer>()
        {
            @Override
            public int applyAsInt(Integer value)
            {
                return value;
            }
        }));
        System.out.println(integer);

        // 平均值
        Double aDouble = list.stream().collect(Collectors.averagingInt(new ToIntFunction<Integer>()
        {
            @Override
            public int applyAsInt(Integer value)
            {
                return value;
            }
        }));
        System.out.println(aDouble);


        // 统计数量
        Long aLong = list.stream().collect(Collectors.counting());
        System.out.println(aLong);
    }
}
```





### 对流中数据进行分组

当我们使用Stream流处理数据后，可以根据某个属性将数据分组



```java
package mao;

import java.util.ArrayList;
import java.util.List;
import java.util.Map;
import java.util.function.Function;
import java.util.stream.Collectors;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test24
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/26
 * Time(创建时间)： 17:26
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test24
{
    public static void main(String[] args)
    {
        List<Integer> list = new ArrayList<>();
        for (int i = 1000; i < 1010; i++)
        {
            list.add(i);
        }
        Map<String, List<Integer>> collect = list.stream().collect(Collectors.groupingBy(new Function<Integer, String>()
        {
            @Override
            public String apply(Integer integer)
            {
                if (integer > 1005)
                {
                    return "大于1005";
                }
                else
                {
                    return "小于等于1005";
                }
            }
        }));
        System.out.println(collect);
    }
}
```



```sh
{小于等于1005=[1000, 1001, 1002, 1003, 1004, 1005], 大于1005=[1006, 1007, 1008, 1009]}
```





### 对流中数据进行多级分组

```java
package mao;

import java.util.ArrayList;
import java.util.List;
import java.util.Map;
import java.util.function.Function;
import java.util.stream.Collectors;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test25
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/27
 * Time(创建时间)： 15:55
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test25
{
    public static void main(String[] args)
    {
        List<Integer> list = new ArrayList<>();
        for (int i = 1000; i < 1030; i++)
        {
            list.add(i);
        }
        Map<String, Map<String, List<Integer>>> mapMap = list.stream().collect(Collectors.groupingBy(new Function<Integer, String>()
        {
            @Override
            public String apply(Integer integer)
            {
                if (integer % 2 == 0)
                {
                    return "双数";
                }
                else
                {
                    return "单数";
                }
            }
        }, Collectors.groupingBy(new Function<Integer, String>()
        {
            @Override
            public String apply(Integer integer)
            {
                if (integer > 1010)
                {
                    return "大于1010";
                }
                else
                {
                    return "小于等于1010";
                }
            }
        })));
        System.out.println(mapMap);
    }
}
```



```sh
{单数={大于1010=[1011, 1013, 1015, 1017, 1019, 1021, 1023, 1025, 1027, 1029], 小于等于1010=[1001, 1003, 1005, 1007, 1009]}, 双数={大于1010=[1012, 1014, 1016, 1018, 1020, 1022, 1024, 1026, 1028], 小于等于1010=[1000, 1002, 1004, 1006, 1008, 1010]}}
```







### 对流中数据进行分区

Collectors.partitioningBy 会根据值是否为true，把集合分割为两个列表，一个true列表，一个false列表



```java
package mao;

import java.util.ArrayList;
import java.util.List;
import java.util.Map;
import java.util.function.Predicate;
import java.util.stream.Collectors;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test26
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/27
 * Time(创建时间)： 16:02
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test26
{
    public static void main(String[] args)
    {
        List<Integer> list = new ArrayList<>();
        for (int i = 1000; i < 1030; i++)
        {
            list.add(i);
        }
        Map<Boolean, List<Integer>> collect = list.stream().collect(Collectors.partitioningBy(integer -> integer % 2 == 0));
        System.out.println(collect);
        collect = list.stream().collect(Collectors.partitioningBy(integer -> integer % 2 == 1));
        System.out.println(collect);
        collect = list.stream().collect(Collectors.partitioningBy(integer -> integer > 1015));
        System.out.println(collect);
    }
}
```



```sh
{false=[1001, 1003, 1005, 1007, 1009, 1011, 1013, 1015, 1017, 1019, 1021, 1023, 1025, 1027, 1029], true=[1000, 1002, 1004, 1006, 1008, 1010, 1012, 1014, 1016, 1018, 1020, 1022, 1024, 1026, 1028]}
{false=[1000, 1002, 1004, 1006, 1008, 1010, 1012, 1014, 1016, 1018, 1020, 1022, 1024, 1026, 1028], true=[1001, 1003, 1005, 1007, 1009, 1011, 1013, 1015, 1017, 1019, 1021, 1023, 1025, 1027, 1029]}
{false=[1000, 1001, 1002, 1003, 1004, 1005, 1006, 1007, 1008, 1009, 1010, 1011, 1012, 1013, 1014, 1015], true=[1016, 1017, 1018, 1019, 1020, 1021, 1022, 1023, 1024, 1025, 1026, 1027, 1028, 1029]}
```





### 对流中数据进行拼接

```java
package mao;

import java.util.ArrayList;
import java.util.List;
import java.util.function.Function;
import java.util.stream.Collectors;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test27
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/27
 * Time(创建时间)： 16:06
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test27
{
    public static void main(String[] args)
    {
        List<Integer> list = new ArrayList<>();
        for (int i = 1000; i < 1030; i++)
        {
            list.add(i);
        }
        String collect = list.stream()
                .map(Object::toString)
                .collect(Collectors.joining(",,"));
        System.out.println(collect);
         collect = list.stream()
                .map(Object::toString)
                .collect(Collectors.joining(",","[","]"));
        System.out.println(collect);
    }
}
```



```sh
1000,,1001,,1002,,1003,,1004,,1005,,1006,,1007,,1008,,1009,,1010,,1011,,1012,,1013,,1014,,1015,,1016,,1017,,1018,,1019,,1020,,1021,,1022,,1023,,1024,,1025,,1026,,1027,,1028,,1029
[1000,1001,1002,1003,1004,1005,1006,1007,1008,1009,1010,1011,1012,1013,1014,1015,1016,1017,1018,1019,1020,1021,1022,1023,1024,1025,1026,1027,1028,1029]
```







## 并行的Stream流

### 概述

parallelStream其实就是一个并行执行的流。它通过默认的ForkJoinPool，可能提高多线程任务的速度



获取并行Stream流的两种方式：

* 直接获取并行的流
* 将串行流转成并行流





### 直接获取并行的流

```java
package mao;

import java.util.ArrayList;
import java.util.List;
import java.util.stream.Stream;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test28
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/27
 * Time(创建时间)： 16:18
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test28
{
    public static void main(String[] args)
    {
        List<Integer> list = new ArrayList<>();
        for (int i = 1000; i < 1030; i++)
        {
            list.add(i);
        }
        Stream<Integer> stream = list.parallelStream();
        
    }
}
```





### 将串行流转成并行流

```java
package mao;

import java.util.ArrayList;
import java.util.List;
import java.util.function.Function;

/**
 * Project name(项目名称)：JDK8_Stream
 * Package(包名): mao
 * Class(类名): Test29
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/27
 * Time(创建时间)： 16:21
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test29
{
    public static void main(String[] args)
    {
        List<Integer> list = new ArrayList<>();
        for (int i = 1000; i < 1030; i++)
        {
            list.add(i);
        }
        list.stream().map(Object::toString).parallel()
                .forEach(s -> System.out.println(Thread.currentThread().getName() + "  " + s));
    }
}
```



```sh
main  1019
main  1018
main  1021
main  1020
ForkJoinPool.commonPool-worker-8  1003
ForkJoinPool.commonPool-worker-8  1000
ForkJoinPool.commonPool-worker-30  1007
ForkJoinPool.commonPool-worker-29  1013
ForkJoinPool.commonPool-worker-8  1029
ForkJoinPool.commonPool-worker-26  1014
ForkJoinPool.commonPool-worker-26  1022
ForkJoinPool.commonPool-worker-29  1015
ForkJoinPool.commonPool-worker-8  1028
ForkJoinPool.commonPool-worker-9  1026
ForkJoinPool.commonPool-worker-26  1017
ForkJoinPool.commonPool-worker-11  1004
ForkJoinPool.commonPool-worker-26  1002
ForkJoinPool.commonPool-worker-25  1009
ForkJoinPool.commonPool-worker-20  1010
ForkJoinPool.commonPool-worker-22  1001
ForkJoinPool.commonPool-worker-15  1006
ForkJoinPool.commonPool-worker-1  1023
main  1016
ForkJoinPool.commonPool-worker-19  1008
ForkJoinPool.commonPool-worker-9  1005
ForkJoinPool.commonPool-worker-4  1024
ForkJoinPool.commonPool-worker-9  1025
ForkJoinPool.commonPool-worker-4  1011
ForkJoinPool.commonPool-worker-18  1027
ForkJoinPool.commonPool-worker-30  1012
```





### 效率对比

使用for循环，串行Stream流，并行Stream流来对5亿个数字求和

```java
package mao;

import java.util.stream.LongStream;

/**
 * Project name(项目名称)：JDK_parallelStream
 * Package(包名): mao
 * Class(类名): Test3
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/27
 * Time(创建时间)： 16:29
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test3
{
    private static long times = 50000000000L;


    public static void main(String[] args)
    {
        testSerialStream();
        testStream();
        testFor();
    }

    private static void testSerialStream()
    {
        System.out.println("serialStream");
        long start = System.currentTimeMillis();
        LongStream.rangeClosed(0, times)
                .parallel()
                .reduce(0, Long::sum);
        long end = System.currentTimeMillis();
        System.out.println("时间：" + (end - start));
    }

    private static void testStream()
    {
        System.out.println("stream");
        long start = System.currentTimeMillis();
        LongStream.rangeClosed(0, times)
                .reduce(0, Long::sum);
        long end = System.currentTimeMillis();
        System.out.println("时间：" + (end - start));
    }

    private static void testFor()
    {
        System.out.println("for");
        long start = System.currentTimeMillis();
        long result = 0L;
        for (long i = 1L; i < times; i++)
        {
            result += i;
        }
        long end = System.currentTimeMillis();
        System.out.println("时间：" + (end - start));
    }
}

```



```sh
serialStream
时间：1259
stream
时间：50593
for
时间：10068
```



**parallelStream是线程不安全的**











## Optional类

### 概述

以前对null的处理方式：

```java
package mao;

import java.util.ArrayList;
import java.util.List;

/**
 * Project name(项目名称)：JDK8_Optional
 * Package(包名): mao
 * Class(类名): Test1
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/27
 * Time(创建时间)： 16:50
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test1
{
    public static void main(String[] args)
    {
        List<String> list = new ArrayList<>();
        if (list == null)
        {
            System.out.println("null");
        }
        else
        {
            System.out.println("todo");
        }
    }
}
```



Optional是一个没有子类的工具类，Optional是一个可以为null的容器对象。它的作用主要就是为了解决避免Null检 查，防止NullPointerException



### 常用方法

* Optional.of(T t) :  创建一个 Optional 实例
* Optional.empty() : 创建一个空的 Optional 实例
* Optional.ofNullable(T t):若 t 不为 null,创建 Optional 实例,否则创建空实例



常用方法：

* isPresent() :  判断是否包含值,包含值返回true，不包含值返回false
* get() : 如果Optional有值则将其返回，否则抛出NoSuchElementException
* orElse(T t) :  如果调用对象包含值，返回该值，否则返回参数t
* orElseGet(Supplier s) :如果调用对象包含值，返回该值，否则返回 s 获取的值
* map(Function f): 如果有值对其处理，并返回处理后的Optional，否则返回 Optional.empty()







```java
/*
 * Copyright (c) 2012, 2013, Oracle and/or its affiliates. All rights reserved.
 * DO NOT ALTER OR REMOVE COPYRIGHT NOTICES OR THIS FILE HEADER.
 *
 * This code is free software; you can redistribute it and/or modify it
 * under the terms of the GNU General Public License version 2 only, as
 * published by the Free Software Foundation.  Oracle designates this
 * particular file as subject to the "Classpath" exception as provided
 * by Oracle in the LICENSE file that accompanied this code.
 *
 * This code is distributed in the hope that it will be useful, but WITHOUT
 * ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or
 * FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License
 * version 2 for more details (a copy is included in the LICENSE file that
 * accompanied this code).
 *
 * You should have received a copy of the GNU General Public License version
 * 2 along with this work; if not, write to the Free Software Foundation,
 * Inc., 51 Franklin St, Fifth Floor, Boston, MA 02110-1301 USA.
 *
 * Please contact Oracle, 500 Oracle Parkway, Redwood Shores, CA 94065 USA
 * or visit www.oracle.com if you need additional information or have any
 * questions.
 */
package java.util;

import java.util.function.Consumer;
import java.util.function.Function;
import java.util.function.Predicate;
import java.util.function.Supplier;

/**
 * A container object which may or may not contain a non-null value.
 * If a value is present, {@code isPresent()} will return {@code true} and
 * {@code get()} will return the value.
 *
 * <p>Additional methods that depend on the presence or absence of a contained
 * value are provided, such as {@link #orElse(java.lang.Object) orElse()}
 * (return a default value if value not present) and
 * {@link #ifPresent(java.util.function.Consumer) ifPresent()} (execute a block
 * of code if the value is present).
 *
 * <p>This is a <a href="../lang/doc-files/ValueBased.html">value-based</a>
 * class; use of identity-sensitive operations (including reference equality
 * ({@code ==}), identity hash code, or synchronization) on instances of
 * {@code Optional} may have unpredictable results and should be avoided.
 *
 * @since 1.8
 */
public final class Optional<T> {
    /**
     * Common instance for {@code empty()}.
     */
    private static final Optional<?> EMPTY = new Optional<>();

    /**
     * If non-null, the value; if null, indicates no value is present
     */
    private final T value;

    /**
     * Constructs an empty instance.
     *
     * @implNote Generally only one empty instance, {@link Optional#EMPTY},
     * should exist per VM.
     */
    private Optional() {
        this.value = null;
    }

    /**
     * Returns an empty {@code Optional} instance.  No value is present for this
     * Optional.
     *
     * @apiNote Though it may be tempting to do so, avoid testing if an object
     * is empty by comparing with {@code ==} against instances returned by
     * {@code Option.empty()}. There is no guarantee that it is a singleton.
     * Instead, use {@link #isPresent()}.
     *
     * @param <T> Type of the non-existent value
     * @return an empty {@code Optional}
     */
    public static<T> Optional<T> empty() {
        @SuppressWarnings("unchecked")
        Optional<T> t = (Optional<T>) EMPTY;
        return t;
    }

    /**
     * Constructs an instance with the value present.
     *
     * @param value the non-null value to be present
     * @throws NullPointerException if value is null
     */
    private Optional(T value) {
        this.value = Objects.requireNonNull(value);
    }

    /**
     * Returns an {@code Optional} with the specified present non-null value.
     *
     * @param <T> the class of the value
     * @param value the value to be present, which must be non-null
     * @return an {@code Optional} with the value present
     * @throws NullPointerException if value is null
     */
    public static <T> Optional<T> of(T value) {
        return new Optional<>(value);
    }

    /**
     * Returns an {@code Optional} describing the specified value, if non-null,
     * otherwise returns an empty {@code Optional}.
     *
     * @param <T> the class of the value
     * @param value the possibly-null value to describe
     * @return an {@code Optional} with a present value if the specified value
     * is non-null, otherwise an empty {@code Optional}
     */
    public static <T> Optional<T> ofNullable(T value) {
        return value == null ? empty() : of(value);
    }

    /**
     * If a value is present in this {@code Optional}, returns the value,
     * otherwise throws {@code NoSuchElementException}.
     *
     * @return the non-null value held by this {@code Optional}
     * @throws NoSuchElementException if there is no value present
     *
     * @see Optional#isPresent()
     */
    public T get() {
        if (value == null) {
            throw new NoSuchElementException("No value present");
        }
        return value;
    }

    /**
     * Return {@code true} if there is a value present, otherwise {@code false}.
     *
     * @return {@code true} if there is a value present, otherwise {@code false}
     */
    public boolean isPresent() {
        return value != null;
    }

    /**
     * If a value is present, invoke the specified consumer with the value,
     * otherwise do nothing.
     *
     * @param consumer block to be executed if a value is present
     * @throws NullPointerException if value is present and {@code consumer} is
     * null
     */
    public void ifPresent(Consumer<? super T> consumer) {
        if (value != null)
            consumer.accept(value);
    }

    /**
     * If a value is present, and the value matches the given predicate,
     * return an {@code Optional} describing the value, otherwise return an
     * empty {@code Optional}.
     *
     * @param predicate a predicate to apply to the value, if present
     * @return an {@code Optional} describing the value of this {@code Optional}
     * if a value is present and the value matches the given predicate,
     * otherwise an empty {@code Optional}
     * @throws NullPointerException if the predicate is null
     */
    public Optional<T> filter(Predicate<? super T> predicate) {
        Objects.requireNonNull(predicate);
        if (!isPresent())
            return this;
        else
            return predicate.test(value) ? this : empty();
    }

    /**
     * If a value is present, apply the provided mapping function to it,
     * and if the result is non-null, return an {@code Optional} describing the
     * result.  Otherwise return an empty {@code Optional}.
     *
     * @apiNote This method supports post-processing on optional values, without
     * the need to explicitly check for a return status.  For example, the
     * following code traverses a stream of file names, selects one that has
     * not yet been processed, and then opens that file, returning an
     * {@code Optional<FileInputStream>}:
     *
     * <pre>{@code
     *     Optional<FileInputStream> fis =
     *         names.stream().filter(name -> !isProcessedYet(name))
     *                       .findFirst()
     *                       .map(name -> new FileInputStream(name));
     * }</pre>
     *
     * Here, {@code findFirst} returns an {@code Optional<String>}, and then
     * {@code map} returns an {@code Optional<FileInputStream>} for the desired
     * file if one exists.
     *
     * @param <U> The type of the result of the mapping function
     * @param mapper a mapping function to apply to the value, if present
     * @return an {@code Optional} describing the result of applying a mapping
     * function to the value of this {@code Optional}, if a value is present,
     * otherwise an empty {@code Optional}
     * @throws NullPointerException if the mapping function is null
     */
    public<U> Optional<U> map(Function<? super T, ? extends U> mapper) {
        Objects.requireNonNull(mapper);
        if (!isPresent())
            return empty();
        else {
            return Optional.ofNullable(mapper.apply(value));
        }
    }

    /**
     * If a value is present, apply the provided {@code Optional}-bearing
     * mapping function to it, return that result, otherwise return an empty
     * {@code Optional}.  This method is similar to {@link #map(Function)},
     * but the provided mapper is one whose result is already an {@code Optional},
     * and if invoked, {@code flatMap} does not wrap it with an additional
     * {@code Optional}.
     *
     * @param <U> The type parameter to the {@code Optional} returned by
     * @param mapper a mapping function to apply to the value, if present
     *           the mapping function
     * @return the result of applying an {@code Optional}-bearing mapping
     * function to the value of this {@code Optional}, if a value is present,
     * otherwise an empty {@code Optional}
     * @throws NullPointerException if the mapping function is null or returns
     * a null result
     */
    public<U> Optional<U> flatMap(Function<? super T, Optional<U>> mapper) {
        Objects.requireNonNull(mapper);
        if (!isPresent())
            return empty();
        else {
            return Objects.requireNonNull(mapper.apply(value));
        }
    }

    /**
     * Return the value if present, otherwise return {@code other}.
     *
     * @param other the value to be returned if there is no value present, may
     * be null
     * @return the value, if present, otherwise {@code other}
     */
    public T orElse(T other) {
        return value != null ? value : other;
    }

    /**
     * Return the value if present, otherwise invoke {@code other} and return
     * the result of that invocation.
     *
     * @param other a {@code Supplier} whose result is returned if no value
     * is present
     * @return the value if present otherwise the result of {@code other.get()}
     * @throws NullPointerException if value is not present and {@code other} is
     * null
     */
    public T orElseGet(Supplier<? extends T> other) {
        return value != null ? value : other.get();
    }

    /**
     * Return the contained value, if present, otherwise throw an exception
     * to be created by the provided supplier.
     *
     * @apiNote A method reference to the exception constructor with an empty
     * argument list can be used as the supplier. For example,
     * {@code IllegalStateException::new}
     *
     * @param <X> Type of the exception to be thrown
     * @param exceptionSupplier The supplier which will return the exception to
     * be thrown
     * @return the present value
     * @throws X if there is no value present
     * @throws NullPointerException if no value is present and
     * {@code exceptionSupplier} is null
     */
    public <X extends Throwable> T orElseThrow(Supplier<? extends X> exceptionSupplier) throws X {
        if (value != null) {
            return value;
        } else {
            throw exceptionSupplier.get();
        }
    }

    /**
     * Indicates whether some other object is "equal to" this Optional. The
     * other object is considered equal if:
     * <ul>
     * <li>it is also an {@code Optional} and;
     * <li>both instances have no value present or;
     * <li>the present values are "equal to" each other via {@code equals()}.
     * </ul>
     *
     * @param obj an object to be tested for equality
     * @return {code true} if the other object is "equal to" this object
     * otherwise {@code false}
     */
    @Override
    public boolean equals(Object obj) {
        if (this == obj) {
            return true;
        }

        if (!(obj instanceof Optional)) {
            return false;
        }

        Optional<?> other = (Optional<?>) obj;
        return Objects.equals(value, other.value);
    }

    /**
     * Returns the hash code value of the present value, if any, or 0 (zero) if
     * no value is present.
     *
     * @return hash code value of the present value or 0 if no value is present
     */
    @Override
    public int hashCode() {
        return Objects.hashCode(value);
    }

    /**
     * Returns a non-empty string representation of this Optional suitable for
     * debugging. The exact presentation format is unspecified and may vary
     * between implementations and versions.
     *
     * @implSpec If a value is present the result must include its string
     * representation in the result. Empty and present Optionals must be
     * unambiguously differentiable.
     *
     * @return the string representation of this instance
     */
    @Override
    public String toString() {
        return value != null
            ? String.format("Optional[%s]", value)
            : "Optional.empty";
    }
}
```





### 基本使用

```java
package mao;

import java.util.Optional;

/**
 * Project name(项目名称)：JDK8_Optional
 * Package(包名): mao
 * Class(类名): Test2
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/27
 * Time(创建时间)： 16:58
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test2
{
    public static void main(String[] args)
    {
        System.out.println(Optional.of("123").get());
        System.out.println(Optional.of("22").isPresent());
        System.out.println(Optional.of(null).isPresent());
        Optional.of(null).get();
    }
}
```







## 新日期和时间API

### 旧版日期时间API问题

* 设计很差： 在java.util和java.sql的包中都有日期类，java.util.Date同时包含日期和时间，而java.sql.Date仅包含日期。此外用于格式化和解析的类在java.text包中定义
* 非线程安全：java.util.Date 是非线程安全的，所有的日期类都是可变的，这是Java日期类最大的问题之一
* 时区处理麻烦：日期类并不提供国际化，没有时区支持，因此Java引入了java.util.Calendar和 java.util.TimeZone类，但他们同样存在上述所有的问题





### 概述

JDK8中增加了一套全新的日期时间API，这套API设计合理，是线程安全的。新的日期及时间API位于java.time包中



![image-20231027171550880](img/JDK新特性学习笔记/image-20231027171550880.png)



* LocalDate ：表示日期，包含年月日，格式为 2019-10-16
*  LocalTime ：表示时间，包含时分秒，格式为 16:38:54.158549300
*  LocalDateTime ：表示日期时间，包含年月日，时分秒
*  DateTimeFormatter ：日期时间格式化类
* Instant：时间戳，表示一个特定的时间瞬间
* Duration：用于计算2个时间(LocalTime，时分秒)的距离
* Period：用于计算2个日期(LocalDate，年月日)的距离
* ZonedDateTime ：包含时区的时间



 Java中使用的历法是ISO 8601日历系统，它是世界民用历法，也就是我们所说的公历。平年有365天，闰年是366 天。此外Java 8还提供了4套其他历法：

* ThaiBuddhistDate ：泰国佛教历
* MinguoDate ：中华民国历
* JapaneseDate：日本历
*  HijrahDate：伊斯兰历





```java
package mao;

import java.time.LocalDate;
import java.time.chrono.HijrahDate;
import java.time.chrono.JapaneseDate;
import java.time.chrono.MinguoDate;
import java.time.chrono.ThaiBuddhistDate;

/**
 * Project name(项目名称)：JDK8_data_time_API
 * Package(包名): mao
 * Class(类名): Test1
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/27
 * Time(创建时间)： 17:14
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test1
{
    public static void main(String[] args)
    {
        MinguoDate now = MinguoDate.now();
        System.out.println(now);
        System.out.println(JapaneseDate.now());
        LocalDate localDate = LocalDate.now();
        System.out.println(localDate);
        HijrahDate hijrahDate = HijrahDate.now();
        System.out.println(hijrahDate);
        ThaiBuddhistDate thaiBuddhistDate = ThaiBuddhistDate.now();
        System.out.println(thaiBuddhistDate);
    }
}
```



```sh
Minguo ROC 112-10-27
Japanese Reiwa 5-10-27
2023-10-27
Hijrah-umalqura AH 1445-04-12
ThaiBuddhist BE 2566-10-27
```





### LocalDate

```java
package mao;

import java.time.LocalDate;

/**
 * Project name(项目名称)：JDK8_data_time_API
 * Package(包名): mao
 * Class(类名): Test2
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/27
 * Time(创建时间)： 17:23
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test2
{
    public static void main(String[] args)
    {
        //创建指定日期
        LocalDate fj = LocalDate.of(1985, 9, 23);
        System.out.println("fj = " + fj); // 1985-09-23
        //得到当前日期
        LocalDate nowDate = LocalDate.now();
        System.out.println("nowDate = " + nowDate);
        //获取日期信息
        System.out.println("年: " + nowDate.getYear());
        System.out.println("月: " + nowDate.getMonthValue());
        System.out.println("日: " + nowDate.getDayOfMonth());
        System.out.println("星期: " + nowDate.getDayOfWeek());
    }
}
```



```sh
fj = 1985-09-23
nowDate = 2023-10-28
年: 2023
月: 10
日: 28
星期: SATURDAY
```





### LocalTime

```java
package mao;

import java.time.LocalTime;

/**
 * Project name(项目名称)：JDK8_data_time_API
 * Package(包名): mao
 * Class(类名): Test3
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/28
 * Time(创建时间)： 17:56
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test3
{
    public static void main(String[] args)
    {
        // 得到指定的时间
        LocalTime time = LocalTime.of(12, 15, 28, 129_900_000);
        System.out.println("time = " + time);
        // 得到当前时间
        LocalTime nowTime = LocalTime.now();
        System.out.println("nowTime = " + nowTime);
        // 获取时间信息
        System.out.println("小时: " + nowTime.getHour());
        System.out.println("分钟: " + nowTime.getMinute());
        System.out.println("秒: " + nowTime.getSecond());
        System.out.println("纳秒: " + nowTime.getNano());
    }
}
```



```sh
time = 12:15:28.129900
nowTime = 17:58:30.571
小时: 17
分钟: 58
秒: 30
纳秒: 571000000
```







### LocalDateTime

```java
package mao;

import java.time.LocalDateTime;

/**
 * Project name(项目名称)：JDK8_data_time_API
 * Package(包名): mao
 * Class(类名): Test4
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/28
 * Time(创建时间)： 17:59
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test4
{
    public static void main(String[] args)
    {
        LocalDateTime fj = LocalDateTime.of(1985, 9, 23, 9, 10, 20);
        System.out.println("fj = " + fj);
        // 得到当前日期时间
        LocalDateTime now = LocalDateTime.now();
        System.out.println("now = " + now);
        System.out.println(now.getYear());
        System.out.println(now.getMonthValue());
        System.out.println(now.getDayOfMonth());
        System.out.println(now.getHour());
        System.out.println(now.getMinute());
        System.out.println(now.getSecond());
        System.out.println(now.getNano());
    }
}
```



```sh
fj = 1985-09-23T09:10:20
now = 2023-10-28T17:59:41.449
2023
10
28
17
59
41
449000000
```





### 日期时间的修改

对日期时间的修改，对已存在的LocalDate对象，创建它的修改版，最简单的方式是使用withAttribute方法

withAttribute方法会创建对象的一个副本，并按照需要修改它的属性。以下所有的方法都返回了一个修改属性的对 象，他们不会影响原来的对象

```java
package mao;

import java.time.LocalDateTime;

/**
 * Project name(项目名称)：JDK8_data_time_API
 * Package(包名): mao
 * Class(类名): Test5
 * Author(作者）: mao
 * Author QQ：1296193245
 * GitHub：https://github.com/maomao124/
 * Date(创建日期)： 2023/10/28
 * Time(创建时间)： 18:05
 * Version(版本): 1.0
 * Description(描述)： 无
 */

public class Test5
{
    public static void main(String[] args)
    {
        LocalDateTime now = LocalDateTime.now();
        System.out.println("now = " + now);
        LocalDateTime localDateTime = now.withYear(2021);
        System.out.println(localDateTime);
        System.out.println(now == localDateTime);
        System.out.println("修改月份: " + now.withMonth(8));
        System.out.println("修改小时: " + now.withHour(2));
        System.out.println("修改分钟: " + now.withMinute(13));

        LocalDateTime localDateTime1 = now.plusYears(3);
        System.out.println(localDateTime1);
        System.out.println(localDateTime1 == now);
        System.out.println("20月后: " + now.plusMonths(20));
        System.out.println("20年前: " + now.minusYears(20));
        System.out.println("5月前: " + now.minusMonths(5));
        System.out.println("100天前: " + now.minusDays(100));
        System.out.println("3周前: " + now.minusWeeks(3));
    }
}
```



```sh
now = 2023-10-28T18:10:08.748
2021-10-28T18:10:08.748
false
修改月份: 2023-08-28T18:10:08.748
修改小时: 2023-10-28T02:10:08.748
修改分钟: 2023-10-28T18:13:08.748
2026-10-28T18:10:08.748
false
20月后: 2025-06-28T18:10:08.748
20年前: 2003-10-28T18:10:08.748
5月前: 2023-05-28T18:10:08.748
100天前: 2023-07-20T18:10:08.748
3周前: 2023-10-07T18:10:08.748
```





### 日期时间的比较

