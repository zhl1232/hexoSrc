---
title: leetcode.80.删除排序数组中的重复项II
categories:
  - 算法
tags:
  - leetcode
  - 数组
  - 双指针
  - 中等
comments: true
abbrlink: 48396
date: 2020-07-19 14:09:08
img:
---
<!--
 * @File: 
 * @Author: 张宏亮 - zhl@xiaoniren.cn
 * @Date: 2019-08-18 15:46:12
 * @LastEditors: 张宏亮<zhl@xiaoniren.cn>
 * @LastEditTime: 2019-08-24 11:45:57
 * @Description: file content
 * @Versions: 1.0.0
 -->
### 题目描述

给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素最多出现两次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。

示例 1:
```
给定 nums = [1,1,1,2,2,3],

函数应返回新长度 length = 5, 并且原数组的前五个元素被修改为 1, 1, 2, 2, 3 。

你不需要考虑数组中超出新长度后面的元素。
```
示例 2:
```
给定 nums = [0,0,1,1,1,1,2,3,3],

函数应返回新长度 length = 7, 并且原数组的前五个元素被修改为 0, 0, 1, 1, 2, 3, 3 。

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
链接：https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array-ii
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

标签 **双指针** **数组**
### 解题思路

原地算法，就是不依赖额外的资源或者依赖少数的额外资源，仅依靠输出来覆盖输入的一种算法操作。

在不复制数组的情况下从数组中删除元素的一些提示：
- 尝试双指针法。
- 你是否使用“元素顺序可以更改”这一属性？
- 当要删除的元素很少时会发生什么？

### 解法一：数组api

定义 nums[0...i] 满足每个元素最多出现两次，遍历整个数列不断的维护这个定义。

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {
  let i = 0
  while (i < nums.length) {
    if (nums[i] === nums[i - 2]) {
      nums.splice(i, 1)
    } else {
      i++
    }
  }
};
```


### 解法二：双指针

维护两个指针，
1. 慢指针 p1 初始为 0 ，快指针 p2 初始为 1
2. 如果快指针的后一位 (p2 + 1) 和前一位( p1 )都相同，那说明该元素出现三次。
3. 出现三次把快指针 p2 下元素原地删除，快指针不变，继续比较
4. 如果快指针和慢指针不相同，说明之前的数字都是最多出现两次的，把慢指针 p1 改为当前不同的数字下标，也就是快指针 p2


```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {
  let p1 = 0
  let p2 = 1
  
    while (p2 < nums.length) {
    if(nums[p2] == nums[p1] && nums[p2 + 1] == nums[p1]) {
        nums.splice(p2, 1)
      } else if(nums[p2] !== nums[p1]){
        p1 = p2
        p2++
      } else {
        p2++
      }
  }
};
```