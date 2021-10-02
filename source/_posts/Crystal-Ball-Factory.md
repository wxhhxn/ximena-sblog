---
title: Crystal Ball Factory
date: 2021-09-12 11:23:53
tags:
---

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>
#include <cmath>
#include <string>
#define bug(x) cout<<#x<<"=="<<x<<endl;
using namespace std;
typedef long long ll;
const int maxn = 1005;
ll dp[maxn][maxn]={0};
struct node
{
    int price;
    int need;
} week[maxn];
int n;

int main()
{
    while(scanf("%d",&n)!=EOF&&n)
    {
        int bcost,scost,mxcap;
        scanf("%d %d %d",&bcost,&scost,&mxcap);
        ///每周制作水晶球的基础花费
        ///每个水晶球的储存花费
        ///最大仓库的储存容量
        memset( dp, 0x3f3f3f, sizeof(dp) );
        for(int i=1; i<=n; i++)
        {
            scanf("%d %d",&week[i].price,&week[i].need);
        }
        dp[0][0] = 0;
        for(int i=1;i<=n;i++)
        {
            for(int j=0; j+week[i].need<=mxcap; j++)
            {
                dp[i][j]=min(dp[i][j],dp[i-1][j+week[i].need] + (ll)(j)*(ll)(scost));
            }
            for(int j=0;j<=mxcap;j++)
            {
                for(int k=max(1,week[i].need-j);k+j-week[i].need<=mxcap;k++)
                {
                    ///至少需要生产week[i].need-j个水晶球
                    dp[i][ k+j-week[i].need ] = min(bcost + week[i].price*k + dp[i-1][j] + (k+j-week[i].need)*scost,dp[i][ k+j-week[i].need ]);
                }
            }
        }
        ll minn=0x3f3f3f;
        for(int i=0;i<=mxcap;i++)
        {
            minn=min(dp[n][i],minn);
        }
        printf("%lld\n",minn);
    }
}

```

