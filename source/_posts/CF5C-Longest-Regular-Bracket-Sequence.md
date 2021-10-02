---
title: CF5C Longest Regular Bracket Sequence
date: 2021-09-08 17:42:48
tags: cf
categories: 模拟
---

[https://www.luogu.com.cn/problem/CF5C]()

看最长的合法字符串的长度和数目
首先左右括号对应才是合法的
利用一个数组模拟出栈和入栈将左括号和右括号进行匹配
e.g:)((())))(()())
01111110111111
1代表的是该位置有匹配的括号，最后求最长的连续1的字符串即可

```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef pair<int, int> P;
const int INF = 0x3f3f3f3f;
const int maxn = 1e6+18;
const int MOD = 998244353;
const double eps = 1e-10;
#define bug(x) cout<<#x<<"=="<<x<<endl;
typedef pair<int,int> pp;
int sta[maxn] = { 0 };
int c[maxn] = { 0 };
int main()
{
    string a;
    cin>>a;
    int len = a.length();
    int t=0;
    for(int i=0; i<len; i++)
    {
        if(a[i]=='(')
        {
            t++;
            sta[t]=i;
        }
        else if(t)///栈中有可以匹配的左括号
        {
            c[ sta[t] ]=1;
            c[i] = 1;
            ///bug(i);
            ///bug(sta[t]);
            ///匹配成功
            t--;
            ///出栈
        }
    }
    int ans = 0;
    int sum = 0;
    int w=0;
    for(int i=0;i<len;i++)
    {
        if(c[i]==1)
        {
            w++;
            ///bug(w);
            if(w>ans)
            {
                ans = w;
                sum = 1;
            }
            else if(w==ans)
            {
                sum++;
            }
        }
        else
        {
            w = 0;
        }
    }
    if(ans)
    {
        printf("%d %d\n",ans,sum);
    }
    else
    {
        printf("0 1\n");
    }
}

```
