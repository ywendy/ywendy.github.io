---
layout: post
title:  "String 字符串反转（reverse）方法."
category: java 基础.
tags: java 基础 reverse String
---


##字符串反转方法。


```java
package com.wendy.test.string;

/**
 * <b>time:</b>2015年3月12日
 *
 * @author admin
 *
 */
public class StringReverse {

	/* 适用中间值mid. */
	public static String reverse(String source) {
		if (source == null || source.length() <= 1) {
			return source;
		}
		char[] array = source.toCharArray();
		int size = array.length;
		int mid = size >> 1;
		int index = 0;
		while (index < mid) {
			int opLength = size - index - 1;
			array[index] ^= array[opLength];
			array[opLength] ^= array[index];
			array[index] ^= array[opLength];
			index++;
		}
		return new String(array);
	}

	/* 不适用mid中间值. */
	public static String reverse2(String source) {
		if (source == null || source.length() <= 1) {
			return source;
		}
		char[] arr = source.toCharArray();
		int len = arr.length - 1;
		for (int i = 0; i < len; i++, len--) {
			arr[i] ^= arr[len];
			arr[len] ^= arr[i];
			arr[i] ^= arr[len];
		}
		return new String(arr);
	}

	/* 递归. */
	public static String reverse3(String source) {
		if (source == null || source.length() <= 1) {
			return source;
		}
		return reverse3(source.substring(1)) + source.charAt(0);
	}

	public static void main(String[] args) {

		System.out.println("reverse===" + reverse("I am in bj"));
		System.out.println("reverse2===" + reverse2("I am in bj"));
		System.out.println("reverse3===" + reverse3("I am in bj"));

	}

}



```