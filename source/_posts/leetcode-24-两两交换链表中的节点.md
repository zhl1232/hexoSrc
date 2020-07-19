---
title: leetcode.24.两两交换链表中的节点
categories:
  - 算法
tags:
  - leetcode
  - 链表
  - 中等
comments: true
abbrlink: 12544
date: 2020-07-19 14:05:55
img:
---

### 题目描述

给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

示例:
```
给定 1->2->3->4, 你应该返回 2->1->4->3.
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/swap-nodes-in-pairs
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

标签 **链表**
### 解题思路

这道题递归和非递归其实差不多。

先拆分子问题，
1. 要把 head 和 head.next 交换，也就是相邻的节点交换
2. 交换之后的 head.next.next 要指向下一对交换节点的 head 节点
3. 然后递归直到 head 或者 head.next 为 null，也就是不够两个节点进行交换
4. 要注意递归时传入下一对交换节点的 head 节点要传哪个，
```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var swapPairs = function(head) {
    if(!head || !head.next) {
        return head
    }
    let tempHead = head.next   
    head.next = swapPairs(head.next.next)  
    tempHead.next = head
    return tempHead
};
```

非递归写法

```js
var swapPairs = function(head) {
    let tempHead = new ListNode(0)
    tempHead.next = head
    let prev = tempHead
    while(prev.next && prev.next.next) {
        let a = prev.next
        let b = a.next
        prev.next = a.next
        a.next = b.next
        prev = b.next = a
    }
    return tempHead.next
};
```