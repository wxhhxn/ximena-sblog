---
title: Cheat in the Game
date: 2021-09-16 13:41:00
tags: practise
categories: 博弈
---

```cpp
#include <bits/stdc++.h>
#define bug(x) cout<<#x<<"=="<<x<<endl;
using namespace std;
typedef long long ll;
const ll maxn=1e5+10;
int dp[maxn][2] = { 0 };
int a[maxn] = { 0 };
int main()
{
    int n,m;
    while(scanf("%d %d",&n,&m)!=EOF&&n&&m)
    {
        memset(dp,0,sizeof(dp));
        for(int i=1; i<=n; i++)
        {
            scanf("%d",&a[i]);
        }
        for(int i=1;i<=n;i++)
        {
            for(int j=m;j>a[i];j--)
            {
                if(dp[ j-a[i] ][0])
                {
                    dp[j][1] = 1;
                }
                if(dp[ j-a[i] ][1])
                {
                    dp[j][0] = 1;
                }
            }
            dp[ a[i] ][1]=1;
        }
        int ans=0;
        for(int i=1;i<=m;i++)
        {
            if(dp[i][1]&&(!dp[i][0]))
            {
                ans++;
            }
        }
        printf("%d\n",ans);
    }
}

```

一个先手后手的思想，因为只要是抽奇数次牌先手必胜，所以只需要计算可以组成的数而且是先手胜利的情况，最后统计即可。

于是想到了无限背包->类似于这个背包容量最多为1~m,计算通过这些卡牌转移到容量x所需要的卡牌数目
