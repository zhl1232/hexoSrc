---
title: leetcode.771.宝石与石头
categories:
  - 算法
tags:
  - leetcode
  - 哈希表
  - 简单
comments: true
abbrlink: 64216
date: 2020-07-19 14:13:00
img:
---
<!--
 * @File: 
 * @Author: 张宏亮 - zhl@xiaoniren.cn
 * @Date: 2019-08-09 22:04:59
 * @LastEditors: 张宏亮<zhl@xiaoniren.cn>
 * @LastEditTime: 2019-08-09 22:06:27
 * @Description: file content
 * @Versions: 1.0.0
 -->
### 题目描述

 给定字符串J 代表石头中宝石的类型，和字符串 S代表你拥有的石头。 S 中每个字符代表了一种你拥有的石头的类型，你想知道你拥有的石头中有多少是宝石。

J 中的字母不重复，J 和 S中的所有字符都是字母。字母区分大小写，因此"a"和"A"是不同类型的石头。

示例 1:
```
输入: J = "aA", S = "aAAbbbb"
输出: 3
```
示例 2:
```
输入: J = "z", S = "ZZ"
输出: 0
```
注意:

S 和 J 最多含有50个字母。
 J 中的字符不重复。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/jewels-and-stones
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

标签 **哈希表**

标准的哈希集合题目，没啥说的。。
```js
/**
 * @param {string} J
 * @param {string} S
 * @return {number}
 */
var numJewelsInStones = function(J, S) {
    let setJ = new Set(J)
    let res = 0
    for(i = 0; i < S.length; i++) {
        if(setJ.has(S[i])) {
            res += 1
        }
    }
    return res
};
```