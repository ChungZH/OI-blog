---
title: 2019~2020 创新班递推学习笔记
tags:
- 递推
- 创新班
categories:
- 笔记
date: 2019/11/10 12:07:00
---

> 呼~今年的创新班开得格外迟，都已经开学第十周了。
> 
> 不过比起之前，今年的创新班倒是水平高多了，和初中生一个班呢！

递推的学习是 2019/11/02 -> 2019/11/09，两节课。~~当然有可能未完待续~~

<!-- more -->

## The First Lesson

首先讲了一下加法原理和乘法原理，~~一知半解~~。

然后讲了一下上楼梯和骨牌这两个例题，小测了一下。。

还有一个 pdf：[递推.pdf](/pdf/递推.pdf)

## The Second Lesson

上 SMOJ 测试咯啦啦啦

### T1:

**题目描述**：给你 n 个钱币，去一个不找钱的商场买东西，你可以买多少种价格的物品？

**输入格式**：第一行：一个整数n，范围在[0, 100]。第二行：n个整数，每个数范围在[1, 100]

**输出格式**：可能买的不同价格数。(包括价格 0)


`f[i][j]` 表示用前i枚硬币是否能能够凑出 $j$ 元
`f[i][j] = true` 至少要满足以下两个条件之一（分类讨论）：

1. 不用第 $i$ 枚硬币，则要满足 `f[i-1][j] = true`
2. 用第 $i$ 枚硬币，则要满足 `f[i-1][j-a[i]] = true, j >= a[i]`



图示：

![](https://raw.githubusercontent.com/ChungZH/picgo-upload/master/dt-t1-smoj-1918.png)

```cpp
// [SMOJ 1918] 
// 2019/11/02 -> 2019/11/09 创新班 
// 递推 第一题 
// 给你 n 个钱币，去一个不找钱的商场买东西，你可以买多少种价格的物品？ 
 
/*
f[i][j] 表示用前i枚硬币是否能能够凑出 j 元
f[i][j] = true 至少要满足以下两个条件之一： 
1. 不用第 i 枚硬币，则要满足 f[i-1][j] = true
2. 用第 i 枚硬币，则要满足 f[i-1][j-a[i]] = true, j >= a[i] 
*/ 

#include <bits/stdc++.h>
using namespace std;
int ans = 1;
bool f[10003][10003];
int main()
{
	freopen("1918.in", "r", stdin);
	freopen("1918.out", "w", stdout);
	int n;
	cin >> n;
	
	int a[n+3];
	for (int i = 1; i <= n; i++)
	{
		cin >> a[i];
	} 
	
	f[0][0] = true;
	
	for (int i = 1; i <= n; i++)
	{
		f[i][0] = true;
		for (int j = 1; j <= 10000; j++)
		{
			if (f[i-1][j] == true)
			{
				f[i][j] = true;
			}
			if (j >= a[i] && f[i-1][j-a[i]] == true)
			{
				f[i][j] = true;
			}
		}
	}
	
	int ans = 0;
	for (int i = 0; i <= 10000; i++)
	{
		if (f[n][i] == true) ans++;
	}
	
	cout << ans << endl;
	return 0;
}
```

### T2：

**题目描述**：给你n个正整数，每个数可选或不选，问可以选一些数它们的和可以生成多少100以内的不同数？

**输入格式**：第一行：一个整数n，范围在[0, 100000]。第二行：n个整数，每个数范围在[1, 10000]

**输出格式**： 可生成数。(包括0和100)

和上一题基本上是一样的，只不过要求 100 以内而已。

```cpp
// [SMOJ 1919] 
// 2019/11/02 -> 2019/11/09 创新班 
// 递推 第二题 
// 给你n个正整数，每个数可选或不选，问可以选一些数它们的和可以生成多少100以内的不同数？ 

/*
和上一题基本一样，只是 100 以内。
*/

#include <bits/stdc++.h>
using namespace std;
int ans = 1;
bool f[100003][103];
int a[100003];
int main()
{
	freopen("1919.in", "r", stdin);
	freopen("1919.out", "w", stdout);
	int n;
	cin >> n;
	for (int i = 1; i <= n; i++)
	{
		int t;
		cin >> t;
		
		if (t <= 100)     // 大于 100 就不要了
			a[i] = t;
	} 
	f[0][0] = true;
	for (int i = 1; i <= n; i++)
	{
		f[i][0] = true;
		for (int j = 1; j <= 100; j++)
		{
			if (f[i-1][j] == true)
			{
				f[i][j] = true;
			}
			if (j >= a[i] && f[i-1][j-a[i]] == true)
			{
				f[i][j] = true;
			}
		}
	}
	
	int ans = 0;
	for (int i = 0; i <= 100; i++)
	{
		if (f[n][i] == true) ans++;
	}
	
	cout << ans << endl;
	return 0;
}
```

### T3：

**题目描述**：给你n个正整数，每个数可选或不选，要求选一些数，使它们的和为100，问有多少种方案？

**输入格式**： 第一行：一个整数n，范围在[1, 100000]。第二行：n个整数，每个数范围在[1, 10000]

**输出格式**： 方案数。（答案不超过2^63）



![](https://raw.githubusercontent.com/ChungZH/picgo-upload/master/dt-t3-smoj-1920.png)

还是在上一题的基础上改一改。

```cpp
// [SMOJ 1920] 
// 2019/11/02 -> 2019/11/09 创新班 
// 递推 第三题 
// 给你n个正整数，每个数可选或不选，要求选一些数，使它们的和为100，问有多少种方案？ 

/*
在上一题的基础上修改
*/
#include <iostream>
#include <cmath>
#include <algorithm>
#include <cstdio>

using namespace std;

int n, a[100005], useful;
long long f[100005][105];

int main()
{
    freopen("1920.in", "r", stdin);
    freopen("1920.out", "w", stdout);
    cin >> n;

    for (int i = 1; i<= n; i++)
    {
        int x;
        cin >> x;
        if (x <= 100) a[++useful] = x;
    }

    f[0][0] = 1;
    for (int i = 1; i <= useful; i++)
    {
        f[i][0] = 1;
        for (int j = 1; j <= 100; j++)
        {
            f[i][j] = f[i-1][j];
            if (j >= a[i]) f[i][j] += f[i-1][j-a[i]];
        }
    }

    cout << f[useful][100] << endl;
    return 0;
}
```


