---
title: leetcode.36.有效的数独
categories:
  - 算法
tags:
  - leetcode
  - 哈希表
  - 中等
comments: true
abbrlink: 16645
date: 2020-07-19 14:06:50
img:
---


### 题目描述

判断一个 9x9 的数独是否有效。只需要根据以下规则，验证已经填入的数字是否有效即可。

数字 1-9 在每一行只能出现一次。
数字 1-9 在每一列只能出现一次。
数字 1-9 在每一个以粗实线分隔的 3x3 宫内只能出现一次。

![image](https://raw.githubusercontent.com/zhl1232/javascript-algorithm/master/static/img/36.png)

上图是一个部分填充的有效的数独。

数独部分空格内已填入了数字，空白格用 '.' 表示。

示例 1:
```
输入:
[
  ["5","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
输出: true
```
示例 2:
```
输入:
[
  ["8","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
输出: false
```
解释: 除了第一行的第一个数字从 5 改为 8 以外，空格内其他数字均与 示例1 相同。
     但由于位于左上角的 3x3 宫内有两个 8 存在, 因此这个数独是无效的。

说明:
一个有效的数独（部分已被填充）不一定是可解的。
只需要根据以上规则，验证已经填入的数字是否有效即可。
给定数独序列只包含数字 1-9 和字符 '.' 。
给定数独永远是 9x9 形式的。

标签 **哈希表**

https://leetcode-cn.com/problems/valid-sudoku/

### 方法一：一次迭代

思路：
- 每一行、每一列、每一个小正方形都不能重复出现相同数字
- 用hash记录它的行，列和小正方形的值，有重复就false
- 可以用 (~~(i/3))*3 + ~~(j/3) 来确定小正方块的位置

![image](https://raw.githubusercontent.com/zhl1232/javascript-algorithm/master/static/img/36-1.png)

时间复杂度：O(1)，因为我们只对 81 个单元格进行了一次迭代。

```js
/**
 * @param {character[][]} board
 * @return {boolean}
 */
var isValidSudoku = function(board) {
    let rows = new Map()
    let cols = new Map()
    let boxs = new Map() 
    
    for(let i = 0; i < board.length; i++) {
        rows.set(`rows${i}`, new Map())
        cols.set(`cols${i}`, new Map())
        boxs.set(`boxs${i}`, new Map())
    }
    
    for(let i = 0; i < board.length; i++) {
        
        for(let j = 0; j < board[i].length; j++) {
            if(board[i][j] == '.') continue
            let boxIndex = (~~(i/3))*3 + ~~(j/3)
            
            let row = rows.get(`rows${i}`)
            let col = cols.get(`cols${j}`)
            let box = boxs.get(`boxs${boxIndex}`)
            
            if(row.has(board[i][j]) || col.has(board[i][j]) || box.has(board[i][j])) {
                return false
            } else {
                row.set(board[i][j], 1)
                col.set(board[i][j], 1)
                box.set(board[i][j], 1)
            }
        }
    }
    return true
};
```

### 方法二：三次迭代

一个简单的解决方案是遍历该 9 x 9 数独 三 次，以确保：

- 行中没有重复的数字。
- 列中没有重复的数字。
- 3 x 3 子数独内没有重复的数字。

这个没啥说的。

```js
/**
 * @param {character[][]} board
 * @return {boolean}
 */
var isValidSudoku = function(board) {
  for (let i = 0; i < 9; i++) { // 检查行重复项
    let row = {};
    for (let j = 0; j < 9; j++) {
      if (board[i][j] !== '.') {
        if (row[board[i][j]]) return false;
        row[board[i][j]] = 1;
      }
    }
  }
  for (let i = 0; i < 9; i++) { // 检查列重复项
    let col = {};
    for (let j = 0; j < 9; j++) {
      if (board[j][i] !== '.') {
        if (col[board[j][i]]) return false;
        col[board[j][i]] = 1;
      }
    }
  }
  for (let i = 0; i < 9; i += 3) { // 检查3*3宫格重复项
    for (let j = 0; j < 9; j += 3) {
      let miniTable = {};
      for (let m = i; m < i + 3; m++) {
        for (let n = j; n < j + 3; n++) {
          if (board[m][n] !== '.') {
            if (miniTable[board[m][n]]) return false;
            miniTable[board[m][n]] = 1;
          }
        }
      }
    }
  }
  return true;
};
```