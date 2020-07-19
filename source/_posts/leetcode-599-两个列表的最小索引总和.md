---
title: leetcode.599.两个列表的最小索引总和
categories:
  - 算法
tags:
  - leetcode
  - 哈希表
  - 简单
comments: true
abbrlink: 54315
date: 2020-07-19 14:12:06
img:
---
### 题目描述

假设Andy和Doris想在晚餐时选择一家餐厅，并且他们都有一个表示最喜爱餐厅的列表，每个餐厅的名字用字符串表示。

你需要帮助他们用最少的索引和找出他们共同喜爱的餐厅。 如果答案不止一个，则输出所有答案并且不考虑顺序。 你可以假设总是存在一个答案。

示例 1:
```
输入:
["Shogun", "Tapioca Express", "Burger King", "KFC"]
["Piatti", "The Grill at Torrey Pines", "Hungry Hunter Steakhouse", "Shogun"]
输出: ["Shogun"]
解释: 他们唯一共同喜爱的餐厅是“Shogun”。
```
示例 2:
```
输入:
["Shogun", "Tapioca Express", "Burger King", "KFC"]
["KFC", "Shogun", "Burger King"]
输出: ["Shogun"]
解释: 他们共同喜爱且具有最小索引和的餐厅是“Shogun”，它有最小的索引和1(0+1)。
```
提示:

- 两个列表的长度范围都在 [1, 1000]内。
- 两个列表中的字符串的长度将在[1，30]的范围内。
- 下标从0开始，到列表的长度减1。
- 两个列表都没有重复的元素。

标签 **哈希表**

https://leetcode-cn.com/problems/minimum-index-sum-of-two-lists/


### 解题思路

根据提示两个列表都没有重复的元素。
所以两个列表同一餐厅最多出现两次。
所以只要比较出现两次的餐厅的下标和就可以。
如果下标和小就当作返回值，如果下标和相等，就push到返回值里。


```js
/**
 * @param {string[]} list1
 * @param {string[]} list2
 * @return {string[]}
 */
var findRestaurant = function(list1, list2) {
    let res = []
    let indexSum
    let hash = new Map()
    for(let i = 0; i < list1.length; i++) {
        hash.set(list1[i], i)
    }
    for(let i = 0; i < list2.length; i++) {
        if(hash.has(list2[i])) {
            if(typeof indexSum === 'undefined') {
                indexSum = hash.get(list2[i]) + i
                res = [list2[i]]
            } else {
                if(indexSum > hash.get(list2[i]) + i) {
                    indexSum = hash.get(list2[i]) + i
                    res = [list2[i]]
                } else if(indexSum == hash.get(list2[i]) + i){
                    res.push(list2[i])
                }
            }
            
        }
    }
    return res
};
```