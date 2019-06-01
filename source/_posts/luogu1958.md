---
title: 洛谷 P1958 上学路线_NOI导刊2009普及（6）
date: 2019-06-01 11:30
categories:
- 题解
tags:
- DFS
- 递推
- 动态规划
---

## 题目链接

https://www.luogu.org/problemnew/show/P1958

<!-- More -->

## 题解

dp DFS 都可以吧。

flag 是标记可不可以通行。

由于只能往东和北走，所以一个地方的走法数量就是它 **西（左）边走法之和** 加 **南（下）边走法之和**。

```cpp
#include <iostream>

using namespace std;

int a, b, n, ans;
bool flag[50][50];
int dp[50][50]; 

int main()
{
    cin >> a >> b >> n;
    
    int x, y;
    
    for (int i = 1; i <= n; i++)
    {
        cin >> x >> y;
        flag[x][y] = true;
    }
    
    dp[1][1] = 1;
    
    for (int i = 1; i <= a; i++)
    {
        for (int j = 1; j <= b; j++)
        {
            if (i == 1 && j == 1 || flag[i][j] == true) continue;
            
            dp[i][j] = dp[i-1][j] + dp[i][j-1];
        }
    }
    
    cout << dp[a][b] << endl;
    return 0;
}
```

