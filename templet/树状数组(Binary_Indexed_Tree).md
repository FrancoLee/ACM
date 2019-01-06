## 树状数组(Binary_Indexed_Tree) 

---

### 特点：

​	在logn时间内计算区间和修改某个位置值；

​	lowbit(i):计算i的二进制表示中，从右往左数，第一个1代表的数字

​	如1-6的和为 c6+c4, 4=(l-lowbit(6)),如果i-lowbit(i)为0表示已经计算完所有前缀

​	更新C1时候，可以从图中看到要更新C2,C4,C8, 8=4+lowbit(4),4=2+lowbit(2),2=1+lowbit(1)

## 模板（HDU 1166）

---

[题目链接](http://acm.hdu.edu.cn/showproblem.php?pid=1166)

### AC代码

```
#include <iostream>
#include <stdio.h>
#include <string.h>
#include <algorithm>
#include <vector>
#include <deque>
#include <queue>
#include <map>
#include <cmath>

#define INF 0x3f3f3f;
#define esp 1e-8
using namespace std;
const int MAXN = 50010;
int c[MAXN];
int n;
//在logn时间内维护修改和区间查询,注意下标从1开始

//计算i的二进制表示中，从右往左数，第一个1代表的数字
// lowbit(x) x的二进制为1100 return 4
int lowbit(int x) {
    return x & (-x);
}
//给第i个位置加上val
void update(int i, int val) {
    while (i <= n) {
        c[i] += val;
        i += lowbit(i);
    }
}
//从下标1-i的总和
int sum(int i) {
    int s = 0;
    while (i > 0) {
        s += c[i];
        i -= lowbit(i);
    }
    return s;
}

int main() {
    int t;
    cin>>t;
    for(int ct=1;ct<=t;ct++){
        cout<<"Case "<<ct<<":"<<endl;
        int val;
        cin>>n;
        memset(c,0,sizeof(c));
        for(int i=1;i<=n;i++){
            scanf("%d",&val);
            update(i,val);
        }
        char s[10];
        int x,y;
        while(~scanf("%s",s)){
            if(s[0]=='Q'){
                cin>>x>>y;
                cout<<sum(y)-sum(x-1)<<endl;
            }else if(s[0]=='A'){
                cin>>x>>y;
                update(x,y);
            }else if(s[0]=='S'){
                cin>>x>>y;
                update(x,y*-1);
            }else if(s[0]=='E'){
                break;
            }
        }
    }
    return 0;
}

```


























