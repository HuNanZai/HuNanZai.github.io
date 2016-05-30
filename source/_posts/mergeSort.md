---
title: 曾经的拦路虎系列——归并排序
date: 2016-05-18 16:50:32
tags: [算法, 排序]
---

# 前言

什么是分治法?  

将一个比较大问题划分为许多小问题来解决,之后将小结果统一得到大结果

 - 类似hadoop中的map/reduce
 - 快排\归并 排序都属于这类

# 算法介绍

[维基传送门](https://zh.wikipedia.org/wiki/归并排序)

## 模式介绍

### 迭代法
	1. 申请空间，使其大小为两个已经排序序列之和，该空间用来存放合并后的序列
	2. 设定两个指针，最初位置分别为两个已经排序序列的起始位置
	3. 比较两个指针所指向的元素，选择相对小的元素放入到合并空间，并移动指针到下一位置
	4. 重复步骤3直到某一指针到达序列尾
	5. 将另一序列剩下的所有元素直接复制到合并序列尾

### 递归法
	1. 将序列每相邻两个数字进行归并操作，形成floor(n/2)个序列，排序后每个序列包含两个元素
	2. 将上述序列再次归并，形成floor(n/4)个序列，每个序列包含四个元素
	3. 重复步骤2，直到所有元素排序完毕

# 算法实现代码
```php
<?php
/**
 * 新的归并排序写法
 *
 * 涉及到的原生函数:
 * 		count:
 * 		array_chunk: 将一个数组按照个数分割
 * 		array_shift: 删除数组中第一个元素,并返回其值
 * 		array_merge: 将多个数组合并为一个
 */
function mergeSort(&$arr)
{
	$len = count($arr);
	if ($len == 1) 
		return;
	//分
	$mid = ($len>>1) + ($len&1);
	$tmp = array_chunk($arr, $mid);
	$left = $tmp[0];
	$right = $tmp[1];
	//治
	mergeSort($left);
	mergeSort($right);
	//合
	$arr = [];
	while (isset($left[0]) && isset($right[0])) {
		if ($left[0] > $right[0]) {
			$arr[] = array_shift($right);
		} else {
			$arr[] = array_shift($left);
		}
	}
	$arr = array_merge($arr, $left, $right);
}

```
## 代码贴士
 - 计算中位数的表达式: ($len>>1) + ($len&1)
 - 利用&可以有效减少大数组的拷贝

# 总结
 - 效率: O(nlogn)

比较简单,记住中间的分治法的思想！