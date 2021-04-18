---
layout:     post
title:     	Java equals（） 的作用
subtitle:    Java equals（）的作用
date:       2021-04-18
author:     wzk
header-img: img/home-bg-o.jpg
catalog: true
tags:
    - java基础
    - java
---

## 前言

每日学习总结记录


>关键词：java,基础

### Java equals（）
equals()的作用是用来判断两个对象是否相等。
equals（）在JDK的Object.java中，通过判断两个对象是否相等来区分它们是否相等。源码如下：  
```
public boolean equals(Object obj){
	return (this==obj);
}
```
既然Object.java中定义了equals()方法，这就意味着所有的Java类都实现了equals()方法，所有的类都可以通过equals()去比较两个对象是否相等。
但是，我们已经说过，使用默认的“equals()”方法，等价于“==”方法。因此，我们通常会重写equals()方法：若两个对象的内容相等，则equals()方法返回true；否则，返回fasle。
那么我们分为两个类别：  
(01) 若某个类没有覆盖equals()方法，当它的通过equals()比较两个对象时，实际上是比较两个对象是不是同一个对象。这时，等价于通过“==”去比较这两个对象。
(02) 我们可以覆盖类的equals()方法，来让equals()通过其它方式比较两个对象是否相等。通常的做法是：若两个对象的内容相等，则equals()方法返回true；否则，返回fasle。  
首先看没有覆盖equals（）方法：  
```
public class EqualsTest1 {
    public static void main(String[] args) {
        Person p1=new Person("eee",100);
        Person p2=new Person("eee",100);
        System.out.println(p1.equals(p2));
    }
    private static class Person {
        int age;
        String name;
        public Person(String name,int age){
            this.age=age;
            this.name=name;
        }

        @Override
        public String toString() {
            return "Person{" +
                    "age=" + age +
                    ", name='" + name + '\'' +
                    '}';
        }
}
}

结果：false
```
当我们调用equals（）方法的时候，其实还是调用的Object.equals()方法，相当于判断（p1==p2）的是两个是否是同一个对象。但是很明显
我们实例化的是两个对象。  
那么我们来重写一下equals（）方法，看看结果：
```
public class EqualsTest1 {
    public static void main(String[] args) {
        Person p1=new Person("eee",100);
        Person p2=new Person("eee",100);
        System.out.println(p1.equals(p2));
    }
    private static class Person {
        int age;
        String name;
        public Person(String name,int age){
            this.age=age;
            this.name=name;
        }

        @Override
        public String toString() {
            return "Person{" +
                    "age=" + age +
                    ", name='" + name + '\'' +
                    '}';
        }

        @Override
        public boolean equals(Object o) {
           if (o==null)return false;
           if (this==o)return true;
           if (this.getClass()!=o.getClass()){
               return false;
           }
            Person person = (Person) o;
            return name.equals(person.name)&& age==person.age;
        }
    }

}

结果：true

```
当我们重写了equals（）方法之后，我们判断两个对象对应的值只要是相等，就返回true，比较的不再是对象。  
那么总结一下equals（）方法：判断两个对象是否相等。但是可以自定义重写该方法。  
如果你有什么疑问或更好的理解，都可以联系我一起讨论。共同进步！如果本篇文章或者本博客对你有帮助，请给我点一个star吧！




 

