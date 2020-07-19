---
title: leetcdoe.209.长度最小的子数组-二分方法未写
categories:
  - 算法
tags:
  - leetcode
  - 数组
  - 双指针
  - 二分查找
  - 中等
comments: true
abbrlink: 13444
date: 2020-07-19 14:10:32
img:
---
### 题目描述

给定一个含有 n 个正整数的数组和一个正整数 s ，找出该数组中满足其和 ≥ s 的长度最小的连续子数组。如果不存在符合条件的连续子数组，返回 0。

示例: 

输入: s = 7, nums = [2,3,1,2,4,3]
输出: 2
解释: 子数组 [4,3] 是该条件下的长度最小的连续子数组。
进阶:

如果你已经完成了O(n) 时间复杂度的解法, 请尝试 O(n log n) 时间复杂度的解法。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/minimum-size-subarray-sum
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

标签 **数组** **双指针** **二分查找**

### 解法一：双指针，滑动窗口




```js
/**
 * @param {number} s
 * @param {number[]} nums
 * @return {number}
 */
var minSubArrayLen = function(s, nums) {
	let left = 0
	let right = -1 // 滑动窗口 nums[left...right]
	let sum = 0 // 记录找到的最大值
	let res = nums.length + 1 // 记录连续数组的长度

	while (left < nums.length) {
		if (right + 1 < nums.length && sum < s) {
			right++
			sum += nums[right]
		} else {
      sum -= nums[left]
      left++;
		}
		if (sum >= s) {
			res = Math.min(res, right - left + 1)
		}
	}
	if (res === nums.length+1) {
		return 0 // 没有找到答案返回0
	}
	return res  
};
```