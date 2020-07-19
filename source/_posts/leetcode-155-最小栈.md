---
title: leetcode.155.最小栈
categories:
  - 算法
tags:
  - leetcode
  - 栈
  - 设计
  - 简单
comments: true
abbrlink: 20751
date: 2020-07-19 14:09:48
img:
---
<!--
 * @File: 
 * @Author: 张宏亮 - zhl@xiaoniren.cn
 * @Date: 2019-08-18 15:46:12
 * @LastEditors: 张宏亮<hongliang@yunshan.net>
 * @LastEditTime: 2019-09-22 15:54:19
 * @Description: file content
 * @Versions: 1.0.0
 -->
### 题目描述

设计一个支持 push，pop，top 操作，并能在常数时间内检索到最小元素的栈。
```
push(x) -- 将元素 x 推入栈中。
pop() -- 删除栈顶的元素。
top() -- 获取栈顶元素。
getMin() -- 检索栈中的最小元素。
```
示例:
```js
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.getMin();   --> 返回 -2.
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/min-stack
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

标签 **栈** **设计**
### 解题思路

push，pop，top 操作都是正常的栈操作。关键是在**常数时间内**检索到最小元素的栈。

要在常数时间内检索，常规做法是以空间换时间，一般使用辅助栈解决。

1. 设一个临时栈
2. 数据入栈时，临时栈为空，必须放入新元素
3. 数据入栈时，临时栈不为空，要判断新元素是否小于等于临时栈顶。符合条件放入临时栈。
4. 数据出栈时，判断元素是否等于临时栈栈顶元素。符合条件临时栈栈顶出栈。

### 解题方法
```js
/**
 * initialize your data structure here.
 */
var MinStack = function() {
    this.stack = []
    this.tempStack = []
};

/** 
 * @param {number} x
 * @return {void}
 */
MinStack.prototype.push = function(x) {
    this.stack.push(x)
    if(this.tempStack.length) {
        this.tempStack[this.tempStack.length - 1] < x ? '' : this.tempStack.push(x)
    } else {
        this.tempStack.push(x)
    }
};

/**
 * @return {void}
 */
MinStack.prototype.pop = function() {
    let pop = this.stack.pop()
    if(pop == this.tempStack[this.tempStack.length - 1]) {
        this.tempStack.pop()
    }
};

/**
 * @return {number}
 */
MinStack.prototype.top = function() {
    return this.stack[this.stack.length - 1]
};

/**
 * @return {number}
 */
MinStack.prototype.getMin = function() {
    return this.tempStack[this.tempStack.length - 1]
};

/** 
 * Your MinStack object will be instantiated and called as such:
 * var obj = new MinStack()
 * obj.push(x)
 * obj.pop()
 * var param_3 = obj.top()
 * var param_4 = obj.getMin()
 */
```