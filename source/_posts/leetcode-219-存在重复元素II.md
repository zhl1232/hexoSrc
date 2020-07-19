---
title: leetcode.219.存在重复元素II
categories:
  - 算法
tags:
  - leetcode
  - 哈希表
  - 数组
  - 简单
comments: true
abbrlink: 42524
date: 2020-07-19 14:10:43
img:
---
<!--
 * @File: 
 * @Author: 张宏亮 - zhl@xiaoniren.cn
 * @Date: 2019-07-19 00:38:41
 * @LastEditors: 张宏亮<zhl@xiaoniren.cn>
 * @LastEditTime: 2019-07-19 00:38:41
 * @Description: file content
 * @Versions: 1.0.0
 -->
### 题目描述

给定一个整数数组和一个整数 k，判断数组中是否存在两个不同的索引 i 和 j，使得 nums [i] = nums [j]，并且 i 和 j 的差的绝对值最大为 k。

示例 1:
```
输入: nums = [1,2,3,1], k = 3
输出: true
```
示例 2:
```
输入: nums = [1,0,1,1], k = 1
输出: true
```
示例 3:
```
输入: nums = [1,2,3,1,2,3], k = 2
输出: false
```

标签 **哈希表** **数组**

https://leetcode-cn.com/problems/contains-duplicate-ii/

### 解题思路

时间复杂度O(n)

1. 遍历数组，如果当前值不存在hash表里，把值->key,下标->value,存进hash表
2. 如果当前值在hash表里存在，看下两个值下标的绝对值是否 <= k
3. 如果 <= k，返回true
4. 否则，更新当前值的下标。因为之前的都不成功，如果有下一个相同元素的话绝对值会更大。
5. 循环完成还没有匹配成功，返回false


```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {boolean}
 */
var containsNearbyDuplicate = function(nums, k) {
    let hash = new Map()
    
    for(let i = 0; i < nums.length; i++) {
        if(hash.has(nums[i])) {
            if(Math.abs(hash.get(nums[i]) - i) <= k) {
                return true
            } else {
                hash.set(nums[i], i)
            }
        } else {
            hash.set(nums[i], i)
        }
    }
    return false
};
```

官方解题的思路

1. 用哈希表来维护这个k大小的滑动窗口。
2. 遍历数组，对于每个元素做以下操作：
- 在哈希表中搜索当前元素，如果找到了就返回 true。
- 在哈希表中插入当前元素。
- 如果当前哈希表的大小超过了 k，删除哈希表中最旧的元素。
- 返回 false。


时间复杂度：O(n)，n为数组长度

```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {boolean}
 */
var containsNearbyDuplicate = function(nums, k) {
    const set = new Set();
    for(let i = 0; i < nums.length; i++) {
        if(set.has(nums[i])) {
            return true;
        }
        set.add(nums[i]);
        if(set.size > k) {
            set.delete(nums[i - k]);
        }
    }
    return false;
};
```