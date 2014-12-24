---
layout: post
title:  "javascript 重写字符串对象的toString方法"
category: javascript
tags: javascript
---

##重写javaScript的toString（）方法
	



```javascript
String.prototype.toString = function() {

	return 2;
}

var str1 = "a";
var str2 = "b";
console.log(str1.toString() + str2.toString());



```
