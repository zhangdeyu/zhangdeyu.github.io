---
date: 2015-04-25
layout: post
title: 浅谈js的冒泡机制
categories: javascript
tags:  javascript 冒泡
---

JavaScript中的冒泡问题来源很简单
>
比如当你在一个元素(element1)里面嵌套了一个元素(element2)，并且两个元素都分别对OnClick事件进行处理，那么当点击嵌套在里面的元素(element2)时，则elemet1以及elemet2的OnClick事件都被触发

---
对于冒泡事件，比较完整的解释是：***在一个对象上触发某类事件（比如单击onclick事件），如果此对象定义了此事件的处理程序，那么此事件就会调用这个处理程序，如果没有定义此事件处理程序或者事件返回true，那么这个事件会向这个对象的父级对象传播，从里到外，直至它被处理（父级对象所有同类事件都将被激活），或者它到达了对象层次的最顶层，即document对象（有些浏览器是window）。***

---

###对于冒泡的阻止

>
w3c的方法是e.stopPropagation()，IE则是使用e.cancelBubble = true


```window.event? window.event.cancelBubble = true : e.stopPropagation(); ```

###对于默认事件的阻止

>
w3c的方法是e.preventDefault()，IE则是使用e.returnValue = false;


```window.event? window.event.returnValue = false : e.preventDefault(); ```