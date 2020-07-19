---
title: leetcode.349.两个数组的交集
categories:
  - 算法
tags:
  - leetcode
  - 双指针
  - 哈希表
  - 排序
  - 二分查找
  - 简单
comments: true
abbrlink: 15820
date: 2020-07-19 14:11:18
img:
---
<!--
 * @File: 
 * @Author: 张宏亮 - zhl@xiaoniren.cn
 * @Date: 2019-08-09 23:03:47
 * @LastEditors: 张宏亮<zhl@xiaoniren.cn>
 * @LastEditTime: 2019-08-09 23:57:06
 * @Description: file content
 * @Versions: 1.0.0
 -->
### 题目描述

给定两个数组，编写一个函数来计算它们的交集。

示例 1:
```
输入: nums1 = [1,2,2,1], nums2 = [2,2]
输出: [2]
```
示例 2:
```
输入: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出: [9,4]
```
说明:
```
输出结果中的每个元素一定是唯一的。
我们可以不考虑输出结果的顺序。
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/intersection-of-two-arrays
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

标签 **排序** **哈希表** **双指针** **二分查找**

### 解法一 哈希表
时间复杂度：O(m+n)

利用哈希集合值唯一的特性。

```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
var intersection = function(nums1, nums2) {
    let hash1 = new Set(nums1)
    let hash2 = new Set()

    for(let i = 0; i < nums2.length; i++) {
        if(hash1.has(nums2[i])){
            hash2.add(nums2[i])
        }
    }
    return [...hash2]
};
```

### 解法二 双指针，排序

因为标签里有双指针和排序就尝试了下。

执行时间会很长，排序后把数组先去重会好一点。
```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
var intersection = function(nums1, nums2) {
    nums1 = nums1.sort((a,b) => a - b)
    nums2 = nums2.sort((a,b) => a - b)
    
    let p1 = p2 = 0
    let res = new Set()
    while(p1 < nums1.length && p2 < nums2.length) {
        if(nums1[p1] < nums2[p2]) {
            p1++
        } else if(nums1[p1] == nums2[p2]){
            res.add(nums1[p1])
            p1++
            p2++
        } else {
            p2++
        }
    }
    return [...res]
};
```
###  解法三: 数组api

```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
var intersection = function(nums1, nums2) {
    return [...new Set(nums1.filter(v => nums2.includes(v)))]
};
```