---

title: "num和string的转换"
summary: "常用的转换方法"
date: 2023-02-20
weight: 
tags: ["string"]
author: "CHuSeng"
draft: false
isCJKLanguage: true
---

## 一、num转string

头文件

```c++
#include<string>
#include<typeinfo>
```

### 1.1 int转string

```c++
int num = 123;
string num2str = to_string(num);
cout << typeid(to_string(num)) == typeid(string) << endl; 
        // true
```

### 1.2 float/double转string

头文件

```
#include<sstream>
```

```c++
double num = 123.56;  // float同理
stringstream sstream;
sstream << num;
string num2str = sstream.str();  // num2str = "123.56"
cout << typeid(sstream.str()) == typeid(string) << endl;  // true
sstream.clear();  // 若在用一个流中处理大量数据，则需手动清除缓存，小数据或不同流可忽略
```



## 二、string转num

### 2.1

















