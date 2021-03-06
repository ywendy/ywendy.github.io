---
layout: post
title:  "java 接口介绍."
category: java
tags: java 基础
---

##Tagging Interfaces:

An interface with no methods in it is referred to as a tagging interface. 
There are two basic design purposes of tagging interfaces: 
Creates a common parent: As with the EventListener interface, 
which is extended by dozens of other interfaces in the Java API, 
you can use a tagging interface to create a common parent among a group of interfaces. 
For example, when an interface extends EventListener, 
the JVM knows that this particular interface is going to be used in an event delegation scenario. 





####翻译：
一个没有方法的接口被作为一个标记接口引用。关于标记接口有两个基本的设计目的：
####1、Creates a common parent：（创建一个通用的父类）
向EventListener接口一样，在javaAPI中可以被多个接口继承.
你可以使用一个标记接口去创建一个通用的、有个共同父类的接口在组之间。（意思就是可以创建一个标记接口组，标记一组行为）


####Adds a data type to a class: 
This situation is where the term tagging comes from. 
A class that implements a tagging interface does not need to define any methods 
(since the interface does not have any), but the class becomes an interface type through polymorphism.

这种情况用来标记来自于哪里。一个实现标记接口的类，不是必要去定义很多行为方法,但是可以通过多态变成一个接口类型.
例子：spring ware



##java-interface:
An interface is a collection of abstract methods. A class implements an interface, thereby inheriting the abstract methods of the interface.

翻译：接口是抽象方法的集合，一个类可以实现一个接口，因而继承接口中的方法.

An interface is not a class. Writing an interface is similar to writing a class, but they are two different concepts. A class describes the attributes and behaviors of an object. An interface contains behaviors that a class implements.

翻译：接口不是类，写接口和写类比较类似，但是他们是两个不同的概念。类描述了对象的属性和行为，接口只包含行为供类去实现.

##Extending Interfaces(继承接口):
An interface can extend another interface, similarly to the way that a class can extend another class. The extends keyword is used to extend an interface, and the child interface inherits the methods of the parent interface.

翻译：接口可以继承其他的接口

The following Sports interface is extended by Hockey and Football interfaces.

```
package org.wendy.interfaces;

public interface Sports {

	public void setHomeTeam(String name);

	public void setVisitingTeam(String name);

}


package org.wendy.interfaces;

public interface Football extends Sports {

	public void homeTeamScored(int points);

	public void visitingTeamScored(int points);

	public void endOfQuarter(int quarter);

}

package org.wendy.interfaces;

public interface Hockey extends Sports {

	public void homeGoalScored();

	public void visitingGoalScored();

	public void endOfPeriod(int period);

	public void overtimePeriod(int ot);

}


```
The Hockey interface has four methods, but it inherits two from Sports; thus,
 a class that implements Hockey needs to implement all six methods. 
 Similarly, a class that implements Football needs to define the three methods from Football and the two methods from Sports.

翻译：接口Hockey 有4个方法，但是他从Sport接口中继承了2个方法，因而，一个类去实现Hockey接口，需要去
实现6个方法，相似的是一个类实现接口Football 必须去实现Football中的三个方法和Sports中的2个方法。















