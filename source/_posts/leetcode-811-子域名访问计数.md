---
title: leetcode.811.子域名访问计数
categories:
  - 算法
tags:
  - leetcode
  - 哈希表
  - 简单
comments: true
abbrlink: 20458
date: 2020-07-19 14:13:07
img:
---
<!--
 * @File: 
 * @Author: 张宏亮 - zhl@xiaoniren.cn
 * @Date: 2019-08-09 23:03:47
 * @LastEditors: 张宏亮<zhl@xiaoniren.cn>
 * @LastEditTime: 2019-08-10 00:36:23
 * @Description: file content
 * @Versions: 1.0.0
 -->
### 题目描述

一个网站域名，如"discuss.leetcode.com"，包含了多个子域名。作为顶级域名，常用的有"com"，下一级则有"leetcode.com"，最低的一级为"discuss.leetcode.com"。当我们访问域名"discuss.leetcode.com"时，也同时访问了其父域名"leetcode.com"以及顶级域名 "com"。

给定一个带访问次数和域名的组合，要求分别计算每个域名被访问的次数。其格式为访问次数+空格+地址，例如："9001 discuss.leetcode.com"。

接下来会给出一组访问次数和域名组合的列表cpdomains 。要求解析出所有域名的访问次数，输出格式和输入格式相同，不限定先后顺序。

示例 1:
```
输入: 
["9001 discuss.leetcode.com"]
输出: 
["9001 discuss.leetcode.com", "9001 leetcode.com", "9001 com"]
```
说明: 
```
例子中仅包含一个网站域名："discuss.leetcode.com"。按照前文假设，子域名"leetcode.com"和"com"都会被访问，所以它们都被访问了9001次。
```
示例 2
```
输入: 
["900 google.mail.com", "50 yahoo.com", "1 intel.mail.com", "5 wiki.org"]
输出: 
["901 mail.com","50 yahoo.com","900 google.mail.com","5 wiki.org","5 org","1 intel.mail.com","951 com"]
```
说明: 
```
按照假设，会访问"google.mail.com" 900次，"yahoo.com" 50次，"intel.mail.com" 1次，"wiki.org" 5次。
而对于父域名，会访问"mail.com" 900+1 = 901次，"com" 900 + 50 + 1 = 951次，和 "org" 5 次。
```
注意事项：
```
cpdomains 的长度小于 100。
每个域名的长度小于100。
每个域名地址包含一个或两个"."符号。
输入中任意一个域名的访问次数都小于10000。
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/subdomain-visit-count
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

标签 **哈希表**

### 解题思路

1. 将 "900 google.mail.com" 拆成次数 num 900 和 url 'google.mail.com'
2. 再把 url 按 '.' 拆开，每级域名访问次数都是 num 900
['google.mail.com', 'mail.com', 'com']
3. 遍历数组，把拆分的子域名存到哈希表里 key->域名 value->num，如果哈希表里有就把哈希表里的 num 和现在的 num 相加
4. 拼接返回值
```js
/**
 * @param {string[]} cpdomains
 * @return {string[]}
 */
var subdomainVisits = function(cpdomains) {
    let map = new Map()
    let res = []
    for(let i = 0; i < cpdomains.length; i++) {
        let [num, url] = cpdomains[i].split(' ')
        
        while(url.includes('.')){
            if(map.has(url)){
                map.set(url, (Number(map.get(url)) + Number(num)))
            } else {
                map.set(url, num)
            }            
            url = url.slice(url.indexOf('.') + 1)
        }
        
        if(map.has(url)){
            map.set(url, (Number(map.get(url)) + Number(num)))
        } else {
            map.set(url, num)
        }
    }
    map.forEach((value, key) => {
        res.push(`${value} ${key}`)
    })
    return res
};
```