---
date: 2015-03-28
layout: post
title: 前端笔试中的一些JavaScript题目
categories: javascript
tags:  javascript
---

>考察this

<pre><code>
	var length = 10;
	function fn() {
		console.log(this.length);
	}

	var obj = {
		length: 5,
		method: function(fn) {
			fn();
			arguments[0]();
		}
	};
	obj.method(fn, 1);
</code>
</pre>

`输出：10 2`

取对象除了点操作符还可以用中括号，所以第二次执行时相当于arguments调用方法，this指向arguments，而这里传了两个参数，故输出arguments长度为2。

---

>var和函数的提前声明

<pre><code>
	function fn(a) {
		console.log(a);
		var a = 2;
		function a() {}
		console.log(a);
	}
	fn(1);
</code>
</pre>

`输出：function  a() {} 2`

var和function是会提前声明的，而且function是优先于var声明的（如果同时存在的话），所以提前声明后输出的a是个function，然后代码往下执行a进行重新赋值了，故第二次输出是2。

---

>局部变量和全局变量

<pre><code>
	var f = true;
	if (f === true) {
		var a = 10;
	}

	function fn() {
		var b = 20;
		c = 30;
	}

	fn();
	console.log(a);
	console.log(b);
	console.log(c);
</code>
</pre>

`输出：10 error`

只有function(){}内新声明的才能是局部变量，while{…}、if{…}、for(..) 之内的都是全局变量（除非本身包含在function内）。

---

>变量隐式声明

<pre><code>
	if('a' in window) {
		var a = 10;
	}

	alert(a);
</code>
</pre>

`输出：10`

代码还没执行前，a变量已经被声明，于是 ‘a’ in window 返回true，a被赋值。

---

>给基本类型数据添加属性，不报错，但取值时是undefined

<pre><code>
	var a = 10;
	a.pro = 10;
	console.log(a.pro + a);

	var s = 'hello';
	s.pro = 'world';
	console.log(s.pro + s);
</pre>

`输出：NaN undefinedhello`

给基本类型数据加属性不报错，但是引用的话返回undefined，10+undefined返回NaN，而undefined和string相加时转变成了字符串。

---

>函数声明优于变量声明

<pre><code>
	console.log(typeof fn);
	function fn() {};
	var fn;
</pre>

`输出：function`

在代码逐行执行前，函数声明和变量声明会提前进行，而函数声明又会优于变量声明，这里的优于可以理解为晚于变量声明后，如果函数名和变量名相同，函数声明就能覆盖变量声明。

---

>判断一个字符串中出现次数最多的字符，并统计次数

__使用正则表达式__

<pre><code>
	var s = 'aaabbbcccaaabbbaaabbbbbbbbbb';
	var a = s.split('');
	a.sort();
	s = a.join('');
	var pattern = /(\w)\1*/g;
	var ans = s.match(pattern);
	ans.sort(function(a, b) {
		return a.length < b.length;
	});;
	console.log(ans[0][0] + ': ' + ans[0].length);
</pre>

---

>URL参数解析

__请编写一个JavaScript函数 parseQueryString，它的用途是把URL参数解析为一个对象，如： var url =" http://localhost/index.php?key0=0&key1=1&key2=2"__

<pre><code>
	function parseQueryString(url) {
		var obj = {};
		var a = url.split('?');
		if(a === 1) return obj;
		var b = a[1].split('&');
		for(var i = 0, length = b.length; i < length; i++) {
			var c = b[i].split('=');
			obj[c[0]] = c[1];
		}
		return obj;
	}
	var url =" http://localhost/index.php?key0=0&key1=1&key2=2";
	var obj = parseQueryString(url);
	console.log(obj.key0, obj.key1, obj.key2);
</pre>