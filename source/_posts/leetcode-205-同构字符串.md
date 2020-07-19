---
title: leetcode.205.同构字符串
categories:
  - 算法
tags:
  - leetcode
  - 哈希表
  - 简单
comments: true
abbrlink: 7985
date: 2020-07-19 14:10:22
img:
---
### 题目描述

给定两个字符串 s 和 t，判断它们是否是同构的。

如果 s 中的字符可以被替换得到 t ，那么这两个字符串是同构的。

所有出现的字符都必须用另一个字符替换，同时保留字符的顺序。两个字符不能映射到同一个字符上，但字符可以映射自己本身。

示例 1:
```
输入: s = "egg", t = "add"
输出: true
```
示例 2:
```
输入: s = "foo", t = "bar"
输出: false
```
示例 3:
```
输入: s = "paper", t = "title"
输出: true
```
说明:
你可以假设 s 和 t 具有相同的长度。

标签 **哈希表**

https://leetcode-cn.com/problems/isomorphic-strings/


### 解法一：
indexOf会返回指定字符串值在字符串中首次出现的位置

s 和 t 具有相同的长度

所以遍历一次，比较每个位置是否同构

如果遍历当前字符串是未出现过的，那两边indexOf肯定是当前i

如果遍历当前字符串是以前出现过的，那两边indexOf会拿到首次相同字串符的下标，值也应该一样

时间复杂度：两个字符串的indexOf加上一次遍历O(n^2)

```js
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isIsomorphic = function(s, t) {

    for(let i = 0; i < s.length; i++) {
        if(s.indexOf(s[i]) != t.indexOf(t[i])) return false
    }
    return true
};
```

### 解法二：
哈希映射

两个字符串相互映射。

遇到重复的子字符串，判断两个哈希表里对应的映射是否正确。


```js
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isIsomorphic = function(s, t) {
    let hash1 = new Map()
    let hash2 = new Map()
    for(let i = 0; i < s.length; i++) {
        let S = s[i]
        let T = t[i]
        if(hash1.has(S)) {
            if(hash1.get(S) !== T) return false
        } else if(hash2.has(T)) {
            if(hash2.get(T) !== S) return false
        } else {
            hash1.set(S, T)
            hash2.set(T, S)
        }
    }
    return true
};
```
