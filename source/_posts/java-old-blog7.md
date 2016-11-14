title: Java竞赛赛前复习(五)(异常)
date: 2014-04-24 10:24
tags: [Java,竞赛前复习]
categories: 辅助攻击技能
description: Java是怎么处理异常的呢？看本文就知道啦～
---

因为我有点担心他会考概念，所以就粘贴出来了，然后例题是自最后面

>异常基本概念：
一、异常的对象从哪里来呢？
有两个来源，一是Java运行时环境自动抛出系统生成的异常，而不管你是否愿意捕获和处理，它总要被抛出！比如除数为0的异常。
二是程序员自己抛出的异常，这个异常可以是程序员自己定义的，也可以是Java语言中定义的，用throw 关键字抛出异常，这种异常常用来向调用者汇报异常的一些信息。
</br>
</br>
二、
异常类从哪里来？有两个来源，一是Java语言本身定义的一些基本异常类型，二是用户通过继承Exception类或者其子类自己定义的异常。Exception 类及其子类是 Throwable 的一种形式，它指出了合理的应用程序想要捕获的条件。
</br>
</br>
三、
Java异常处理通过5个关键字try、catch、throw、throws、finally进行管理。基本过程是用try语句块包住要监视的语句，如果在try语句块内出现异常，则异常会被抛出，你的代码在catch语句块中可以捕获到这个异常并做处理；还有以部分系统生成的异常在Java运行时自动抛出。你也可以通过throws关键字在方法上声明该方法要抛出异常，然后在方法内部通过throw抛出异常对象。finally语句块会在方法执行return之前执行。
</br>
</br>
四、
下面是这几个类的层次图：
java.lang.Object
  java.lang.Throwable
      java.lang.Exception
       java.lang.RuntimeException
   java.lang.Error
       java.lang.ThreadDeath
下面四个类的介绍来自java api 文档。
</br>
1、Throwable
        Throwable 类是 Java 语言中所有错误或异常的超类。只有当对象是此类（或其子类之一）的实例时，才能通过 Java 虚拟机或者 Java throw 语句抛出。类似地，只有此类或其子类之一才可以是 catch 子句中的参数类型。
两个子类的实例，Error 和 Exception，通常用于指示发生了异常情况。通常，这些实例是在异常情况的上下文中新近创建的，因此包含了相关的信息（比如堆栈跟踪数据）。
2、Exception
        Exception 类及其子类是 Throwable 的一种形式，它指出了合理的应用程序想要捕获的条件，表示程序本身可以处理的异常。
3、Error
        Error 是 Throwable 的子类，表示仅靠程序本身无法恢复的严重错误，用于指示合理的应用程序不应该试图捕获的严重问题。
在执行该方法期间，无需在方法中通过throws声明可能抛出但没有捕获的 Error 的任何子类，因为Java编译器不去检查它，也就是说，当程序中可能出现这类异常时，即使没有用try...catch语句捕获它，也没有用throws字句声明抛出它，还是会编译通过。
4、RuntimeException
        RuntimeException 是那些可能在 Java 虚拟机正常运行期间抛出的异常的超类。Java编译器不去检查它，也就是说，当程序中可能出现这类异常时，即使没有用try...catch语句捕获它，也没有用throws字句声明抛出它，还是会编译通过，这种异常可以通过改进代码实现来避免。
5、ThreadDeath
        调用 Thread 类中带有零参数的 stop 方法时，受害线程将抛出一个 ThreadDeath 实例。
        仅当应用程序在被异步终止后必须清除时才应该捕获这个类的实例。如果 ThreadDeath 被一个方法捕获，那么将它重新抛出非常重要，因为这样才能让该线程真正终止。
如果没有捕获 ThreadDeath，则顶级错误处理程序不会输出消息。
        虽然 ThreadDeath 类是“正常出现”的，但它只能是 Error 的子类而不是 Exception 的子类，因为许多应用程序捕获所有出现的 Exception，然后又将其放弃。
</br>
</br>
五、Java异常处理机制
        对于可能出现异常的代码，有两种处理办法：
        第一、在方法中用try...catch语句捕获并处理异常，catach语句可以有多个，用来匹配多个异常。
第二、对于处理不了的异常或者要转型的异常，在方法的声明处通过throws语句抛出异常。例如：
public void test1() throws MyException{
 ...
 if(....){
  throw new MyException();
 }
} 
第一、调用异常的对象的printStackTrace()方法，打印方法调用栈的异常信息。
第二、如果出现异常的线程为主线程，则整个程序运行终止；如果非主线程，则终止该线程，其他线程继续运行。
</br>
</br>
六、
        那怎么判断一个方法可能会出现异常呢？一般来说，方法声明的时候用了throws语句，方法中有throw语句，方法调用的方法声明有throws关键字。
        throw和throws关键字的区别
        throw用来抛出一个异常，在方法体内。语法格式为：throw 异常对象。
        throws用来声明方法可能会抛出什么异常，在方法名后，语法格式为：throws 异常类型1，异常类型2...异常类型n。
