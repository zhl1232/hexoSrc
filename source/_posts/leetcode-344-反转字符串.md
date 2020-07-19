---
title: leetcode.344.反转字符串
categories:
  - 算法
tags:
  - leetcode
  - 双指针
  - 字符串
  - 简单
comments: true
abbrlink: 53197
date: 2020-07-19 14:10:58
img:
---
### 题目描述

编写一个函数，其作用是将输入的字符串反转过来。输入字符串以字符数组 char[] 的形式给出。

不要给另外的数组分配额外的空间，你必须原地修改输入数组、使用 O(1) 的额外空间解决这一问题。

你可以假设数组中的所有字符都是 ASCII 码表中的可打印字符。

示例 1：
```
输入：["h","e","l","l","o"]
输出：["o","l","l","e","h"]
```
示例 2：
```
输入：["H","a","n","n","a","h"]
输出：["h","a","n","n","a","H"]
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/reverse-string
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

标签 **双指针** **字符串**

### 解题思路

经典的对撞指针题目，设置首尾两个指针，相互交换元素，两个指针向中间移动。

然后直到两个指针相遇。

### 解题方法
```js
/**
 * @param {character[]} s
 * @return {void} Do not return anything, modify s in-place instead.
 */
var reverseString = function(s) {
    let right = 0
    let left = s.length - 1
    while(right < left) {
        [s[right], s[left]] = [s[left], s[right]]
        right++
        left--
    }
};
```

递归写法
```js
/**
 * @param {character[]} s
 * @return {void} Do not return anything, modify s in-place instead.
 */
var reverseString = function(s) {
    let seed = ~~(s.length / 2)
    swap(seed, s)
};
var swap = function(seed, s) {
    if(seed > 0) {
        [s[seed - 1], s[s.length-seed]] = [s[s.length-seed], s[seed - 1]]
        swap(--seed, s)
    }
}
```