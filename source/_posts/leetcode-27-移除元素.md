---
title: leetcode.27.移除元素
categories:
  - 算法
tags:
  - leetcode
  - 双指针
  - 数组
  - 简单
comments: true
abbrlink: 64273
date: 2020-07-19 14:06:40
img:
---

<!--
 * @File: 
 * @Author: 张宏亮 - zhl@xiaoniren.cn
 * @Date: 2019-08-18 15:46:12
 * @LastEditors: 张宏亮<zhl@xiaoniren.cn>
 * @LastEditTime: 2019-08-18 17:20:33
 * @Description: file content
 * @Versions: 1.0.0
 -->
### 题目描述

给定一个数组 nums 和一个值 val，你需要原地移除所有数值等于 val 的元素，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

示例 1:
```
给定 nums = [3,2,2,3], val = 3,

函数应该返回新的长度 2, 并且 nums 中的前两个元素均为 2。

你不需要考虑数组中超出新长度后面的元素。
```
示例 2:
```
给定 nums = [0,1,2,2,3,0,4,2], val = 2,

函数应该返回新的长度 5, 并且 nums 中的前五个元素为 0, 1, 3, 0, 4。

注意这五个元素可为任意顺序。

你不需要考虑数组中超出新长度后面的元素。
```
说明:
```
为什么返回数值是整数，但输出的答案是数组呢?

请注意，输入数组是以“引用”方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。
```
你可以想象内部操作如下:
```
// nums 是以“引用”方式传递的。也就是说，不对实参作任何拷贝
int len = removeElement(nums, val);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中该长度范围内的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/remove-element
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

标签 **双指针** **数组**
### 解题思路

原地算法，就是不依赖额外的资源或者依赖少数的额外资源，仅依靠输出来覆盖输入的一种算法操作。

在不复制数组的情况下从数组中删除元素的一些提示：
- 尝试双指针法。
- 你是否使用“元素顺序可以更改”这一属性？
- 当要删除的元素很少时会发生什么？
### 解法一：双指针

注意是原地算法，数组长度是会变动的，所以定义一个变量存储数组长度。
```js
/**
 * @param {number[]} nums
 * @param {number} val
 * @return {number}
 */
var removeElement = function(nums, val) {
    let temp = 0
    let len = nums.length
    
    for(let i = 0; i < len; i++) {
        if(nums[temp]=== val) {
            nums.splice(temp, 1)
        } else {
            temp++
        }
    }

    return nums.length
};
```

上面的代码等于 val 的值有几个就要多做几次无意义的循环。

优化下代码。

当我们遇到 nums[i] = val 时，我们可以将当前元素与最后一个元素进行交换，并释放最后一个元素。这实际上使数组的大小减少了 1。

请注意，被交换的最后一个元素可能是您想要移除的值。但是不要担心，在下一次迭代中，我们仍然会检查这个元素。

```js
/**
 * @param {number[]} nums
 * @param {number} val
 * @return {number}
 */
var removeElement = function(nums, val) {
    let i = 0
    let len = nums.length
    
    while(i < len) {
        if(nums[i] == val) {     
            nums[i] = nums[len - 1]   
            len--
        } else {
            i++
        }
    }
    return len
};
```