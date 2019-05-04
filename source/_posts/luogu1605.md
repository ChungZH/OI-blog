---
title: 洛谷 P1605 迷宫
date: 2019-5-4 11:00:00
tags:
- DFS
---

## 题目链接

https://www.luogu.org/problemnew/show/P1605

## 题解

就是一道 DFS，不过坑有点多。

一道 `普及-` 的题目提交了 3 次才 A 掉，还是太弱了......

坑点总结：

- 起点不是 `1, 1`，而是数据中的 `sx, sy`。
- 记得要把**起点设为已经访问**！！！
  我就因为这个一直没 AC，看了看题解才意识到这个坑。。。

其它的就没什么了，DFS 打熟练了都会写。

```cpp
#include <iostream>
using namespace std;

void dfs(int x, int y);
int ans, n, m, t;
int sx, sy, fx, fy;
int a[10][10];
bool book[10][10];
const int dx[4] {-1, 1, 0, 0},
          dy[4] {0, 0, -1, 1};

int main()
{
    cin >> n >> m >> t;
    cin >> sx >> sy >> fx >> fy;

    for (int i = 0; i < t; i++)
    {
        int x, y;
        cin >> x >> y;

        a[x][y] = -1;
    }

    book[sx][sy] = 1;    

    dfs(sx, sy);

    cout << ans << endl;
    return 0;
}

void dfs(int x, int y)
{
    if (x == fx && y == fy)
    {
        ans++;
        return;
    }

    for (int i = 0; i < 4; i++)
    {
        int tx = x+dx[i], ty = y+dy[i];

        if (tx < 1 || tx > n || ty < 1 || ty > m) continue;

        if (book[tx][ty] == 0 && a[tx][ty] != -1 && tx <= n && tx >= 1)
        {
            book[tx][ty] = 1;
            dfs(tx, ty);
            book[tx][ty] = 0;
        }
    }
}
```