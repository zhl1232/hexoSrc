---
title: leetcode.283.移动零
categories:
  - 算法
tags:
  - leetcode
  - 数组
  - 双指针
  - 简单
comments: true
abbrlink: 28492
date: 2020-07-19 14:10:51
img:
---
<!--
 * @File: 
 * @Author: 张宏亮 - zhl@xiaoniren.cn
 * @Date: 2019-08-18 15:46:12
 * @LastEditors: 张宏亮<zhl@xiaoniren.cn>
 * @LastEditTime: 2019-08-18 16:40:56
 * @Description: file content
 * @Versions: 1.0.0
 -->
### 题目描述

给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。

示例:
```
输入: [0,1,0,3,12]
输出: [1,3,12,0,0]
```
说明:

- 必须在原数组上操作，不能拷贝额外的数组。
- 尽量减少操作次数。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/move-zeroes
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

标签 **双指针** **数组**
### 解题思路

解法一：数组API

时间复杂度O(N)

对数组 API 熟悉，遍历数组，如果是 0 ，直接操作移到数组末尾。


```js
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var moveZeroes = function(nums) {
    let temp = 0

    for(let i = 0; i < nums.length; i++) {
        if(nums[temp] === 0) {
            nums.splice(temp, 1)
            nums[nums.length] = 0
        } else {
            temp++
        }
    }
};
```


方法二：双指针/初始定义

首先遍历一遍数列，用另个数列按顺序存储所有非 0 的元素，在将存储的非零元素按顺序复制到原数列中，空位补 0 即可。

![image](https://raw.githubusercontent.com/zhl1232/javascript-algorithm/master/static/img/283.png)

直观的解题思路需要新建额外的数组，不符合要求，但是对于我们下面的优化算法很有起始。

只要把数组中所有的非零元素，按顺序给数组的前段元素位赋值，剩下的全部直接赋值 0。我们定义一个初始变量，为非 0 元素的数组下标，之后在遍历数列的时候不断维护这个定义。

```js

/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var moveZeroes = function(nums) {
    let lastNotZero = 0
    for(let i = 0; i < nums.length; i++) {
        if(nums[i]) {
            nums[lastNotZero++] = nums[i]
        }
    }
    for(let i = lastNotZero; i < nums.length; i++) {
        nums[i] = 0
    }
};

```