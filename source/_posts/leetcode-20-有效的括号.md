---
title: leetcode.20.有效的括号
categories:
  - 算法
tags:
  - leetcode
  - 栈
  - 字符串
  - 简单
comments: true
abbrlink: 34299
date: 2020-07-19 13:54:45
img:
---

<!--
 * @File: 
 * @Author: 张宏亮 - zhl@xiaoniren.cn
 * @Date: 2019-08-18 15:46:12
 * @LastEditors: 张宏亮<hongliang@yunshan.net>
 * @LastEditTime: 2019-09-22 16:03:00
 * @Description: file content
 * @Versions: 1.0.0
 -->
### 题目描述

给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：
```
左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。
```
示例 1:
```
输入: "()"
输出: true
```
示例 2:
```
输入: "()[]{}"
输出: true
```
示例 3:
```
输入: "(]"
输出: false
```
示例 4:
```
输入: "([)]"
输出: false
```
示例 5:
```
输入: "{[]}"
输出: true
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/valid-parentheses
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

标签 **栈** **字符串**
### 解题思路

1. 如果括号数量为奇数，肯定是错误的
2. 如果括号数量为偶数，使用栈，遍历输入字符串
3. 如果当前字符为左半边括号时，肯定是正确的，将其压入栈中
4. 如果遇到右半边括号时，右半边括号与栈顶的左半括号不匹配，返回错误
5. 如果匹配，把匹配的左半括号弹出栈

![image](https://raw.githubusercontent.com/zhl1232/javascript-algorithm/master/static/img/stack.png)

图片来自： https://github.com/MisterBooo/LeetCodeAnimation

### 解法一

```js
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function(s) {
    let sArr = s.split('')
    let temp = []
    let res = true
    if(sArr.length % 2 == 1) return false
    try {
      sArr.forEach(item => {
        if (item.match(/\(|\{|\[/)) {
          temp.push(item)
        } else {
          if (item == ')' && temp.pop() == '(') {
            return
          } else if (item == '}' && temp.pop() == '{') {
            return
          } else if (item == ']' && temp.pop() == '[') {
            return
          } else {
            res = false
            throw new Error()
            // 如果为false，用try catch跳出循环
          }
        }
      })
    } catch (error) {}

    if (temp.length == 0 && res) {
      return true
    } else {
      return false
    }
};
```
> js没有现成的栈，用数组模拟
> 可以用 try catch 跳出 forEach 循环

这道题写法可能各不相同，但解题逻辑只有这一种。

比如写法可以把每对括号存hash表里，然后匹配的时候用 key: value 匹配对应的括号

或者用for循环，跳出和return容易很多。
```js
let hash = { ')': '(', '}': '{', ']': '[' }
```

### 扩展

事实上，这类问题还可以进一步扩展，我们可以去解析类似HTML等标记语法， 比如检查XML标签是否闭合如何检查， 更进一步如果要你实现一个简单的XML的解析器，应该怎么实现？