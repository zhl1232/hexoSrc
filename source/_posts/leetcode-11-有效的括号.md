---
title: leetcode.11.有效的括号
categories:
  - 算法
tags:
  - 数组
  - 双指针
  - leetcode
  - 中等
comments: true
abbrlink: 20826
date: 2020-07-19 13:41:00
img:
---

### 题目描述

给定 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

说明：你不能倾斜容器，且 n 的值至少为 2。

![image](https://raw.githubusercontent.com/zhl1232/javascript-algorithm/master/static/img/11.jpg)

图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。

示例:
```
输入: [1,8,6,2,5,4,8,3,7]
输出: 49
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/container-with-most-water
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

标签 **数组** **双指针**

### 解题思路

设置对撞指针 left，right，每次选两指针中的短板向中间移动1格，并且更新面积最大值 res，直到 i == j 时返回 res。

至于为什么移动短的指针不会漏掉最优解，下面这个是大神写的正确性证明。

[11题双指针正确性证明](https://leetcode-cn.com/problems/container-with-most-water/solution/shuang-zhi-zhen-fa-zheng-que-xing-zheng-ming-by-r3/)


下面这个可能容易理解点

![image](https://raw.githubusercontent.com/zhl1232/javascript-algorithm/master/static/img/11-1.png)

1. 原面积s = h(i) * w
2. 如果移动 j, 有两种肩况
3. 移动后 j' 的高度比i 高, s'= h(i) * (w-l) < s
4. 移动后 j' 的高度比i 低, s'= h(j') * (w-l) < s
5. 两种情况下, 移动后的面积s 都会小于s
所以可证， 只有移动较短边才有可能面积更大

### 解法一：双指针

```js
/**
 * @param {number[]} height
 * @return {number}
 */
var maxArea = function(height) {
    let res = 0
    let left = 0
    let right = height.length - 1
    while(left < right) {
        let h = Math.min(height[left], height[right])
        let w = right - left
        res = Math.max(h * w, res)
        if(height[left] < height[right]) {
            left++
        } else {
            right--
        }
    }
    return res
};
```