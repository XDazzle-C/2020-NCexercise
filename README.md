# 2020-
题解 标程 总结
A了两个题。 F，J

/*
第一场
*/

F题题意简单，判断两个字符串a,b无限循环后的字典序大小。WA了一发，内存超限，思路有问题，想的是求两字符串长度的LCA然后将两字符串处理成一样的长度，再直接用string的特性判断大小，结果超了内存。 然后转换思路，推测在长度为2 * max(a,b)的范围内必然可以判断出字典序的大小，直接遍历，核心为取模循环，A了。
代码：
#include <bits/stdc++.h>

using namespace std;

typedef long long ll;

const int N = 2e5 + 9;

string str1,str2;

int main(){
    while(cin >> str1 >> str2){
        ll a,b;
        a = str1.size();
        b = str2.size();
        int i = 0;
        int flag = 0;
        while(i < 2 * max(a,b)){
            if(str1[(i + a) % a] > str2[(i + b) % b]){//标红的是算法核心
                flag = 1;
                break;
            }
            else if(str1[(i + a) % a] < str2[(i + b) % b]){
                flag = -1;
                break;
            }
            i++;
        }
        if(flag == 1)
            cout << '>' << endl;
        else if(flag == 0)
            cout << '=' << endl;
        else
            cout << '<' << endl;
    }
    return 0;
}
J题题意最初没看懂，队友解释后才了解，发现题意也是比较简单的，难度在于找规律，就求一个积分的结果的逆元，最初的想法是推公式，解不定积分求出原函数F(X),然后就可得出F(1) - F(0)即结果为F(1)然后求一个逆元即可，但是。。。。。难度超出我的想象，甚至我觉得可能求不出，于是转换思路找规律，手推之后发现分子P始终为1，q的前四项为6、30、140、630然后瞎推了一下，蒙出了个结果（n!）^ 2 / (2n + 1)!,样例都过了就交，然而还是WA了一发，时间超限，说明式子没有推错，发现第一次在n次循环内计算阶乘求逆元时间复杂度太过于高，于是用了两个数组来存放数据，初始化了n!以及(2n + 1)!，那么之后就是O(1)的复杂度，AC。
代码：
#include <bits/stdc++.h>
#define MOD 998244353
using namespace std;

typedef long long ll;

const int N = 1e6 + 9;

ll num1[N];
ll num2[N];

ll inv(ll x) {//除法取模
	ll b = MOD - 2, ans = 1;
	while (b) {
		if (b & 1) {
			ans = ans * x % MOD;
		}
		x = x * x % MOD;
		b >>= 1;
	}
	return ans;
}

void check(){
    ll t = 1;
    for(int i = 1;i <= 1000000;i++){
        t *= i;
        t %= MOD;
        num1[i] = (t * t) % MOD;
    }
}

void check2(){
    ll t = 1;
    int j = 1;
    for(int i = 1;i <= 2 * 1000000 + 1;i++){
        t *= i;
        t %= MOD;
        if(i == 2 * j + 1){
            num2[j] = t;
            j++;
        }
    }
}

int main(){
    int n;
    check();//此处为预处理
    check2();
    //cout << ((1 % MOD) * inv(6 % MOD)) % MOD<< endl;
    while(cin >> n){
        cout << ((num1[n] % MOD) * inv(num2[n] % MOD)) % MOD<< endl;
    }
    return 0;
}

还看了其他的一个题，A题，看榜发现A题一血才用了13分钟，认为难度应该不大，结果题目没读懂，过得比较多的H、I两题队友说是图论题，就没去看，图论需要好好补。

总结：看了一下榜单，如果三题快的话拿牌没问题，还是太次了。
