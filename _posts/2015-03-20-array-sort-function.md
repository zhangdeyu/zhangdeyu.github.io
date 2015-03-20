---
date: 2015-03-20
layout: post
title: PHP实现四种基本排序方法
categories: php
tags:  array
---

#PHP实现四种基本排序方法
数组有四种基本的排序方法：

* 冒泡排序
* 选择排序
* 插入排序
* 快速排序

---
本文仅针对一维数组进行简单排序

---
##冒泡排序
>基本思想：两两比较，发现两数值的次序相反时进行交换

```
function bubblesort($arr){
    $len=count($arr);
	for ($i=0; $i <$len-1; $i++) {
		for ($j=$i+1; $j <$len; $j++) {
			if ($arr[$j]<$arr[$i]) {
				$tmp=$arr[$i];
				$arr[$i]=$arr[$j];
				$arr[$j]=$tmp;
			}
		}
	}
	return $arr;
}
```
##选择排序
>基本思想：对比数组中前一个元素跟后一个元素的大小，如果后面的元素比前面的元素小则用一个变量来记住他的位置，接着第二次比较，前面“后一个元素”现变成了“前一个元素”，继续跟他的“后一个元素”进行比较如果后面的元素比他要小则用变量k记住它在数组中的位置(下标)，等到循环结束的时候，我们应该找到了最小的那个数的下标了，然后进行判断，如果这个元素的下标不是第一个元素的下标，就让第一个元素跟他交换一下值，这样就找到整个数组中最小的数了。然后找到数组中第二小的数，让他跟数组中第二个元素交换一下值，以此类推。

```
function select($arr){
    for ($i=0; $i <count($arr)-1; $i++) {
		$p=$i;
		for ($j=$i+1; $j <count($arr); $j++) {
			if($arr[$p]>$arr[$j]){
				$p=$j;
			}
		}
		if ($p!=$i) {
			$tmp=$arr[$i];
			$arr[$i]=$arr[$p];
			$arr[$p]=$tmp;
		}
	}
	return $arr;
}
```

##插入排序
>基本思想：每次将一个待排序的元素，按其数值的大小插入到前面已经排好序的子数组中的适当位置，直到全部元素插入完成为止。

```
function insertsort($arr){
    $len=count($arr);
	for ($i=1; $i <$len; $i++) {
		$tmp=$arr[$i];
		for ($j=$i-1; $j >=0 ; $j--) {
			if ($tmp<$arr[$j]) {
				$arr[$j+1]=$arr[$j];
				$arr[$j]=$tmp;
			}
		}
	}
	return $arr;
}
```

##快速排序
>基本思想：快速排序（Quicksort）是对冒泡排序的一种改进，通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。

```
function quicksort($arr){
    $len=count($arr);
	if($len>1){
		$middle=$arr[0];
		$left=array();
		$right=array();
		for ($i=1; $i <$len; $i++) {
			if($arr[$i]>$middle){
				$right[]=$arr[$i];
			}else{
				$left[]=$arr[$i];
			}
		}
		$left=quicksort($left);
		$right=quicksort($right);
		return array_merge($left,array($middle),$right);
	}else{
		return $arr;
	}
}
```