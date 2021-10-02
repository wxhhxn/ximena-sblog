---
title: POJ poker card game
date: 2021-09-11 12:43:08
tags: practise
categories: tree
---

**霍夫曼树：给定N个权值作为N个叶子结点，构造一棵二叉树，若该树的带权路径长度达到最小，称这样的二叉树为最优二叉树，也称为哈夫曼树(Huffman Tree)。哈夫曼树是带权路径长度最短的树，权值较大的结点离根较近。**
本题就利用了霍夫曼树的求最大带权路径长度的思想。
易知：权值较小的点肯定在深度较高的位置。
通过合并果子实现：
一个树中的一个带权结点到根节点的距离是deep，权值为value，值应该为deep*value。通过合并果子，不断加深权值小的结点的深度。

```cpp
#include <bits/stdc++.h>
using namespace std;
const int maxn =1e5+18;
#define bug(x) cout<<#x<<"=="<<x<<endl;
typedef  long long ll ;
int main()
{
    int T;
    scanf("%d",&T);
    while(T--)
    {
        int n;
        scanf("%d",&n);
        priority_queue<int,vector<int>,greater<int> > pq;
        for(int i=1;i<=n;i++)
        {
            int x;
            scanf("%d",&x);
            pq.push(x);
        }
        ll ans=0;
        while(pq.size()>1)
        {
            int x=pq.top();
            pq.pop();
            int y=pq.top();
            pq.pop();
            int z=x+y;
            pq.push(z);
            ans+=z;
        }
        printf("%lld\n",ans);
    }
}

```
