---
title: 88.未完成，占坑
categories:
  - 算法
tags:
  - leetcode
comments: true
abbrlink: 39804
date: 2020-07-19 14:09:23
img:
---
<!--
 * @File: 
 * @Author: 张宏亮 - zhl@xiaoniren.cn
 * @Date: 2019-08-18 15:46:12
 * @LastEditors: 张宏亮<hongliang@yunshan.net>
 * @LastEditTime: 2019-09-30 15:49:46
 * @Description: file content
 * @Versions: 1.0.0
 -->
### 题目描述

给定两个有序整数数组 nums1 和 nums2，将 nums2 合并到 nums1 中，使得 num1 成为一个有序数组。

说明:
```
初始化 nums1 和 nums2 的元素数量分别为 m 和 n。
你可以假设 nums1 有足够的空间（空间大小大于或等于 m + n）来保存 nums2 中的元素。
```
示例:
```
输入:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

输出: [1,2,2,3,5,6]
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/merge-sorted-array
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

标签 **双指针** **数组**
### 解题思路



### 解法一：
唔。没学算法的解法。没啥用的。

时间复杂度较差，为O((n+m)log(n+m))
```js
/**
 * @param {number[]} nums1
 * @param {number} m
 * @param {number[]} nums2
 * @param {number} n
 * @return {void} Do not return anything, modify nums1 in-place instead.
 */
var merge = function(nums1, m, nums2, n) {
    nums1.splice(m,nums1.length)
    nums2.splice(n,nums2.length)
    nums1.push(...nums2)
    nums1.sort((a,b) => {
        return a - b
    })
};
```
