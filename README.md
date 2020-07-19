# 2020-第三场
题解 标程 总结


这场比赛做了三个题 A、B、L

题意：
小月有 n 单位的时间都在钓鱼，每个单位时间有四种状态，有蛤蜊/没蛤蜊 , 有鱼/没鱼。小月事先知道这 n 个时间点的状态。每个时间点有四种可能 的动作：
1.若该时间点有鱼，则可以直接钓鱼。
2.若该时间点有蛤蜊，则可以用该蛤蛎制作一个鱼饵。 
3.若该时间点身上有至少一个鱼饵，则可以用一个鱼饵钓一条鱼，钓完后就少 了一个鱼饵。 
4. 什么事都不做。
• 请问小月最多可以钓多少条鱼。

A题贪心，主要观察：有鱼的时候就钓鱼一定是最好的策略之一 
• 用鱼饵钓鱼会多浪费一个鱼饵。 
• 若该时间拿来制作鱼饵，顶多之后用该鱼饵掉一条鱼，还多占用未来 的时间，不如现在就直接钓鱼。 
• 于是我们只需再考虑有无蛤蜊的情形作为子题。

AC代码：
#include<bits/stdc++.h>
using namespace std;
const int maxn=2e5+10;
typedef long long ll;
 
string str;
 
int main(){
   int T;
   cin >> T;
   while(T--){
        int n;
        cin >> n;
        cin >> str;
        int cnt = 0;
        int yr = 0;
        int flag = 0;
        for(int i = 0;i < n;i++){
            if(str[i] == '2' || str[i] == '3')
                flag++;
        }
        for(int i = 0;i < n;i++){
            if(str[i] == '0'){
                if(yr > 0){
                    cnt++;
                    yr--;
                }
            }
            else if(str[i] == '1'){
                if(yr >= (n - i - flag)){
                    cnt++;
                    yr--;
                }
                else{
                    yr++;
                }
            }
            else if(str[i] == '2'){
                cnt++;
                flag--;
            }
            else{
                cnt++;
                flag--;
            }
        }
        cout << cnt << endl;
   }
   return  0;
}


C题
题意：正序或逆序给你20个点，由你判断这些点是左手还是右手。

思路，判断正序还是逆序，然后求连续点之间的距离就可以判断。在多边形正逆序判断上卡了很久，后来发现可以用格林公式求出正逆序。

博客链接：https://blog.csdn.net/qq_37602930/article/details/80496498

代码：
double d = 0;
for (int i = 0; i < n - 1; i++) {
    d += -0.5 * ( y[i + 1] + y[i]) * (x[i + 1] - x[i]);
}
if ( d > 0)
    cout << "counter clockwise" << endl;
else
    cout << "clockwise" << endl;




B题
题意：
• 有一个字符串，有两种操作： 
1.询问第 x 个字符。 
2.把最左边的 x 个字符搬到最右边或把最右边 x 个字符搬到最左边。

考虑将字符构成环，用取模的方法来O(1)求解

AC代码：
#include<bits/stdc++.h>
  
using namespace std;
const int maxn = 2e6 + 10;
char s[maxn];
  
int main(){
    int T, x, len, num = 0;
    scanf("%s%d",s,&T);
    len = strlen(s);
    while(T--){
        getchar();
        char op;
        scanf("%c%d",&op,&x);
        if(op == 'A') {
            x--;
            int pos = (x - num + len) % len;
            printf("%c\n",s[pos]);
        }
        else {
            num -= x;
            if(num > len) num -= len;
            else if(num < -len) num += len;
        }
    }
}


L题：
 题意：判断一个字符串是否为 lovely 开头，不分大小写。

签到题

AC代码：
#include<bits/stdc++.h>
using namespace std;
const int maxn=2e5+10;
typedef long long ll;
const ll Mod = 998244353;
ll n,k;
ll a[maxn];
//int mp[5000+10][5000+10];
vector<int> ve;
map<int,int> mp;
 
int main(){
 
   string s;
   cin >> s;
   for(int i=0;i<s.length();i++){
        if(s[i]>='A'&&s[i]<='Z') s[i]+=32;
   }
    string temp{s.begin(),s.begin()+6};
   // cout << temp << endl;
    if(temp=="lovely") cout << "lovely" << endl;
    else cout << "ugly" << endl;
    return  0;
}

