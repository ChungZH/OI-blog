---
title: 洛谷 P1162 填涂颜色
date: 2019-5-4 12:00:00
mathjax: true
categories: 
- 题解
tags: 
- DFS
- 连通块
---

## 题目链接

https://www.luogu.org/problemnew/show/P1162

<!-- More -->

## 题解

这道题有点意思，个人感觉比跳马和迷宫那两题都要难一点。

个人感觉 DFS 好写点，于是我就用了 DFS。

我的思路是这样的：

首先，$2$ 不可能出现在方阵边缘。因为闭合圈周围都要有数字 $1$。

所以我们先遍历方阵的四条边，用 DFS 先把闭合圈外面所有的 $0$ 改成 $2$。

这样方阵就会有三种数字：$0$、$1$、$2$。

其中，$0$ 表示在闭合圈内，$1$ 表示是闭合圈的边缘，$2$ 表示在闭合圈外。

比如下面这个样例：

```
0 0 0 0 0 0
0 0 1 1 1 1
0 1 1 0 0 1
1 1 0 0 0 1
1 0 0 0 0 1
1 1 1 1 1 1
```

经过如上处理后，就会变成这样：

```
2 2 2 2 2 2
2 2 1 1 1 1
2 1 1 0 0 1
1 1 0 0 0 1
1 0 0 0 0 1
1 1 1 1 1 1
```

所以我们只要这样输出：

- 如果是 $2$，就输出 $0$
- 如果是 $1$，就输出 $1$
- 如果是 $0$，就输出 $2$

```cpp
#include <iostream>

using namespace std;

int n;
int a[35][35];
const int dx[] {-1, 1, 0, 0},
          dy[] {0, 0, -1, 1};

void dfs(int x, int y);

int main()
{
    cin >> n;

    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= n; j++)
        {
            cin >> a[i][j];
        }
    }
    
    for (int j = 1; j <= n; j++)
    {
        if (a[1][j] == 0) { dfs(1, j); }
        if (a[n][j] == 0) { dfs(n, j); }
    }

    for (int i = 1; i <= n; i++)
    {
        if (a[i][1] == 0) { dfs(i, 1); }
        if (a[i][n] == 0) { dfs(i, n); }
    }

    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= n; j++)
        {
            if (a[i][j] == 2) cout << 0 << ' ';
            else if (a[i][j] == 0) cout << 2 << ' ';
            else cout << 1 << ' ';
        }
        cout << endl;
    }


    return 0;
}

void dfs(int x, int y)
{
    if (x < 1 || x > n || y < 1 || y > n || a[x][y] != 0)
    {
        return;
    } else {
        a[x][y] = 2;
    }

    for (int i = 0; i < 4; i++)
    {
        int tx = x+dx[i];
        int ty = y+dy[i];

        dfs(tx, ty);
    }
}
```