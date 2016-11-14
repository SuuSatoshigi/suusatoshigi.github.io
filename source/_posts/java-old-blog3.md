title: Java竞赛赛前复习(一)(基础语法篇上)
date: 2014-04-24 10:20
tags: [Java,竞赛前复习]
categories: 辅助攻击技能
description: Java有什么基础语法的呢？看本文就知道啦～
---


<b>1.转义字符：</b>
>Java转义字符：
>特殊字符：\' ，\"，\\
>控制字符：\r回车、\n换行、\f、\t、\b


其它的都不可以！！比如下题：说一声看到其他都编译出错

![](/images/java1/2.png)


---


<b>2.字符串：</b>
记住性能排行
性能：String < StringBuffer(线程安全) < StringBuilder(线程不安全)
后两个常用append()、insert()方法

String改内容导致新对象生成 ： x = “ab” + “cd”;

![](/images/java1/3.png)


---


<b>3.关键字：</b>
This：类本身、或者当前对象的引用。This()可用在构造方法第一句，调用其他构造方法。

Super：不可以x.super.super，只能访问直接父类。构造方法中super()，可调用父类的构造方法。

Static：static中不可以用this和super，常驻内存直到程序结束

Final：修饰方法：方法不可重写！修饰类：类不可继承！修饰属性：不可改（常量的意思）！

动态可以调静态，静态不可以调动态

![](/images/java1/4.png)


---

<b>4.对象比较：</b>

![](/images/java1/5.png)



比如放新的对象：先比较hashcode再比较equal

Equal等，hashcode等
Equal不等，hashcode可等可不等



初赛编程题：做个人的类，可以放到SET里面：
```
public class Person {
 int age;
 String name;
   
 public boolean equals(Object obj){    //记得参数是Object
  if(obj   instanceof   Person){
  		Person p = (Person)obj;
  		return(name.equals(p.name) && age == p.age);
  }
 	 return super.equals(obj);
}
 public int hashCode(){
 	 return name.hashCode()+age;
}
 
 Person(Object n){
 }
 Person(String name,int age){
  this.age=age;
  this.name=name;
 }
 public int getAge(){
  return age;
 }
 public String getName(){
  return name;
 }
 public void setAge(int age){
  this.age=age;
 }
 public void setName(String name) {
 this.name=name;
}
}
```

1、当向集合Set中增加对象时，首先集合计算要增加对象的hashCode码，根据该值来得到一个位置用来存放当前对象，挡在该位置没有一个对象存在的话，那么集合Set认为该对象在集合中不存在，直接增加进去。如果在该位置有一个对象存在的话，接着将准备增加到集合中的对象与该位置上的对象进行equals方法比较，如果该equals方法返回false,那么集合认为集合中不存在该对象，在进行一次散列，将该对象放到散列后计算出的新地址里，如果equals方法返回true，那么集合认为集合中已经存在该对象了，不会再将该对象增加到集合中了。
    2、重写equals方法的时候必须重写hashCode方法。如果一个类的两个对象，使用equals方法比较时，结果为true,那么该两个对象具有相同的hashCode。原因是equals方法为true,表明是同一个对象，它们的hashCode当然相同。
    3、Ojbect类的hashCode方法返回的是Object对象的内存地址。可以通过Integer.toHexString(new Object().hashCode);来得到。


查看Object类的源码：

![](/images/java1/6.png)看到native，就是本地化的，根据本地机器来形成


![](/images/java1/7.png)比较两个对象的引用是否相等（当作比较地址）




例题：


![](/images/java1/8.png)


![](/images/java1/9.png)



答案：
D  A  B、C  A  B、D
