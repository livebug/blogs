---
title: 正则表达式的先行断言(lookahead)和后行断言(lookbehind)
date: 2023-09-17 23:48:19
tags:
- regex
---

正则表达式的先行断言和后行断言一共有 4 种形式：
 
+ `(?=pattern)`  零宽正向先行断言`(zero-width positive lookahead assertion)`
+ `(?!pattern)`  零宽负向先行断言`(zero-width negative lookahead assertion)`
+ `(?<=pattern)` 零宽正向后行断言`(zero-width positive lookbehind assertion)`
+ `(?<!pattern)` 零宽负向后行断言`(zero-width negative lookbehind assertion)`