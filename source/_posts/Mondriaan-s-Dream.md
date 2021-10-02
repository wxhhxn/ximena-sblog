---
title: Mondriaan's Dream
date: 2021-09-26 16:59:27
tags: HDU
categories: 轮廓线DP
---

```cpp
#include<iostream>
#include<cstdio>
#include<vector>
#include<map>
#include<queue>
#include<stack>
#include<string>
#include<cstring>
#include<cmath>
#include<algorithm>
using namespace std;
typedef long long ll;
#define lson rt<<1,l,mid
#define rson rt<<1|1,mid+1,r
const int maxn=1e5+10;
#define INF 0x3f3f3f3f
int n,m;
ll dp[2][(1<<15)] = { 0 };
///循环数组＋dp
#define u dp[0][s]
int cur = 0;
inline void update(int a,int b)
{
    if(b&(1<<m))///有无空的地方
        dp[cur][b^(1<<m)] += dp[cur^1][a];
}
int main()
{
    int n,m;
    while(scanf("%d %d",&n,&m)&&n&&m)
    {
        if(n>m)swap(n,m);
        memset(dp,0,sizeof(dp));
        dp[1][0] = 1;
        for(int i=0; i<n; i++)
        {
            for(int j=0; j<m; j++)
            {
                swap(dp[1],dp[0]);
                fill(dp[1],dp[1]+(1<<m),0);

                for(int s=0; s<(1<<m); s++)
                {
                    if(u)
                    {
                        if(j!=m-1&&(!( (s>>j) &3)))
                            dp[1][s^( 1<<(j+1) ) ] += u;
                        dp[1][s^(1<<j)] += u;
                    }
                }
            }
        }
        cout<<dp[1][0]<<endl;
    }
}

```

根据图的轮廓线用类似于状压的方法求值
