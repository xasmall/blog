---
title: java方法CompareTo引发的错误
date: 2022-06-08 18:44:14
categories:
- 开发
tags:
- java
- bug修复
---

### java CompareTo方法

记录一下今天刷力扣的时候使用Arrays.sort时出现的错误

```
Comparison method violates its general contract!
```

这个问题的意思就是说比较顺序需要满足可逆比较

我们看一下java实现的CompareTo方法

```
public int compareTo(String anotherString) {
    int len1 = value.length;
    int len2 = anotherString.value.length;
    int lim = Math.min(len1, len2);
    char v1[] = value;
    char v2[] = anotherString.value;

    int k = 0;
    while (k < lim) {
        char c1 = v1[k];
        char c2 = v2[k];
        if (c1 != c2) {
            return c1 - c2;
        }
        k++;
    }
    return len1 - len2;
}
```

在这个compareTo方法中，从前到后比较第一个不同的字符，走到其中一个没有字符后，比较两者的长度
那么这个里面的一个东西时``` len1 - len2 ``` 当两个字符串相等的时候，需要返回0，特此注意一下