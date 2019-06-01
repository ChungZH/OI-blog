---
title: 洛谷 P4305 [JLOI2011]不重复数字
date: 2019-06-01 10:43:26
categories:
- 题解
tags:
- 桶排序思想
---

## 题目链接

https://www.luogu.org/problemnew/show/P4305

<!-- More -->

## 题解

一看题目里面 **去重** 我就想到了桶排序，不过这道题不是完全的桶排序，只是用到 **桶** 但是不用 **排序**。

虽然数字比较大，但是不用遍历桶数组，速度也不是问题。

其实很简单，开一个 bool 类型的桶数组（不需要 int），然后如果有出现的数字就标 true，否则 false。

最后输出，如果桶里面这个数是 true，就直接输出然后标 false。如果是 false 就不输出。这样就可以去重了。

（后来发现题解里也有一个思路一样的，不过他的代码要比我的更优秀点。）

```cpp
#include <cstdio>
#include <cstring>

using namespace std;

bool bucket[10000005];
int a[50005];

int main()
{

    int T;
    scanf("%d", &T);

    while (T --> 0)
    {
        int n;
        scanf("%d", &n);
		
        // 下面一行其实是可以不用的，看到题解才恍然大悟：bucket 数组在输出的时候已经被全部标成 0 了！
        memset(bucket, 0, sizeof(bucket));
        // memset(a, 0, sizeof(a));
        // 无必要

        for (int i = 0; i < n; i++)
        {
            scanf("%d", &a[i]);
            bucket[a[i]] = 1;
        }

        for (int i = 0; i < n; i++)
        {
            if (bucket[a[i]] == 1)
            {
                printf("%d ", a[i]);
                bucket[a[i]] = 0;
            }
        }
        
        putchar('\n');
    }
    return 0;
}
```

