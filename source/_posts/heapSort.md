---
title: 曾经拦路虎系列——堆排序
date: 2016-05-17 15:02:52
tags: [算法, 排序]
---

# 前言

之前就没有好好学习过堆排序, 也是现在话时间填坑吧  
怎么说呢,现在掌握好过一辈子都学不会

# 定义

惯例:[维基百科传送门](https://zh.wikipedia.org/wiki/%E5%A0%86%E6%8E%92%E5%BA%8F#)  

## 核心思想

 - 堆化数据！—— 将数据想象成一个堆

# 算法说明

 1. 自底向上堆化数据
 2. 交换第一个(最大的)和末尾的节点
 3. 自顶向下调整堆(同时堆大小-1——最大的已经在最后一个了)
 4. 重复2-3步骤

## 结构上的关键点
 - 父节点i的左子节点在位置(2*i+1)
 - 父节点i的右子节点在位置(2*i+2)
 - 子节点i的父节点在位置floor((i-1)/2)

## 难理解的地方标注

 - 调整堆  

```
之前对于调整堆的操作有诸多疑问:
	- 为什么只需要跟一边的子节点比较就可以了?
	- 为什么只要向下调整，难道不会出现需要向上考虑的情况吗?

现在终于想明白了:
	- 调整便意味着数据已经堆化(从上到下大小不会乱)

...想不通的时候觉得十分难, 想通了也就这么一回事(以前太浪)
```
	
# 示例解法代码
```php
<?php
/**
 * 堆排序
 * 		
 * @param  array &$arr 
 * @return 
 */
function heapSort(&$arr)
{
	$len = count($arr);

	//建堆
	for ($i=intval(floor(($len-2)/2)); $i>=0; $i--) {
		heapify($arr, $i, $len);
	}

	while ($len > 1) {
		swap($arr[0], $arr[$len-1]);
		heapify($arr, 0, --$len);
	}
}

/**
 * 调整堆(基于子树都是最大堆的前提)
 * 
 * @param  array &$arr 数组
 * @param  int $node 节点位置
 * @param  int $len  当前堆大小(堆排也是就地排序的一种)
 * @return null       
 */
function heapify(&$arr, $node, $len)
{
	$child = 2*$node+1;

	if ($child > $len) 
		return;

	if (($child+1) < $len && $arr[$child+1] > $arr[$child])
		$child++;

	if ($arr[$node] <= $arr[$child]) {
		swap($arr[$node], $arr[$child]);
		heapify($arr, $child, $len);
	}
}

function swap(&$a, &$b)
{
	$tmp = $a;
	$a = $b;
	$b = $tmp;
}
```

# 特点
 - 平均 时间复杂度为:O(nlogn) 空间复杂度:O(1)
 - [为什么平均情况下快排比堆排序要优秀?](https://www.zhihu.com/question/23873747)
 - 思想没有快排优秀——比较次数比快排多(快排一般都能划分出两个严格的区分大小子集,堆排序不能)
 - [鼎力推荐！排序中信息的损耗](http://blog.csdn.net/pongba/article/details/2544933)