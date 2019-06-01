---
title: 洛谷 P2799 国王的魔镜
date: 2019-06-01 14:05:56
tags:
- 字符串
- 模拟
---

## 题目链接

https://www.luogu.org/problemnew/show/P2799

<!-- More -->

## 题解

利用 **增加的那部分是反的** 这个规律，每次把字符串分成两半，分别记作 `left` 和 `right`。然后反转其中的一个，再对比一下是不是一样的，直到不一样了为止。

```cpp
#include <iostream>
#include <string>
#include <algorithm>

using namespace std;

int main()
{
    string s;
    cin >> s;

    int ans = s.length();

    while (s.length() > 1)
    {
        string left  = s.substr(0, s.length()/2);
        string right = s.substr(s.length()/2, s.length()-1);
        reverse(left.begin(), left.end());

        // cout << "left=" << left << "  right=" << right << endl;

        if (left != right)
            break;

        s = left; 
        ans /= 2;
    }

    cout << ans << endl;

    return 0;
}
```

