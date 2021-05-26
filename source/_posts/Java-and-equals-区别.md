---
title: Java ==  equals() 区别
catalog: true
date: 2021-04-07 22:15:13
subtitle: Difference between == and equals() in Java
header-img:
tags:
- Array
categories:
- TECH
- BackEnd
- Java
---

# Java ==  equals() 区别

类型 | == | `equals()`
---------|----------|----------
类型 | operator 运算符|method 方法
基本类型 | 值是否相同，本质是比较其中的字节组合是否相同。```int a = 3; byte b = 3; if(a == b) {} // true``` a 和 b 的字节码都是0000000011 == 00000011（忽略a有更多的0）| 
引用类型 | 引用变量是否相同，本质同样是是比较引用变量（对象在堆中的地址）的字节组合是否相同。```Foo a = new Foo(); Foo b = new Foo(); Foo c = a; if(a == b) {} // false if(a == c) {} // true if(c == b) {} // false``` 对象是存储在堆上的，这里的a， b， c都是对象的引用变量（堆中的地址），而非堆上的对象的值。| 1 如果是未被父类或自身重载override过，则与==相同 。Object类的equals方法：```public boolean equals(Object obj) {return (this == obj);}``` 2 如果像String 和 Integer 等重载了 equals 方法，把它变成了对象的值比较。


# 参考文章

- [What is the difference between == and equals() in Java?](https://stackoverflow.com/questions/7520432/what-is-the-difference-between-and-equals-in-java)