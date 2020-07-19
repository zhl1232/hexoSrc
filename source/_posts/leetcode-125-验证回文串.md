---
title: leetcode.125.验证回文串
categories:
  - 算法
tags:
  - leetcode
  - 字符串
  - 双指针
  - 简单
comments: true
abbrlink: 12585
date: 2020-07-19 14:09:37
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

1. 处理字符串，只考虑字母和数字字符，忽略字母的大小写
2. 用对撞指针，递归查看首尾是否一致即是否回文串
### 解题方法
```js
/**
 * @param {string} s
 * @return {boolean}
 */
var isPalindrome = function(s) {
    // s = s.replace(/[^\w]/g, '').toLowerCase()
    // 题目要求只考虑字母和数字字符，所以上面的写法也没啥问题
    s = s.replace(/[^0-9a-zA-Z]/g, '').toLowerCase()
    let left = 0;
    let right = s.length - 1;

    while(left < right) {
        if(s[left] != s[right]) {
           return false 
        }
        left++
        right--
    }
    return true
};
```