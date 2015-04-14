---
layout: post
title:  "java 接口介绍."
category: java
tags: java 基础
---


##java-interface
An interface is a collection of abstract methods. A class implements an interface, thereby inheriting the abstract methods of the interface.

翻译：接口是抽象方法的集合，一个类可以实现一个接口，因而继承接口中的方法.

An interface is not a class. Writing an interface is similar to writing a class, but they are two different concepts. A class describes the attributes and behaviors of an object. An interface contains behaviors that a class implements.

翻译：接口不是类，写接口和写类比较类似，但是他们是两个不同的概念。类描述了对象的属性和行为，接口只包含行为供类去实现.

##Extending Interfaces(继承接口):
An interface can extend another interface, similarly to the way that a class can extend another class. The extends keyword is used to extend an interface, and the child interface inherits the methods of the parent interface.

翻译：接口可以继承其他的接口

The following Sports interface is extended by Hockey and Football interfaces.

```
//Filename: Sports.java public interface Sports { public void setHomeTeam(String name); public void setVisitingTeam(String name); } //Filename: Football.java public interface Football extends Sports { public void homeTeamScored(int points); public void visitingTeamScored(int points); public void endOfQuarter(int quarter); } //Filename: Hockey.java public interface Hockey extends Sports { public void homeGoalScored(); public void visitingGoalScored();

```java














