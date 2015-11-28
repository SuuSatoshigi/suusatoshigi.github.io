title: Java竞赛赛前复习(二)(省略参数与变长参数方法的优化)
date: 2014-04-24 10:21
tags: [Java,竞赛前复习]
categories: 辅助攻击技能 #文章文类
---

<b>变长参数方法的优化 </b>
Java7之前版本中的变长参数方法： 

```
    public int sum(int... args) {
        int result = 0;
        for (int value : args) {
            result += value;
        }
        return result;
    }
//当参数为不可具体化的类型时，如List，编译器将产生警告，需要使用@SuppressWarnings("unchecked")注解声明；Java7中使用@SafeVarargs注解抑制编译器警告。
    @SafeVarargs
    public static <T> T useVarargs(T... args) {
        return args.length > 0 ? args[0] : null;
}
```

这个被取代：

```
VarargsWarning.useVarargs(new ArrayList<String>());

```

讲这个知识点是因为我们初赛的时候遇到了这个

初赛编程题：
![](/images/java2/1.jpg)


这是我写出来的，不知道对不对，只是输出一样：

```

public class ToList<E> {

java.util.List<E> list = new java.util.ArrayList<E>();
ToList<E> add(E ...  args){
    for (E s :  args) {
    	list.add(s);
    }
    return this;
}
java.util.List<E> toList(){
return list; 
}
static ToList create(Object o1,Object o2,Object o3){
java.util.List list = new java.util.ArrayList();
list.add(o1);
list.add(o2);
list.add(o3);

ToList t = new ToList();
t.list = list;
return t;
}
}
```


这个是没有用省略参数前的代码：

```
public class ToList<E> {
java.util.List<E> list = new java.util.ArrayList<E>();
ToList<E> add(E s1){
list.add(s1);
    return this;
}
ToList<E> add(E s1,E s2){
list.add(s1);
list.add(s2);
    return this;
}
ToList<E> add(E s1,E s2,E s3){
list.add(s1);
list.add(s2);
list.add(s3);
    return this;
}
ToList<E> add(E s1,E s2,E s3,E s4){
list.add(s1);
list.add(s2);
list.add(s3);
list.add(s4);
return this;
}
java.util.List<E> toList(){
return list; 
}
static ToList create(Object o1,Object o2,Object o3){
java.util.List list = new java.util.ArrayList();
list.add(o1);
list.add(o2);
list.add(o3);

ToList t = new ToList();
t.list = list;
return t;
}
}
```
