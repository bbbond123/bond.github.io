---
layout: post
title: 铁路图表示法
description: 
category: blog
---

##什么是铁路图？

铁路图(railroad_diagrams)又叫语法图,代表一个**上下文无关**语法的一种方式。在编译领域铁路图是一种视觉的表现方式,可以让非专业人员更容易理解,有时纳入平面设计，在定义JSON数据交换格式标准来源提供了帮助,国外的编程人员更喜欢些图来表达编程语言。

## 举例说明

下面的标识方式是按照 巴科斯范式（BNF）表示的，有点儿类似于javascript

	<expression> ::= <term> | <term> "+" <expression>
	<term>       ::= <factor> | <term> "*" <factor>
	<factor>     ::= <constant> | <variable> | "(" <expression> ")"
	<variable>   ::= "x" | "y" | "z" 
	<constant>   ::= <digit> | <digit> <constant>
	<digit>      ::= "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"

expression规则是 可以用term 或者 expression 中间用 + 号来连接其他的term
	
digit 规则是 0或1 或2或3...

***铁路图的标识方式是从左到右***

![syntax-diagram](http://bond.qiniudn.com/Syntax%20diagram_20141014_13057736951651465_000.png)

> 不管路线图是走上边还是下边都是一样的，大家就把它想象成铁路轨道就好理解了，下面我具体说一下json api的铁路图的表现方式。
 

## json api标识方式

###object
比较好理解轨道必须要经过左右括号**`{` `}`** ,每对值都必须要用`,`分割。

![syntax-diagram](http://bond.qiniudn.com/JSON_20141014_13057735204924733_000.gif)

###array
数组跟object差不多只是把`{}`换成`[]`。

![syntax-diagram](http://bond.qiniudn.com/JSON_20141014_13057735206208733_000.gif)

###value
这个就不说了！
![syntax-diagram](http://bond.qiniudn.com/JSON_20141014_13057735207868733_000.gif)

###string
string这个图也比较简单，大家对string的用法都比较熟悉了，这里主要说的是`\`转移那些字符。
![syntax-diagram](http://bond.qiniudn.com/JSON_20141014_13057735210088733_000.gif)

###number
这个比较复杂了，但是要仔细分析也不难。从左边开始
![syntax-diagram](http://bond.qiniudn.com/JSON_20141014_13057735212342733_000.gif)


