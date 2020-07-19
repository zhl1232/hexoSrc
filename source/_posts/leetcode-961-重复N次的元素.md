---
title: leetcode.961-重复N次的元素
categories:
  - 算法
tags:
  - leetcode
  - 哈希表
  - 简单
comments: true
abbrlink: 59872
date: 2020-07-19 14:13:24
img:
---
<!--
 * @File: 
 * @Author: 张宏亮 - zhl@xiaoniren.cn
 * @Date: 2019-08-09 23:03:47
 * @LastEditors: 张宏亮<zhl@xiaoniren.cn>
 * @LastEditTime: 2019-08-09 23:09:07
 * @Description: file content
 * @Versions: 1.0.0
 -->
### 题目描述

在大小为 2N 的数组 A 中有 N+1 个不同的元素，其中有一个元素重复了 N 次。

返回重复了 N 次的那个元素。


示例 1：
```
输入：[1,2,3,3]
输出：3
```
示例 2：
```
输入：[2,1,2,5,3,2]
输出：2
```
示例 3：
```
输入：[5,1,5,2,5,3,5,4]
输出：5
```

提示：
```
4 <= A.length <= 10000
0 <= A[i] < 10000
A.length 为偶数
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/n-repeated-element-in-size-2n-array
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

标签 **哈希表**

### 解题思路

数组大小2N，一共 N+1 个元素，目标元素出现N次，说明其他元素只出现一次。

新建一个空的哈希表，遍历数组，如果当前元素出现2次，该元素为目标元素。

```js
/**
 * @param {number[]} A
 * @return {number}
 */
var repeatedNTimes = function(A) {
    let hash = new Map()
    for(num of A) {
        if(hash.has(num)) {
            return num
        } else {
            hash.set(num, 1)
        }
    }
};
```