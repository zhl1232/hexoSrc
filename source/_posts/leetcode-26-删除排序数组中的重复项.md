---
title: leetcode.26.删除排序数组中的重复项
categories:
  - 算法
tags:
  - leetcode
  - 双指针
  - 数组
  - 简单
comments: true
abbrlink: 443
date: 2020-07-19 14:06:09
img:
---


<!--
 * @File: 
 * @Author: 张宏亮 - zhl@xiaoniren.cn
 * @Date: 2019-08-18 15:46:12
 * @LastEditors: 张宏亮<zhl@xiaoniren.cn>
 * @LastEditTime: 2019-08-18 17:23:25
 * @Description: file content
 * @Versions: 1.0.0
 -->
### 题目描述

给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。

示例 1:
```
给定数组 nums = [1,1,2], 

函数应该返回新的长度 2, 并且原数组 nums 的前两个元素被修改为 1, 2。 

你不需要考虑数组中超出新长度后面的元素。
```
示例 2:
```
给定 nums = [0,0,1,1,1,2,2,3,3,4],

函数应该返回新的长度 5, 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4。

你不需要考虑数组中超出新长度后面的元素。
```
说明:
```
为什么返回数值是整数，但输出的答案是数组呢?

请注意，输入数组是以“引用”方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。
```
你可以想象内部操作如下:
```
// nums 是以“引用”方式传递的。也就是说，不对实参做任何拷贝
int len = removeDuplicates(nums);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中该长度范围内的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array
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
 * @return {number}
 */
var removeDuplicates = function(nums) {
    const length = nums.length
    if(length == 0) return 0
    let slow = 0
    for(let fast = 1; fast < length; fast++) {
        if(nums[slow] !== nums[fast]) {
            slow++
            nums[slow] = nums[fast]
        }
    }
    return slow + 1
};
```

也可以看下 [27. 移除元素](https://github.com/zhl1232/javascript-algorithm/tree/master/solve-problems/27.md) 的写法，基本一样。