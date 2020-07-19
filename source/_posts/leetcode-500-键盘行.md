---
title: leetcode.500.键盘行
categories:
  - 算法
tags:
  - leetcode
  - 哈希表
  - 简单
comments: true
abbrlink: 33235
date: 2020-07-19 14:11:42
img:
---
<!--
 * @File: 
 * @Author: 张宏亮 - zhl@xiaoniren.cn
 * @Date: 2019-08-09 22:04:59
 * @LastEditors: 张宏亮<zhl@xiaoniren.cn>
 * @LastEditTime: 2019-08-09 22:55:16
 * @Description: file content
 * @Versions: 1.0.0
 -->
### 题目描述

给定一个单词列表，只返回可以使用在键盘同一行的字母打印出来的单词。键盘如下图所示。

 ![image](https://raw.githubusercontent.com/zhl1232/javascript-algorithm/master/static/img/500.png)


示例：
```
输入: ["Hello", "Alaska", "Dad", "Peace"]
输出: ["Alaska", "Dad"]
```

注意：
```
你可以重复使用键盘上同一字符。
你可以假设输入的字符串将只包含字母。
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/keyboard-row
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

标签 **哈希表**

标签哈希表，建立好映射关系，每一行字母对应一个value。

然后遍历每个单词的每个字母是否在同一行，value 是否相同。

注意大小写。

```js
/**
 * @param {string[]} words
 * @return {string[]}
 */
var findWords = function(words) {
    let map = new Map([
      ['q',1],['w',1],['e',1],['r',1],['t',1],['y',1],['u',1],['i',1],['o',1],['p',1],
      ['a',2],['s',2],['d',2],['f',2],['g',2],['h',2],['j',2],['k',2],['l',2],
      ['z',3],['x',3],['c',3],['v',3],['b',3],['n',3],['m',3]
    ])
    let res = []

    for(let i = 0; i < words.length; i++) {
        let word =  words[i]
        let temp = map.get(word[0].toLowerCase())
        for(let j = 0; j < word.length; j++) {          
            if(temp == map.get(word[j].toLowerCase())) {
                if (j == word.length - 1) {
                  res.push(word)
                }
            } else {
                break
            }
        }
    }
    return res
};
```