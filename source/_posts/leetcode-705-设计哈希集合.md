---
title: leetcode.705.设计哈希集合
categories:
  - 算法
tags:
  - leetcode
  - 哈希表
  - 设计
  - 简单
comments: true
abbrlink: 19625
date: 2020-07-19 14:12:39
img:
---
### 题目描述

不使用任何内建的哈希表库设计一个哈希集合

具体地说，你的设计应该包含以下的功能

- add(value)：向哈希集合中插入一个值。
- contains(value) ：返回哈希集合中是否存在这个值。
- emove(value)：将给定值从哈希集合中删除。如果哈希集合中没有这个值，什么也不做。

示例:
```
MyHashSet hashSet = new MyHashSet();
hashSet.add(1);         
hashSet.add(2);         
hashSet.contains(1);    // 返回 true
hashSet.contains(3);    // 返回 false (未找到)
hashSet.add(2);          
hashSet.contains(2);    // 返回 true
hashSet.remove(2);          
hashSet.contains(2);    // 返回  false (已经被删除)
```
注意：
- 所有的值都在 [1, 1000000]的范围内。
- 操作的总数目在[1, 10000]范围内。
- 不要使用内建的哈希集合库。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/design-hashset
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

标签 **设计** **哈希表**

js的对象本来就是哈希结构，而且也没涉及哈希函数的处理，没啥说的。。。

哈希函数的处理和封装，占坑，后补。

```js
/**
 * Initialize your data structure here.
 */
var MyHashSet = function() {
    this.hash = {}
};

/** 
 * @param {number} key
 * @return {void}
 */
MyHashSet.prototype.add = function(key) {
    this.hash[key] = key
};

/** 
 * @param {number} key
 * @return {void}
 */
MyHashSet.prototype.remove = function(key) {
    delete this.hash[key]
};

/**
 * Returns true if this set contains the specified element 
 * @param {number} key
 * @return {boolean}
 */
MyHashSet.prototype.contains = function(key) {
    return (this.hash[key] != null)
};

/** 
 * Your MyHashSet object will be instantiated and called as such:
 * var obj = new MyHashSet()
 * obj.add(key)
 * obj.remove(key)
 * var param_3 = obj.contains(key)
 */
```