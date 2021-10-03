---
title: dp中的经典例题
date: 2021-10-03 12:29:23
tags: summary
categories: DP
---

# 求最长回文字符串（马拉车算法）

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
const ll int maxn = 3e7+10;
const ll int N = 4e6+10;
#define bug(x) cout<<#x<<" == "<<x<<endl;
int p[maxn] = { 0 };
///以i为中心的最大回文字符串（此时的字符串是处理过的）到左端点的距离 + 1
int id=0;///当前计算的最大长度的字符串的中心
int maxx=0;///以id为中心的最大回文字符串（此时的字符串是处理过的）的右端点+1
///求最大回文串
int main()
{
    string a;
    string b;
    cin>>a;
    b += '$';
    for(int i=0;i<a.size();i++)
    {
        b += '#';
        b += a[i];
    }
    b += '#';
    int len=b.length();
    ///预处理，将每一个字符串变成奇数串 使子串的中心固定
    int ans=0;
    int pos=2;
    for(int i=1;i<len;i++)
    {
        if(maxx>i)
        {
            p[i] = min(maxx-i,p[2*id-i]);
            ///当maxx>i的时候 说明 以id为中心，左右两端长度为maxx-id的字符串里面包含了b[i];
            ///说明 id-(i-id)和b[i]是这个字符串里面两个对称点，
            ///而且i-(i-maxx)~maxx部分也和2*id-maxx~2*id-i+(i-maxx)相同
            ///所以如果p[2*id-1]<=maxx-i -> p[i]==p[2*id-1];
            ///如果p[2*id-1]>maxx-i,只能截取肯定相同的部分即maxx-i;
        }
        else
        {
            p[i] = 1;
        }
        while(b[ i-p[i] ] ==b[ i+p[i] ] )
        {
            p[i]++;
        }
        if(i+p[i]>maxx)
        {
            maxx = i + p[i];
            id = i;
        }
        if(ans<p[i]-1)
        {
            pos=i;
            ans=p[i]-1;
        }
    }
    printf("%d\n",ans);
    ///cout<<(pos/2-1);///最长回文字符串的中心位置
    for(int i=pos/2-1-ans/2;i<=pos/2-1+ans/2;i++)
    {
        cout<<a[i];
    }
}

```

