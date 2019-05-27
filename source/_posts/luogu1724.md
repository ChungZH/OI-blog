---
title: 洛谷 P1724 东风谷早苗
date: 2019-05-27 19:12:00
tags:
- 模拟
- 周期
categories: 
- 题解
---

## 题目链接

https://www.luogu.org/problemnew/show/P1724

<!-- More -->

## 题解

最近在洛谷上发现了这题，突然一阵熟悉的感觉...

原来是 **NHOI 模拟赛** 里面的题目！！！

怪不得呢。。。这波操作也是够 6，直接把网上的题目的背景改一下就放进自己的比赛里。。。

哦对了，还有 [这题](https://www.luogu.org/problemnew/show/P3984) 也是被同样的一波操作给弄进模拟赛了。。

------

其实很简单的一道题，模拟赛的时候就没拿满分。考完之后重新做一次就 A 了。

刚开始想得很简单，觉得直接模拟就可以了。（弄过来的时候数据范围也没写一写，导致了我产生这个错误的思路，~~差评~~）

后来直接模拟没满分，就改了一个麻烦点的做法。

分类讨论：

- T < 命令串长度：直接模拟没毛病！
- T >= 命令串长度：先模拟一次执行一遍命令串后，x 和 y 会是多少。然后乘 T / 命令串长度 ，如果还有余就再模拟一下。

这样一来，速度就上去了。

还有，其实下面的代码里面其实是可以大大简化的，把模拟命令的那部分写成一个函数的话可以大大减少代码长度。~~由于懒就没写成函数了。~~

```cpp
#include <iostream>

int main()
{
    std::string s;
    std::cin >> s;

    long long T;
    std::cin >> T;

    long long x, y, tx, ty;
    x = y = tx = ty = 0;

    if (T < s.length())
    {
        for (int i = 0; i < T; i++)
        {
            switch (s[i])
            {
            case 'E':
                x++;
                break;
            case 'S':
                y--;
                break;
            case 'W':
                x--;
                break;
            case 'N':
                y++;
                break;
            default:
                break;
            }
        }

        std::cout << x << y << std::endl;
    } else {
        for (int i = 0; i < s.length(); i++)
        {
            switch (s[i])
            {
            case 'E':
                tx++;
                break;
            case 'S':
                ty--;
                break;
            case 'W':
                tx--;
                break;
            case 'N':
                ty++;
                break;
            default:
                break;
            }
        }

        int temp = T / s.length();

        x += temp * tx;
        y += temp * ty;

        if (T % s.length() != 0)
        {
            for (int i = 0; i < T % s.length(); i++)
            {
                switch (s[i])
                {
                case 'E':
                    x++;
                    break;
                case 'S':
                    y--;
                    break;
                case 'W':
                    x--;
                    break;
                case 'N':
                    y++;
                    break;
                default:
                    break;
                }
            }
        }

        std::cout << x << " " << y << std::endl;
    }

    return 0;
}
```