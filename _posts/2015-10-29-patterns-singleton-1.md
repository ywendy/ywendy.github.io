---
layout: post
title:  "java patterns."
category: patterns
tags:  java patterns singleton 单利模式.
---

#单利模式
##1、饿汗式
```java

package com.tony.base.patterns.singleton;

import java.lang.reflect.Constructor;

/**
 * <p>
 * 
 * 饿汗式 .缺点：1、没有lazy Load，在类被加载的时候就实例化对象。 2、可以通过反射得到许多新的实例对象.
 * </p>
 * 
 * @author TONY
 *
 */
public class Singleton1 {

	/**
	 * 通过私有的构造方法保证此类不能被new 出对象来
	 */
	private Singleton1() {

	}

	/**
	 * 使用static 关键字，保证此类加载的时候对instance变量初始化一次，可以保证此变量只有一个. 对于 new Singleton1()
	 * 这个对象是分配在堆内存里的，但是此变量被static修饰，属于类变量（全局变量） 被类的class对象引用，而类的class对象被Class
	 * loader引用，从而保证new 出的对相关在堆中不能垃圾 回收器回收，如果想回收掉此对象，需要卸载加载此类的class
	 * loader，同时永久代中的class被回收掉 ，此对象就可以被垃圾回收器回收掉.
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












