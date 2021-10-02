---
title: 855E Salazar Slytherin's Locket
date: 2021-09-12 16:50:25
tags: cf
categories: 数位DP
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
const int maxn = 3005;
ll l,r;
int b;
ll dp[11][100][maxn] = { 0 };
int a[maxn] = { 0 };
int sum[10] = { 0 };
///每个数的和
///lead前导0
///limit有没有数的边界限制
ll dfs(int pos,int state,bool lead,bool limit)
{
    if(!pos)
    {
        return !state;
    }
    if(!limit&&!lead&&dp[b][pos][state]!=-1)
    {
        return dp[b][pos][state];
    }
    ll ans=0;
    int up=b-1;
    if(limit)
    {
        up = a[pos];
    }
    for(int i=0;i<=up;i++)
    {
        ans += dfs( pos-1,( (lead&&i==0)?state:(1<<i)^state ),lead&&(i==0),limit&&i==up );
    }
    if(!limit&&!lead)
    {
        dp[b][pos][state]=ans;
    }
    return ans;
}
ll slove(ll l)///处理
{
    int tot=0;
    while(l)
    {
        tot++;
        a[tot] = (int)(l%b);
        l /= b;
    }
    return dfs(tot,0,1,true);
}
int main()
{
    int q;
    scanf("%d",&q);
    memset( dp,-1,sizeof(dp) );
    while(q--)
    {
        cin>>b>>l>>r;
        l--;
        cout<<slove(r)-slove(l)<<endl;
    }
}

```

无他，数位dp的板子~

一般求数字的范围就需要判断有无前导0

利用状压来计算每一种数字在每一位上出现的次数是计数还是偶数，很不错的思想
