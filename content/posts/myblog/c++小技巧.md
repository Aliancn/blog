---

title: "c++小技巧"
summary: 
date: 2023-02-22
weight: 
tags: ["c++","note"]
author: "CHuSeng"
draft: false
isCJKLanguage: true
---

## 字符串类

### 1.句子判断

```c++
(r!="freopen(\""+q[j]+".in\",\"r\",stdin);")||(w!="freopen(\""+q[j]+".out\",\"w\",stdout);")
    //使用加号直接连接字符串和数组
```

- 有句子的判断的时候尽量使用string类型

### 2.产生子串

```
string substr (size_t pos=0,size_t len = npos) const;
```

返回一个子串，从pos开始，跨越len个字符

## 函数类

### 1.四个常用的取整函数

```c++
	floor();//向下取整
    ceil();//向上取整
    round();//四舍五入
	fix();//向零取整
// 注意传入的参数应该为浮点数，在括号内不要直接进行整数间的除法运算
```
