---
title: leetcode.648.单词替换
categories:
  - 算法
tags:
  - leetcode
  - 哈希表
  - 字典树
  - 中等
comments: true
abbrlink: 25107
date: 2020-07-19 14:12:26
img:
---
<!--
 * @File: 
 * @Author: 张宏亮 - zhl@xiaoniren.cn
 * @Date: 2019-08-09 23:03:47
 * @LastEditors: 张宏亮<zhl@xiaoniren.cn>
 * @LastEditTime: 2019-08-12 17:18:57
 * @Description: file content
 * @Versions: 1.0.0
 -->
### 题目描述

在英语中，我们有一个叫做 词根(root)的概念，它可以跟着其他一些词组成另一个较长的单词——我们称这个词为 继承词(successor)。例如，词根an，跟随着单词 other(其他)，可以形成新的单词 another(另一个)。

现在，给定一个由许多词根组成的词典和一个句子。你需要将句子中的所有继承词用词根替换掉。如果继承词有许多可以形成它的词根，则用最短的词根替换它。

你需要输出替换之后的句子。

示例 1:
```
输入: dict(词典) = ["cat", "bat", "rat"]
sentence(句子) = "the cattle was rattled by the battery"
输出: "the cat was rat by the bat"
```
注:
```
输入只包含小写字母。
1 <= 字典单词数 <=1000
1 <=  句中词语数 <= 1000
1 <= 词根长度 <= 100
1 <= 句中词语长度 <= 1000
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/replace-words
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

标签 **字典树** **哈希表** 

### 解法一：没啥意义的直接解法

时间复杂度O(n^2)

虽然没啥意义，不过结果看起来还不错。
```
执行结果：通过 显示详情
执行用时 : 168 ms, 在所有 JavaScript 提交中击败了 91.67% 的用户
内存消耗 : 40.7 MB, 在所有 JavaScript 提交中击败了 100.00% 的用户
```


```js
/**
 * @param {string[]} dict
 * @param {string} sentence
 * @return {string}
 */
var replaceWords = function(dict, sentence) {
    let words = sentence.split(' ')
    for(let i = 0; i < words.length; i++) {
        for(let j = 0; j < dict.length; j++) {
            if(words[i].startsWith(dict[j])){
                words[i] = dict[j]
                continue
            }
        }
    }
    return words.join(' ')
};
```

### 解法二：字典树

开始用字母对应下标写的 children。

后来看到标签为字典树和哈希表。。

又改成哈希了。2333

```js
/**
 * @param {string[]} dict
 * @param {string} sentence
 * @return {string}
 */

/**
  * Trie
  */
class Trie {
  constructor() {
    this.root = new TrieNode(null)
  }
  insertData(stringData) {
    this.insert(stringData, this.root)
  }
  insert(stringData, node) {
    if (stringData == '') {
      node.done = true
      return
    }
    // 题目里都是单词，只有26个字母。用字母的 ASCII 码减 a 的 ASCII 码正好对应0-25
    // const index = stringData[0].charCodeAt(0) - 'a'.charCodeAt(0)
    let haveData = node.children.get(stringData[0])

    if (haveData) {
      this.insert(stringData.substring(1), haveData)
    } else {
      let newNode = new TrieNode(stringData[0])
      // node.children[index] = newNode
      node.children.set(stringData[0], newNode)
      this.insert(stringData.substring(1), newNode)
    }
  }
  search(stringData) {
    let node = this.root
    let res = ''
    for (let i = 0; i < stringData.length; i++) {
      // cattle
      const element = stringData[i]
      // const index = element.charCodeAt(0) - 'a'.charCodeAt(0)
      const target = node.children.get(element)

      if (node.done) {
        break
      } else if (target) {
        res += target.key
        node = target
      } else {
        res = ''
        break
      }
    }
    return res
  }
}
/**
  * 节点
  * @param {*} key
  */
class TrieNode {
  constructor(key) {
    this.key = key // 节点字符
    this.children = new Map() // 子节点集合
  }
}


var replaceWords = function(dict, sentence) {
    const trie = new Trie();
        for(let i = 0; i < dict.length; i++) {
          trie.insertData(dict[i]);
        }
        
    return sentence.split(' ').map(wrod => trie.search(wrod) || wrod).join(' ');
};
```

字典树资料