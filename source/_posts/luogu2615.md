---
title: 洛谷 P2615 神奇的幻方
date: 2019-06-01 11:10
categories:
- 题解
tags:
- 模拟
---

## 题目链接

https://www.luogu.org/problemnew/show/P2615

<!-- More -->

## 题解

其实很简单嘛，模拟就好啦。。

```cpp
#include <iostream>
#include <algorithm>
      
using namespace std;

int a[45][45] = { 0 };

int main()
{
    int n;
    int k, prevX, prevY;
    
    cin >> n;
    
    a[1][n/2+1] = 1; // 首先将 1 放在第一行中间
    k = 1;
    prevX = 1, prevY = n/2+1;

    k++;

    while (k <= n*n)
    {   
        if (prevX == 1 && prevY != n)
        {
            a[prevX = n][++prevY] = k++;
        } else if (prevY == n && prevX != 1) {
            a[--prevX][prevY = 1] = k++;
        } else if (prevX == 1 && prevY == n) {
            a[++prevX][prevY] = k++;
        } else if (prevX != 1 && prevY != n) {
            if (a[prevX-1][prevY+1] == 0)
            {
                a[--prevX][++prevY] = k++;
            } else {
                a[++prevX][prevY] = k++;
            }
        }
    }
    
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= n; j++)
        {
            cout << a[i][j] << " ";
        }
        cout << endl;
    }

    return 0;
}
```

