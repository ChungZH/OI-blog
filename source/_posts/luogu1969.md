---
title: 洛谷 P1969 积木大赛
date: 2019-06-01 11:20
categories:
- 题解
tags:
- 模拟
---

## 题目链接

https://www.luogu.org/problemnew/solution/P1969

<!-- More -->

## 题解

now 就是当前高度，ans 就是答案。

now 就是当前高度，ans 就是答案。

首先 now = ans = a[0] 就是怎么样最少至少都会操作 a[0] 次。

然后一个一个看，如果大于 now，ans += a[i] - now 也就是增加操作次数，now = a[i] 更新当前高度。

```cpp
#include <bits/stdc++.h>
using namespace std;

long long n, now, ans;
long long a[1000000];

int main()
{
    cin >> n;
    
    for (int i = 0; i < n; i++)
    {
        cin >> a[i];
    }
    
    now = ans = a[0];
    
    for (int i = 1; i < n; i++)
    {
        if (a[i] > now)
        {
            ans += a[i] - now;
        }
        
        now = a[i];
    }
    
    cout << ans << endl;
    
    return 0; 
}
```

