# 2020-牛客第二场
题解 标程 总结

A了一个题。 D题

简单的一个签到题，直接计算就可以。

代码：
#include<bits/stdc++.h>
using namespace std;
const int maxn=2e5+10;
typedef long long ll;
const ll Mod = 998244353;
ll n,k;
ll a[maxn];
int mp[50+10][50+10];
vector<int> ve[50+5];
int main(){
   int h1,h2,m1,m2,s1,s2;
   scanf("%d:%d:%d",&h1,&m1,&s1);
   scanf("%d:%d:%d",&h2,&m2,&s2);
   int ans=0;
   cout <<abs(h1*60*60+m1*60+s1-h2*60*60-m2*60-s2) << endl;
    return  0;
}


F题是开的第二个题，当时没有想到优化的方法，直接是暴力求出矩阵，然后没想到用优先队列来做，卡死了。看了题解，恍然大悟。。。。

#include <cstdio>
#include <algorithm>
using namespace std;
typedef long long LL;
#define N 5000 + 5

int n, m, k, A[N][N], B[N][N];
LL ans;

void Handle(int n, int m)
{
	static int q[N];
	for (int i = 1; i <= n; i ++)
	{
		int l = 1, r = 0;
		for (int j = 1; j < k; j ++)
		{
			for (; l <= r && A[i][q[r]] <= A[i][j]; r --) ;
			q[++ r] = j;
		}
		for (int j = k; j <= m; j ++)
		{
			for (; l <= r && q[l] + k <= j; l ++) ;
			for (; l <= r && A[i][q[r]] <= A[i][j]; r --) ;
			q[++ r] = j;
			B[j - k + 1][i] = A[i][q[l]];
		}
	}
}

int main()
{
	scanf("%d%d%d", &n, &m, &k);
	//n = 5000,m = 5000,k = 2;
	for (int i = 1; i <= n; i ++)
		for (int j = 1; j <= m; j ++)
			if (!A[i][j])
				for (int k = 1; k * i <= n && k * j <= m; k ++)
					A[k * i][k * j] = k;
	for (int i = 1; i <= n; i ++)
		for (int j = 1; j <= m; j ++)
			A[i][j] = i * j / A[i][j];
	Handle(n, m);
	for (int i = 1; i <= m - k + 1; i ++)
		for (int j = 1; j <= n; j ++)
			A[i][j] = B[i][j];
	Handle(m - k + 1, n);
	for (int i = 1; i <= n - k + 1; i ++)
		for (int j = 1; j <= m - k + 1; j ++)
			ans += B[i][j];
	printf("%lld\n", ans);
	return 0;
}




