---
title: 洛谷 P3984 高兴的津津
date: 2019-05-27 19:25:00
tags:
- 模拟
categories: 
- 题解
---

## 题目链接

https://www.luogu.org/problemnew/show/P3984

<!-- More -->

## 题解

很简单的啦。

被 NHOI 一顿神操作给弄进了模拟赛，一模一样的。。。

- sum：累计开心的天数
- sta：上一次开始开心的时候

首先 sum = T，sta = a[0]。

如果上次开心还没结束，a[i] 就来了，sum 就加上 a[i] 减去 sta。

否则就 sum + T，sta = a[i]。

拿样例试一下：

```
3 5
1 2 10
```

ok，现在循环没开始，T 是 5，sum = T，sta = a[0]。

循环开始了，i=1，a[i] 是 2，sta 是 1，`2 < 1 + 5` 这个条件成立，所以 sum += 2 - 1，sta = 2。

i=2，a[i] 是 10，sta 是 2，`10 < 2 + 5` 这个条件不成立，所以 sum += 5，sta = a[i]。

最后输出 sum 即可。

```cpp
#include <bits/stdc++.h>
using namespace std;
int main()
{
	int N, T, sum = 0, sta = 0;
	
	cin >> N >> T;
	
	int a[200002];
	
	for (int i = 0; i < N; i++) cin >> a[i];
	
	sum = T; sta = a[0];
	
	for (int i = 1; i < N; i++)
	{
		if (a[i] < sta + T)
		{
			sum += a[i] - sta;
			sta = a[i];
		} else {
			sum += T;
			sta = a[i];
		}
	}
	
	cout << sum << endl;
	return 0;
}
```