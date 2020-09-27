---
title: Markdown语法
top: false
cover: false
categories: 软件工具
tags:
  - Markdown
keywords: Markdown
abbrlink: 3c50d03d
date: 2020-09-27 14:54:53
---

# Markdown语法

Markdown自查手册

## 标题

```
# 这是一级标题
##### 这是五级标题
###### 这是六级标题
```
# 这是一级标题
##### 这是五级标题
###### 这是六级标题


## 字体

```
*斜体*或_斜体_
**粗体**
***加粗斜体***
~~删除线~~
```
*斜体*或_斜体_
**粗体**
***加粗斜体***
~~删除线~~

## 引用

```markdown
>这是引用的内容
>>这是引用的内容
>>>>>>>>>>这是引用的内容
```
>这是引用的内容
>>这是引用的内容
>>>>>>>>>>这是引用的内容

## 分割线
```markdown
---
----
***
*****
```
---
----
***
*****

## 图片
```markdown
![blockchain](https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=702257389,1274025419&fm=27&gp=0.jpg)

![图片alt](图片地址 ''图片title'')

图片alt就是显示在图片下面的文字，相当于对图片内容的解释。
图片title是图片的标题，当鼠标移到图片上时显示的内容。title可加可不加
```
![blockchain](https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=702257389,1274025419&fm=27&gp=0.jpg)

## 超链接

### 行内式

```markdown
[百度](http://baidu.com)
```
[百度](http://baidu.com)

### 参考式

```markdown
我经常去的几个网站[Google][1]、[Leanote][2]。

[1]:http://www.google.com 
[2]:http://www.leanote.com
```
我经常去的几个网站[Google][1]、[Leanote][2]。

[1]:http://www.google.com 
[2]:http://www.leanote.com

### 注脚

```markdown
使用 Markdown[^1]可以效率的书写文档。

[^1]:Markdown是一种纯文本标记语言
```
使用 Markdown[^1]可以效率的书写文档。

[^1]:Markdown是一种纯文本标记语言


## 列表

### 无序列表
```
- 列表内容
+ 列表内容
* 列表内容
```
- 列表内容
+ 列表内容
* 列表内容

### 有序列表
```
1. 列表内容
2. 列表内容
3. 列表内容
```
1. 列表内容
2. 列表内容
3. 列表内容

## 表格
语法
```markdown
表头|表头|表头
---|:--:|---:
内容|内容|内容
内容|内容|内容

第二行分割表头和内容。
- 有一个就行，为了对齐，多加了几个
文字默认居左
-两边加：表示文字居中
-右边加：表示文字居右
注：原生的语法两边都要用 | 包起来。此处省略
```
```
姓名|序号|排行
--|:--:|--:
刘备|1|大哥
关羽|2|二哥
张飞|3|三弟
```
姓名|序号|排行
--|:--:|--:
刘备|1|大哥
关羽|2|二哥
张飞|3|三弟

## 代码

### 单行代码
```markdown
`create database hero;`
```
`create database hero;`

### 代码块
```
    ```javascript
    $(document).ready(function () {
        alert('success');
    });
    ```
```

```javascript
$(document).ready(function () {
    alert('success');
});
```