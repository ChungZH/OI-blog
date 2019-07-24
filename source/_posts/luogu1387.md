---
title: 洛谷 P1387 最大正方形
date: 2019-7-20 16:01:00
mathjax: true
categories: 
- 题解
tags: 
- 二维前缀和
---

## 题目链接

https://www.luogu.org/problemnew/show/P1387

<!-- More -->

## 题解

我用的是二维前缀和的方法。

首先计算二维前缀和（如果不会就看 [OI Wiki](https://oi-wiki.org/basic/prefix-sum/#_4) 叭，~~懒得解释了~~），我们用 $b$ 数组来存前缀和，公式就是 $b_{i,j} = b_{i - 1,j} + b_{i,j - 1} - b_{i - 1,j - 1} + a_{i,j}$。 

比如下面这个矩阵：

```plain
0 1 1 1
1 1 1 0
0 1 1 0
1 1 0 1
```

计算出来的前缀和数组就是：

```plain
0 1 2 3
1 3 5 6
1 4 7 8
2 6 9 11
```

然后一个一个地枚举正方形就好了，注意枚举的时候要从边长 $2$ 开始枚举，一直到 $min(n, m)$ 结束。

枚举只要判断这个正方形中所有数字的和是不是 棱长*棱长 就行了，如果是，那么说明这是一个可行的解。

那么如何求出这个正方形中所有数字的和呢？一个公式：$b[i][j] - b[i-l][j] - b[i][j-l] + b[i-l][j-l]$ ，其中 $l$ 就是正方形的棱长。

把一种棱长的正方形都枚举完了，那就棱长加一。

```cpp
#include <iostream>
#include <algorithm>
using namespace std;
int a[103][103];
int b[103][103];
int main()
{
    int n, m;
    cin >> n >> m;

    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= m; j++)
        {
            cin >> a[i][j];
            b[i][j] = b[i][j-1] + b[i-1][j] - b[i-1][j-1] + a[i][j];
        }
    }

    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= m; j++)
        {
            cout << b[i][j] << ' ';
        }
        cout << endl;
    }

    int ans = 1;

    int l = 2;
    while (l <= min(n, m))
    {
        for (int i = l; i <= n; i++)
        {
            for (int j = l; j <= m; j++)
            {
                if (b[i][j] - b[i-l][j] - b[i][j-l] + b[i-l][j-l] == l*l)
                {
                    ans = max(ans, l);
                }
            }
        }
        l++;
    }
    
    cout << ans << endl;
    return 0;
}
```

