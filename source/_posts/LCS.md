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

特别的LCS DP求法

```cpp
 #include<bits/stdc++.h>
    #include <iostream>
    #include<cstdio>
    #include <map>
    #include<cstring>
    using namespace std;
    #define ll long long
    #define bug(x) cout<<#x<<"=="<<x<<endl;
    const ll maxn=2e5+10;
    const int INF = 0x3f3f3f3f;
    int n;
    string b;
    char mls[20];
    int dp[maxn][20], nowl[maxn][20], nowr[maxn][20];
    int nowdp[maxn]= {0};
    int check(int l, int r,int len)
    {
        for(int i=0; i<=len; i++)
        {
            dp[0][i]=0;
            nowr[0][i]=nowl[0][i]=0;
            //全部都要初始化一下子
        }
     
        for(int i = 1; i <= n; ++i)
        {
            for(int j = 1; j <= len; ++j)
            {
                dp[i][j] = dp[i - 1][j];
     
                nowr[i][j]=nowr[i-1][j];
                nowl[i][j]=nowl[i-1][j];
     
                if(b[i] == mls[j])
                {
                    dp[i][j]++;
                    if(j == l && nowl[i][j] == 0)
                    {
                        nowl[i][j] = i;
                    }
                    else if(j == r)
                    {
                        nowr[i][j] = i;
                    }
                }
                if(dp[i][j] < dp[i][j - 1])
                {
                    dp[i][j] = dp[i][j - 1];
     
                    nowr[i][j]=nowr[i][j-1];
                    nowl[i][j]=nowl[i][j-1];
     
                }
            }
        }
        return dp[n][len];
    }
     
    void change(char l, char r)
    {
        int tot = 1;
        for(char i = '0'; i <= l; i++)
        {
            mls[tot] = i ;
            tot++;
        }
        for(char i = r; i >= l; i--)
        {
            mls[tot] = i ;
            tot++;
        }
        for(char i = r; i <='9'; i++)
        {
            mls[tot] = i ;
            tot++;
        }
        ///bug(tot);
    }
     
    int main()
    {
        int T;
        scanf("%d", &T);
        while(T--)
        {
            scanf("%d", &n);
            cin>>b;
            for(int i=0; i<n; i++)
            {
                nowdp[i]=INF;
            }
            for(int i = 0; i < n; i++)
            {
                *lower_bound(nowdp, nowdp + n, b[i]) = b[i];
            }
            int maxx = lower_bound(nowdp, nowdp + n, INF) - nowdp;
            b=' '+b;
            int ansl, ansr;
            ansl = ansr = 1;
            for(char i = '0'; i <='9'; i++)
            {
                for(char j = i + 1; j <= '9'; j++)
                {
                    change(i, j);
                    int tmp = check(i + 2-'0', j + 2-'0',12);
                    if(tmp > maxx && nowl[n][12] != 0 && nowr[n][12] != 0)
                    {
                        maxx = tmp;
                        ansl = nowl[n][12];
                        ansr = nowr[n][12];
                    }
                }
            }
            printf("%d %d %d\n", maxx, ansl, ansr);
        }
     
        return 0;
    }
```
赛中一直觉得是通过更改0~9的排序来更改求最长不下降子序列的问题，后来发现一个bug
**0123456789->012 6543 789这样子可能6前面会存在3没有加上**
**所以要更改为0123 6543 6789这样子才可以计算完全!!!!!**
相当重要，不然左右区间会一直计算的问题 这样子当每一次计算到达6的时候而且前面没有记录的翻转的时候更新左区间，而区间可以实现实时更新，因为左区间越小，右区间越大翻转的越多，这个就不多赘述。 
所以一开始往运算法则想是有瑕疵的，应该还是抓LCS的公共字符串问题。
