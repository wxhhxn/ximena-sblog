---
title: LCS
date: 2021-09-12 09:09:28
tags:  summary
categories: DP
---

求最长公共子序列
核心代码：

```cpp
int a[maxn];
int b[maxn];
///a，b序列，求最长公共子序列
for(int i=1;i<=n;i++)
{
   for(int j=1;j<=m;j++)
   {
      if(a[i]==b[j])
      {
         dp[i][j]=dp[i-1][j-1]+1;
      }
      else if(dp[i-1][j]>=dp[i][j-1])
      {
         dp[i][j]=dp[i-1][j];
      }
      else
      {
          dp[i][j]=dp[i][j-1];
      }
   }
```
记录路径：应用一个path[maxn][maxn]记录路径

```cpp
for(int i=1; i<=n; i++)
        {
            for(int j=1; j<=m; j++)
            {
                if(a[i]==b[j])
                {
                    dp[i][j]=dp[i-1][j-1]+1;
                    path[i][j]=1;
                }
                else if(dp[i-1][j]>=dp[i][j-1])
                {
                    dp[i][j]=dp[i-1][j];
                    path[i][j]=2;
                }
                else
                {
                    dp[i][j]=dp[i][j-1];
                    path[i][j]=3;
                }
            }
        }
```
然后通过递归回溯路径
也可以直接通过一个string的二维数组 添加后面的相同元素这样子就不需要递归处理了
