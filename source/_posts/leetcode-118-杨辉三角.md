---
title: leetcode.118.杨辉三角
categories:
  - 算法
tags:
  - leetcode
  - 数组
  - 简单
comments: true
abbrlink: 34917
date: 2020-07-19 14:09:30
img:
---
### 题目描述

给定一个非负整数 numRows，生成杨辉三角的前 numRows 行。

![image](https://raw.githubusercontent.com/zhl1232/javascript-algorithm/master/static/img/118.gif)

在杨辉三角中，每个数是它左上方和右上方的数的和。

示例:
```
输入: 5
输出:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/pascals-triangle
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

标签 **数组**

### 解题思路

是在递归的卡片里看到的这题，所以先用递归解决了

1. 终止条件，结果的 length 大于等于 numRows
2. 返回值，每个二维数据的子数组
3. 拆分的子问题，每个子数组的长度为当前行数，每个子数组里的值为它左上方和右上方的数的和，上方就是行数 - 1，左边就是当前子数组的值下标-1，右边就是下标+1，判断如果左上或者右上不存在，则为0

### 解题方法
```js
var generate = function(numRows) {
  let res = []
  
  return sub(0, numRows, res)
}

var sub = function(row, numRows, arr) {
  let temp = []
  if (row < numRows) {
    for (let i = 0; i <= row; i++) {
      if (row === 0) {
        temp.push(1)
      } else {
        let left = i-1 >= 0 ? arr[row-1][i-1] : 0
        let right = i < arr[row-1].length ? arr[row-1][i] : 0
        temp.push(left+right)
      }
    }
    arr.push(temp)
    sub(++row, numRows, arr)
    return arr
  }
}
```