五、运行时异常和受检查异常
Exception类可以分为两种：运行时异常和受检查异常。
1、运行时异常
RuntimeException类及其子类都被称为运行时异常，这种异常的特点是Java编译器不去检查它，也就是说，当程序中可能出现这类异常时，即使没有用try...catch语句捕获它，也没有用throws字句声明抛出它，还是会编译通过。例如，当除数为零时，就会抛出java.lang.ArithmeticException异常。
2、受检查异常
除了RuntimeException类及其子类外，其他的Exception类及其子类都属于受检查异常，这种异常的特点是要么用try...catch捕获处理，要么用throws语句声明抛出，否则编译不会通过。
4、运行时错误
Error类及其子类表示运行时错误，通常是由Java虚拟机抛出的，JDK中与定义了一些错误类，比如VirtualMachineError
和OutOfMemoryError，程序本身无法修复这些错误.一般不去扩展Error类来创建用户自定义的错误类。而RuntimeException类表示程序代码中的错误，是可扩展的，用户可以创建特定运行时异常类。
Error（运行时错误）和运行时异常的相同之处是:Java编译器都不去检查它们，当程序运行时出现它们，都会终止运行。
5、最佳解决方案
        对于运行时异常，我们不要用try...catch来捕获处理，而是在程序开发调试阶段，尽量去避免这种异常，一旦发现该异常，正确的做法就会改进程序设计的代码和实现方式，修改程序中的错误，从而避免这种异常。捕获并处理运行时异常是好的解决办法，因为可以通过改进代码实现来避免该种异常的发生。
        对于受检查异常，没说的，老老实实去按照异常处理的方法去处理，要么用try...catch捕获并解决，要么用throws抛出！
对于Error（运行时错误），不需要在程序中做任何处理，出现问题后，应该在程序在外的地方找问题，然后解决。

---

java7的新特性：
---

<b>一、catch的合并</b>
旧语法：
```
try{
    int i = 5/0;//会爆出异常
    FileInputStream in = new FileInputStream("text.txt");
    //因为没有这个文件所以也会爆出异常
}catch(ArimeticException e){
    e.printStackTrack();
}catch(FileNotFoundException e){
    e.printStackTrack();
}
```

新语法：
```
try{
    int i = 5/0;//会爆出异常
    FileInputStream in = new FileInputStream("text.txt");
    //因为没有这个文件所以也会爆出异常
}catch(ArimeticException e | FileNotFoundException e){
    e.printStackTrack();
}
```

<br>
<b>二、自动关闭资源</b>
关于资源调用，在java1.7之前需要在fianlly那里关闭资源，但是在1.7之后，一般的文件处理，数据库连接等都会自动实现autocloseable接口，如果是特殊的自己写的资源，可能需要自己去实现。

ps：如果是RuntimeException类的某子类的出现在catch中的话，它的子类是不可以再出现在他后面的。即子类不能出现在父类后面。
![](/images/java5/1.jpg)


对1.7自动关闭资源的使用方法如下：
![](/images/java5/2.jpg)

而且可以管理多个用分号间隔
try(new();new()){}

自动关闭时在catch和finally之前执行，而且关闭了才执行

<br>
<b>三、抛出异常的新办法</b>
之前抛出的话是要throw new IOExeption（e）；的，现在变成 throw e；即可
![](/images/java5/3.jpg)

<br>
<b>四、异常抑制</b>
①Throwable类增加addSuppressed方法和getSuppressed方法，支持原始异常中加入被抑制的异常（没有被处理的异常）。 
异常抑制：在try和finally中同时抛出异常时，finally中抛出的异常会在异常栈中向上传递，而try中产生的原始异常会消失。 
在Java7之前的版本，可以将原始异常保存，在finally中产生异常时抛出原始异常：
![](/images/java5/4.jpg)
1.7之后：存在异常就保存起来
![](/images/java5/5.jpg)

例题一、
![](/images/java5/6.jpg)

断言是正确的才会执行，如果断言成立，下面则会抛出空指针异常
第三个是因为api没有这个类
第四个要启动断言，默认是关闭断言机制的，启动要用到-ea

例题二、
![](/images/java5/7.jpg)

其实这题没什么，使用了一点点的数据库知识，只是从1.7开始。第88行可以省略
