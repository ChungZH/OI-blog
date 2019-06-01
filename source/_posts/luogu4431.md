---
title: 洛谷 P4431 [COCI2017-2018#2] Košnja
date: 2019-06-01 11:15
categories:
- 题解
tags:
- 模拟
- 搜索
- 找规律
---

## 题目链接

https://www.luogu.org/problemnew/show/P4431

<!-- More -->

## 题解

看上去就很简单，实际上更简单。

刚刚看的时候，觉得一个搜索就 OK 了。

然后又转念一想，又发现了一个规律。

答案就是 `(min(n, m)-1)*2`。

也就是 **(行和列中较小的那个数-1)*2**，手推一下就好了。

```cpp
#include <iostream>

using namespace std;

int main()
{
    int k;
    scanf("%d", &k);

    while (k--)
    {
        int n, m;
        scanf("%d%d", &n, &m);

        printf("%d\n", (min(n, m)-1)*2);
    }

    return 0;
}
```

