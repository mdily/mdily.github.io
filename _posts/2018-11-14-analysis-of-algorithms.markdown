---
layout: post
title:  "浅谈算法分析-算法复杂度"
date:   2018-11-14 23:30:00
categories: Algorithms
tags: algorithms python
---

* content
{:toc}

《数据结构与算法 Python语言描述》算法分析笔记

## 算法复杂度

常见的复杂度函数：O(1), O(log n), O(n), O(n log n), O(n^2), O(n^3), O(2^n)

![image-O(g(n))](http://i.imgur.com/LpD7WBD.png)

从上图可以看到，算法复杂度函数**由简单到复杂**排序：O(1) < O(log n) < O(n) < O(n log n) < O(n^2) < O(n^3) < O(2^n)；复杂度越高，其实施的代价随着规模的增大而增长的速度就越快。

### 基本程序复杂度分析

* 基本操作：O(1)，例如基本的复赋值语句。

* 加法规则（顺序结构）：T(n) = T1(n) + T2(n) = O(T1(n)) + O(T2(n)) = O(max(T1(n), T2(n)))，即取的是复杂度较高的一个程序。

* 乘法规则（循环结构）：T(n) = T1(n) * T2(n) = O(T1(n)) * O(T2(n)) = O(T1(n) * T2(n))，循环体将执行T1(n)次，每次执行需要T2(n)时间。

* 取最大规则（分支结构）：T(n) = O(max(T1(n), T2(n)))

看一个简单的实例：

```python
for i in range(n):
    for j in range(n):
        x = 0
        for k in range(n):
            x = x + m1[i][k] * m2[k][j]
        m[i][j] = x
```

第一个循环：O(n)；第二个循环：O(n)；第三个循环：O(n)

T(n) = O(n) * O(n) * O(n) = O(n^3)

以上就是简单的程序复杂度分析......

这是我的第一篇blog，共勉。


