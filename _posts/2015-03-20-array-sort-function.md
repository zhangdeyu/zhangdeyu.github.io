---
date: 2015-03-20 09:22:30+00:00
layout: post
title: PHP数组排序基本方法
categories: php
tags:  array
---

#PHP数组排序方法
PHP共有四种基本的数组排序方法：

* 冒泡排序
* 选择排序
* 插入排序
* 快速排序

##冒泡排序

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