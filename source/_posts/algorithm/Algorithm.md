
from： https://zhuanlan.zhihu.com/p/50479555

## 时间复杂度

* 基本思路

```
// 通过分析每一行的复杂度相加
// T(n) = O(f(n)) = O(2n + 1) ≈ O(n)
for(i=1; i<=n; ++i)     // f(n) = 1
{
   j = i;               // f(n) = n
   j++;                 // f(n) = n
}

```


* 常见复杂度算法
```
// O(1) 没有循环等结构， 复杂度不随某个变量而变化
int i = 1;
int j = 2;
++i;
j++;
int m = i + j;


// O(n) 如上一条所描述

// O(n^2) 双重循环
for(x=1; i<=n; x++)
{
   for(i=1; i<=n; i++)
    {
       j = i;
       j++;
    }
}

// O(logN), 这个循环需要执行的次数 x = log2^N ≈ O(logN)
int i = 1;
while(i<N)
{
    i = i * 2;
}

// O(nlogN), 复杂度为 logN 的算法循环循环 n 次
for(m=1; m<N; m++)
{
    i = 1;
    while(i<n)
    {
        i = i * 2;
    }
}

// 依此类推

```



## 空间复杂度

*  基本思想，推算 算法所需的临时空间和变量大小变化的关系

```
// 第一行new了一个数组出来，这个数据占用的大小为n，
// 这段代码的2-6行，虽然有循环，但没有再分配新的空间
// S(n) = O(n) 
int[] m = new int[n]
for(i=1; i<=n; ++i)
{
   j = i;
   j++;
}


// O(1) 算法执行所需要的临时空间不随着某个变量n的大小而变化
int i = 1;
int j = 2;
++i;
j++;
int m = i + j;


```