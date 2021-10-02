---
title: Crossed Matchings POJ
date: 2021-09-16 09:38:49
tags: practise
categories: DP
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
typedef pair<int,int> pp;
typedef pair<pp,int> ppp;
const ll maxn = 1e6+1000;
int dp[105][105]= {0};
int a[105] = { 0 };
int b[105] = { 0 };
int main()
{
    int T;
    scanf("%d",&T);
    while(T--)
    {
        int n,m;
        memset( dp,0,sizeof(dp) );
        scanf("%d %d",&n,&m);
        for(int i=1; i<=n; i++)
            scanf("%d",&a[i]);
        for(int i=1; i<=m; i++)
            scanf("%d",&b[i]);

        for(int i=2; i<=n; i++)
        {
            for(int j=2; j<=m; j++)
            {

                dp[i][j]=max(dp[i-1][j],dp[i][j-1]);
                 if(a[i]!=b[j])
                 {
                     int k1=i-1,k2=j-1;
                     for(k1=i-1;k1>=1;k1--)
                     {
                         if(a[k1]==b[j])
                         {
                             break;
                         }
                     }
                     for(k2=j-1;k2>=1;k2--)
                     {
                         if(b[k2]==a[i])
                         {
                             break;
                         }
                     }

                     if(k1&&k2)
                     {
                         dp[i][j]=max(dp[i][j],dp[k1-1][k2-1]+2);
                     }
                 }
            }
        }
        printf("%d\n",dp[n][m]);
    }
}

```



类似于lcs的思想，比赛的时候没有注意数据范围QwQ呜呜呜呜呜太遗憾了
