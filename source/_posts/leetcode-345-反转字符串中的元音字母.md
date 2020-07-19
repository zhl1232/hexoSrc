---
title: leetcode.345.反转字符串中的元音字母
categories:
  - 算法
tags:
  - leetcode
  - 双指针
  - 字符串
  - 简单
comments: true
abbrlink: 38257
date: 2020-07-19 14:11:06
img:
---
### 题目描述

给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。

说明：本题中，我们将空字符串定义为有效的回文串。

示例 1:
```
输入: "A man, a plan, a canal: Panama"
输出: true
```
示例 2:
```
输入: "race a car"
输出: false
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/valid-palindrome
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

标签 **双指针** **字符串**

### 解题思路

1. 用对撞指针，查看两指针是否为 ieaou 
2. 如两指针都是，交换，两指针都向中间移动
3. 如果其中一指针不是，该指针向中间移动，直到 2 或者循环条件结束 

### 解题方法
```js
/**
 * @param {string} s
 * @return {string}
 */
var reverseVowels = function(s) {
    let reg = /[ieaou]/i
    let left = 0;
    let right = s.length - 1;
    // 为了交换方便，也可以用其他方法交换
    let arr = s.split('')
    while(left < right) {
        if(reg.test(arr[left]) && reg.test(arr[right])) {
            [arr[left], arr[right]] = [arr[right], arr[left]]
            left++
            right--
        } else if(!reg.test(arr[left])) {
            left++
        } else if(!reg.test(arr[right])) {
           right-- 
        }  
    }

    return arr.join('')
};
```