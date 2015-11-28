title: 设计模式之适配器模式
date: 2015-05-16 16:57
tags: [设计模式（Java）]
categories: 辅助攻击技能 #文章文类
---

适配器模式我第一次接触的时候是在刚入大学的时候自学安卓接触到的，当初c语言还没学多少，感觉一头雾水，现在趁着学设计模式，把这部分知识补一下，大牛勿喷。

百度百科说，适配器模式（有时候也称包装样式或者包装）将一个类的接口适配成用户所期待的。
综上，适配器模式：原本的接口不能直接使用在用户写的代码（数据参数不同之类的原因），用户想办法使得该接口可以被适配使用，这种模式是叫适配器模式。
这一点挺重要，因为我问一些同学适配器模式是什么的时候，他们毫不犹豫说，不就是委托嘛！天真的我还信了半个小时看完书之后立刻咆哮，欺负我读书少！委托和适配器并没有关系，委托一般就是当某个事件发生时通知相关的类进行处理（这是一对一的），适配器就是适配，写个中间类。

<b>对象适配器</b>
适配类在类中实例化一个所需适配类的对象，并调用此对象的方法实现适配

```
//被适配的adaptee
public class Adaptee {
	public int bigger(int a, int b) {
	 	return Math.max(a, b);
	}
}
//适配器Adapter
public class ObjectAdapter implements ObjectTarget{
    private Adaptee bigger = new Adaptee();
    public char bigger(char a,char b) {
    	return (char)bigger.bigger((int) a, (int) b);
    }
}
//客户期待得到的接口
public interface  ObjectTarget {
	public char bigger(char a,char b);
}
```

<b>类适配器</b>
类适配器，ClassAdapter类既继承了 Adaptee （被适配类），也实现了 通用 target接口。

```
//	类适配器
	public class ClassAdapter extends Adaptee implements Target{
	public char bigger(char a, char b) {
		return (char) bigger((int)a,(int)b);
	}
}
//被适配的adaptee
public class Adaptee {
	public int bigger(int a, int b) {
		
		return Math.max(a, b);
	}
}

//客户期待获得的接口
public interface  Target{
	public char bigger(char a,char b);
}
```
