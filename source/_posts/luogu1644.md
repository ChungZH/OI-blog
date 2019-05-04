---
title: 洛谷 P1644 跳马问题
date: 2019-5-4 10:00:00
tags:
- DFS
---

## 题目链接

https://www.luogu.org/problemnew/show/P1644

## 题解

还是不太难的 `DFS`。

虽说马可以有 8 种跳法，但是这里题目 **规定只能往右跳**，也就只有 4 个跳法了。

![P1644-1](/img/luogu1644/P1644-1.jpg)

下面代码中的 `dx` 和 `dy` 数组就是马的走法。

```cpp
#include <iostream>

using namespace std;

int ans, n, m;
const int dx[] {
    2, 1, -1, -2
},        dy[] {
    1, 2, 2, 1
};

void dfs(int x, int y);

int main()
{
    cin >> n >> m;

    dfs(0, 0);

    cout << ans << endl;
    return 0;
}

void dfs(int x, int y)
{
    if (x == n && y == m)
    {
        ans++;
        return ;
    }

    if (x < 0 || y < 0 || x > n || y > m) return; // 判断是否越界

    for (int i = 0; i < 4; i++)
    {
        dfs(x + dx[i], y + dy[i]);
    }
}
```