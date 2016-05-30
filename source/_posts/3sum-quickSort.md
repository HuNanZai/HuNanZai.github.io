---
title: 3sum_quickSort
date: 2016-05-06 15:32:37
tags: [算法, leetecode, 排序]
---

# KSum问题

对于leetcode上类似的问题以及博客有很多，以下是我的个人总结

## 解决思路
1. 排序(去除部分重复的情况比如-1 -1 -1 0...就只需要判断一个-1即可)
2. hashtable第二次去重

### 示例代码
```javascript
//针对leetcode上的ThreeNum问题
//排序用的下文的排序
var threeSum = function(nums) {
    //特殊情况考虑
    if (nums.length < 3) {
        return [];
    }
    
    //quick sort!
    quickSort(nums, 0, nums.length-1);
    
    //异常情况过滤
    if (nums[0] > 0 || nums[nums.length-1] < 0) {
        return [];
    }

    var result = [];
    var log = {};
    var last_num_i;
    for (var i=0; i<nums.length-2; i++) {
        var num_i = nums[i];
        if (last_num_i === num_i) continue;

        for (var j=i+1; j<nums.length-1; j++) {
            var num_j = nums[j];
            for (var k=j+1; k<nums.length; k++) {
                var num_k = nums[k];

                if (num_i + num_j + num_k === 0) {
                    var tmp = [num_i, num_j, num_k];
                    quickSort(tmp, 0, 2);
                    var key = tmp.join('_');
                    if (!log[key]) {
                        result.push(tmp);
                        log[key] = 1;
                    }
                }
            }
        }
        
        last_num_i = num_i;
    }

    return result;
};
```

# 快速排序
- [动态算法演示网站](http://jsdo.it/norahiko/oxIy/fullscreen)

## 核心思想
原理弄清楚以后还是特别简单的：  

	1. 利用一定的规则（中位数或者whatever）从数组中选择位置k作为中心点
	2. 将数据根据中心点分为：A:{<中位数集合}中位数(pivot)B:{>中位数集合}
	3. 对于子集A\B分别在应用1、2步骤直到个数为1

其中在步骤2中的细节步骤为：  

	1. 初始化i\j两个游标对应开头和结尾
	2. 如果第i个数比pivot大，则交换位置
	3. 如果第j个数比pivot小，则交换位置
	4. 移动i,j直到相遇

其中之间我特别不理解交换位置这个操作。
但是现在已经理解得比较清楚了:

	1. 发生位置交换: 集合A或者B中出现了不属于该集合的数
	2. 交换的实际意义是把需要交换的数放到正确的集合中(<i的位置属于A, >j的位置属于B)
	3. 当i\j相遇的时候，就是pivot应该在的位置

## 特点
	- 性能可以(最好nlogn 最坏n*n)
	- 不稳定(相同的值相对的位置排序完成之后可能发生变化)

## 优化
	- 对于pivot的选择特殊情况下可以优化

## 示例代码
### php
```php
function quickSort(&$arr)
{
	quickSortByPos($arr, 0, count($arr)-1);
	return $arr;
}

function quickSortByPos(&$arr, $begin, $end)
{
	if ($begin >= $end) {
		return;
	}
	$i = $begin;
	$j = $end;
	$pos = intval(floor(($begin+$end)/2));
	$compare	= $arr[$pos];

	while ($i<$j) {
		if ($arr[$i] > $compare) {
			$arr[$pos] = $arr[$i];
			$pos = $i;
		} else {
			$i++;
		}
		if ($arr[$j] < $compare) {
			$arr[$pos] = $arr[$j];
			$pos = $j;
		} else {
			$j--;
		}
	}
	$arr[$pos] = $compare;

	quickSortByPos($arr, $begin, $pos-1);
	quickSortByPos($arr, $pos+1, $end);
}
```

### javascript
```javascript
var quickSort = function (arr, start, end) {
    if (start>=end) {
        return;
    }
    var i, j, pos, compare;
    i = start;
    j = end;
    pos = Math.floor((start+end)/2);

    compare = arr[pos];
    while (i<j) {
        if (arr[i]>compare) {
            arr[pos] = arr[i];
            pos = i;
        } else {
            i++;
        }
        if (arr[j]<compare) {
            arr[pos] = arr[j];
            pos = j;
        } else {
            j--;
        }
    }
    arr[pos] = compare;

    quickSort(arr, start, pos-1);
    quickSort(arr, pos+1, end);
}
```