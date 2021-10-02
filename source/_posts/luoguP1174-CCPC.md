---
title: luoguP1174(CCPC)
date: 2021-09-08 16:09:46
tags:
categories: DP
---

先对这个矩阵进行预处理，将每一列分成n块，每一块以n为开头，这样子便于后续计算

```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef pair<int, int> P;
const int INF = 0x3f3f3f3f;
const int N = 210;
const int MOD = 998244353;
const double eps = 1e-10;
#define bug(x) cout<<#x<<"=="<<x<<endl;
typedef pair<int,int> pp;
int fs[240][240] = { 0 };
bool kind[240][240] = { 0 };
int dy[240][240] = { 0 };
int dn[240][240] = { 0 };
int dpn[240][240] = { 0 };
int dpy[240][240] = { 0 };
int main()
{
    int n,m,k;
    scanf("%d %d %d",&n,&m,&k);
    for(int i=1; i<=n; i++)
    {
        for(int j=1; j<=m; j++)
        {
            char x;
            cin>>fs[i][j]>>x;
            if(x=='Y')
            {
                kind[i][j] = 1;
                ///该地方可以获得一个子弹
            }
        }
    }
    for (int j = 1; j <= m; j++) {///每一列
		int tot = 0;
		for (int i = n; i >= 1; i--) {
			if (kind[i][j] == 1) dy[j][tot] += fs[i][j];///不消耗子弹，可以放到同一类上面
			else {
				tot++;
				dn[j][tot] = dy[j][tot - 1] + fs[i][j];///dn表示此处为消耗子弹的地方，而且这一排拢共消耗tot个子弹得到的分数
				dy[j][tot] = dn[j][tot];///dy表示此处为不消耗子弹的地方
			}
		}
	}
	for (int i = 1; i <= m; i++) {
		for (int j = 0; j <= k; j++) {
			for (int l = 0; l <= min(j, n); l++) {
				dpy[i][j] = max(dpy[i][j], dpy[i - 1][j - l] + dy[i][l]);
				if (l != 0) dpn[i][j] = max(dpn[i][j], dpy[i - 1][j - l] + dn[i][l]);
				if (j != l) dpn[i][j] = max(dpn[i][j], dpn[i - 1][j - l] + dy[i][l]);
			}
		}
	}
	printf("%d\n", dpn[m][k]);
}

```
