---
title: leetcode.832.翻转图像
categories:
  - 算法
tags:
  - leetcode
  - 数组
  - 简单
comments: true
abbrlink: 35635
date: 2020-07-19 14:13:15
img:
---
### 题目描述

给定一个二进制矩阵 A，我们想先水平翻转图像，然后反转图像并返回结果。

水平翻转图片就是将图片的每一行都进行翻转，即逆序。例如，水平翻转 [1, 1, 0] 的结果是 [0, 1, 1]。

反转图片的意思是图片中的 0 全部被 1 替换， 1 全部被 0 替换。例如，反转 [0, 1, 1] 的结果是 [1, 0, 0]。

示例 1:
```
输入: [[1,1,0],[1,0,1],[0,0,0]]
输出: [[1,0,0],[0,1,0],[1,1,1]]
解释: 首先翻转每一行: [[0,1,1],[1,0,1],[0,0,0]]；
     然后反转图片: [[1,0,0],[0,1,0],[1,1,1]]
```
示例 2:
```
输入: [[1,1,0,0],[1,0,0,1],[0,1,1,1],[1,0,1,0]]
输出: [[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]
解释: 首先翻转每一行: [[0,0,1,1],[1,0,0,1],[1,1,1,0],[0,1,0,1]]；
     然后反转图片: [[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]
```
说明:
```
1 <= A.length = A[0].length <= 20
0 <= A[i][j] <= 1
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/flipping-an-image
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

标签 **数组**


### 方法一：数组API

没啥说的。。
```js
/**
 * @param {number[][]} A
 * @return {number[][]}
 */
var flipAndInvertImage = function(A) {
    return A.map(item => item.reverse().map(item1 => item1 === 0 ? 1 : 0))
};
```

### 方法二：对撞双指针

按位异或：

参与运算的两个值，如果两个相应位相同，则结果为0，否则为1。即：0^0=0， 1^0=1， 0^1=1， 1^1=0

所以 (0 和 1) ^ 1 就会相当于反转，1 会变成 0， 0 会变成 1。当然用三元运算符也行。

利用双指针，把右边的值反转放到左边，把左边的值反转放到右边。

就相当于翻转并反转了。


```js
/**
 * @param {number[][]} A
 * @return {number[][]}
 */
var flipAndInvertImage = function(A) {
  for (let i = 0; i < A.length; i++) {
    let left = 0
    let right = A.length - 1
    while (left <= right) {
      let temp = A[i][left]
      A[i][left] = A[i][right] ^ 1
      A[i][right] = temp ^ 1
      // A[i][left] = A[i][right] === 1 ? 0 : 1
      // A[i][right] = temp === 1 ? 0 : 1
      left++
      right--
    }
  }
  return A
}
```

### 方法三：规律

比如 [1,1,0]，水平翻转后是[0,1,1]，再反转就会变为 [1,0,0]。

比如 [1,1,0,0]，水平翻转后是[0,0,1,1]，再反转就会变为 [1,1,0,0].

会发现，两边的值只要不相等，水平翻转后再反转就会和之前一样。奇数长度中间值没法比较的一会再说。

再看两边值相等的，最后结果就是原来的值取反。

最后再看奇数长度中间值，发现都是取反。

所以只要判断对撞指针两边的值是否相等，如果相等，值不变。如果不相等值取反。如果是奇数，那把中间值也取反。


```js
/**
 * @param {number[][]} A
 * @return {number[][]}
 */
var flipAndInvertImage = function(A) {
  let n = A.length
  for (let i = 0; i < n; i++) {
    let left = 0
    let right = n - 1

    while (left < right) {
      if (A[i][left] === A[i][right]) {
        A[i][left] = A[i][left] ^ 1
        A[i][right] = A[i][right] ^ 1
      }
      left++
      right--
    }
    if (n % 2) {
      A[i][~~(n / 2)] = A[i][~~(n / 2)] ^ 1
    }
  }
  return A
}
```