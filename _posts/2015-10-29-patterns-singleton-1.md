---
layout: post
title:  "java patterns."
category: patterns
tags:  java patterns singleton 单利模式.
---

##单利模式
单利模式在软件开发中经常用到，是一种常见的开发模式.
此模式和spring中的单利作用域是不同的概念，在spring中，只是保证此对象的spring作用的
上下文里是一个实例。
单利模式UML图：
![](https://ywendy.github.io/img/java-patterns-singleton.png)

单利模式有很多种写法，这里实现几种简单的写法，并做简单的分析，记录！	
###1、饿汗式
```java

package com.tony.base.patterns.singleton;

import java.lang.reflect.Constructor;

/**
 * 
 * 饿汗式 . 缺点:<br>
 * 1、没有lazy Load，在类被加载的时候就实例化对象。<br>
 * 2、可以通过反射得到许多新的实例对象.
 * 
 * @author TONY
 */
public class Singleton1 {

	/**
	 * 通过私有的构造方法保证此类不能被new 出对象来
	 */
	private Singleton1() {
	}

	/**
	 * 使用static 关键字，保证此类加载的时候对instance变量初始化一次，可以保证此变量只有一个.
	 * <p>
	 * 对于 new Singleton1() 这个对象是分配在堆内存里的，但是此变量被static修饰，<br>
	 * 属于类变量（全局变量） 被类的class 对象引用，而类的class对象被Class loader引用，<br>
	 * 从而保证new 出的对相关在堆中不能垃圾回收器回收.
	 * </p>
	 * 如果想回收掉此对象，需要卸载加载此类的class loader，同时永久代中的class被回收掉 ，<br>
	 * 此对象就可以被垃圾回收器回收掉.
	 */
	private static Singleton1 instance = new Singleton1();

	/**
	 * 提供一个对外公开访问的方法，返回此实例对象.
	 * 
	 * @return instance {@code Singleton1}.
	 */
	public static Singleton1 getInstance() {
		return instance;
	}

	public static void main(String[] args) throws Exception {
		/* 正常的通过静态方法获取对象，每次获取的都是同一个对象. */
		Singleton1 sg1 = Singleton1.getInstance();
		Singleton1 sg2 = Singleton1.getInstance();
		System.out.println("通过单利模式获取的对象equals比较：" + sg1.equals(sg2));
		System.out.println("单利模式实例对象1：" + sg1);
		System.out.println("单利模式实例对象2：" + sg2);

		/* 通过反射获取实例对象，可以构造出多个实例对象出来 */
		Constructor<Singleton1> con = Singleton1.class.getDeclaredConstructor();
		con.setAccessible(true);
		Singleton1 s1 = con.newInstance();
		Singleton1 s2 = con.newInstance();
		System.out.println("通过反射获取单利对象equals比较：" + s1.equals(s2));
		System.out.println("反射获取的对象1：" + s1);
		System.out.println("反射获取对象2：" + s2);
	}
}

```
###2、懒汉式
懒汉式：主要是保证实例的创建，在使用的时候才初始化一次。如果不使用，此实例不会被初始化。

####2.1同步方法写法
分析过程如第一种单例代码里。

```javascript

public class Singleton2 {

	private Singleton2() {
	}

	private static Singleton2 instance;

	public synchronized Singleton2 getInstance() {
		if (instance == null) {
			instance = new Singleton2();
		}
		return instance;
	}
}

```
####2.2双检锁写法
此种写法，避免代码重排。使用volaticle 关键字，遵照happen-before 法则，从而可以保证
实例对象不会被创建多次.

```java

public class Singleton3 {

	private Singleton3() {
	}

	public static volatile Singleton3 instance;

	public Singleton3 getInstance() {
		if (instance == null) {
			synchronized (instance) {
				if (instance == null) {
					instance = new Singleton3();
				}
			}
		}
		return instance;
	}
}

```

###3、通过内部类的方式实现单例
此种方式使用一个静态内部类去实现单例的对象创建，静态内部类声明为私有的，只有在当前类里可以调用
所以，SingletonHolder 的初始化只有在调用getInstance()方法时才能被初始化。
由于是静态的，分析过程请查看第一种单例的代码中的注释。
```java
public class Singleton4 {

	private Singleton4() {
	}

	private static class SingletonHolder {
		public static Singleton4 instance = new Singleton4();
	}

	public static Singleton4 getInstance() {
		return SingletonHolder.instance;
	}
	
	
	public static void main(String[] args) {
		Singleton4 s1 = Singleton4.getInstance();
		Singleton4 s2 = Singleton4.getInstance();
		System.out.println("单例对象1:"+s1);
		System.out.println("单例对象2:"+s2);
		System.out.println("单例对象比较"+s1.equals(s2));
		
	}

```
###4、通过枚举实现单例Enum

```java
public enum Singleton5 {

	INSTANCE;
	public static Singleton5 getInstance() {
		return INSTANCE;
	}

}

```











