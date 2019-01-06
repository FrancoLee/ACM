## Good_Bye_2018

---

[A](http://codeforces.com/contest/1091/problem/A)

​	题意:给定`r`,`y`,`b`,3种颜色的个数，找到一种选择方式使得，`y+1=b,b+1=r`,求最大能取多少个颜色。

​	分析：水题

```c++
#include <iostream>
#include <cstdio>
#include <string.h>
#include <algorithm>
#include <vector>
#include <deque>
#include <queue>
#include <map>
#include <iomanip>
#include <cmath>
#include <stack>
#include <set>
#include <regex>


typedef long long ll;
using namespace std;
const int MAXX = 1e9;
const int INF = 0x3f3f3f3f;
const int mod = 1e9;

int main() {
#ifdef acm
    freopen("input.txt", "r", stdin);
#endif
    int y,b,r;
    cin>>y>>b>>r;
    int ans=min(min(y,b-1),r-2);
    cout<<ans*3+3;
    return 0;
}
```

[B](http://codeforces.com/contest/1091/problem/B)

​	题意：`n`个位置和`n`个线索，一个位置配一个线索，问可能的宝藏位置。

​	分析：`n*(ansx,ansy)=(x1+af(1),y1+bf(1))+(x2+af(2),y2+af(2))....(xn+af(n),yn+bf(n))`,`f(x)`表示第`i`个位置对应的线索。加法满足交换和结合律，故只要把`n`个位置和`n`个线索的`(x,y)`值累加后`/n`就能得到宝藏位置。

```c++
#include <iostream>
#include <cstdio>
#include <string.h>
#include <algorithm>
#include <vector>
#include <deque>
#include <queue>
#include <map>
#include <iomanip>
#include <cmath>
#include <stack>
#include <set>
#include <regex>


typedef long long ll;
using namespace std;
const int MAXX = 1e9;
const int INF = 0x3f3f3f3f;
const int mod = 1e9;

int main() {
#ifdef acm
    freopen("input.txt", "r", stdin);
#endif
    ll x=0,y=0,n,t1,t2;
    cin>>n;
    for(int i=0;i<n;i++){
        cin>>t1>>t2;
        x+=t1;
        y+=t2;
    }
    for(int i=0;i<n;i++){
        cin>>t1>>t2;
        x+=t1;
        y+=t2;
    }
    cout<<x/n<<" "<<y/n;
}
```

[C](http://codeforces.com/contest/1091/problem/C)

​	题意：`n`个人围成一圈，让你选一个距离`x`，从当前位置走到经过`x`个的人的位置，起始从1开始，直到走回1。把停留的位置的下标累加起来，并输出。要求从小到大，并且无重无漏。

​	分析：看样例就能猜到是用因子当距离，知道距离再`O(1)`的计算累加值。记得要用N开方来做算法的上届，`O(N)`会超时。

```c++
#include <iostream>
#include <cstdio>
#include <string.h>
#include <algorithm>
#include <vector>
#include <deque>
#include <queue>
#include <map>
#include <iomanip>
#include <cmath>
#include <stack>
#include <set>
#include <regex>


typedef long long ll;
using namespace std;
const int MAXX = 1e9;
const int INF = 0x3f3f3f3f;
const int mod = 998244353;
vector<ll> arr;

int main() {
#ifdef acm
    freopen("input.txt", "r", stdin);
#endif
    ll n;
    cin >> n;
    int qn = sqrt(n);
    for (int i = 1; i <= qn; i++) {
        if (n % i == 0) {
            arr.push_back((n / i) * (2 + i * (n / i - 1)) / 2);
            int t=n/i;
            if(t==i)
                continue;
            arr.push_back((n / t) * (2 + t * (n / t - 1)) / 2);
        }
    }
    sort(arr.begin(),arr.end());
    for (int i = 0; i < arr.size(); i++) {
        cout << arr[i] << " ";
    }
    return 0;
}
```

[D](http://codeforces.com/contest/1091/problem/D)

​	题意：给你`1-n`个数的字典序，将所有字典序按顺序排列到一起。问你其中有多少个连续子集包含`1-n`的所有数。

​	分析：排列组合死推

```c++
#include <iostream>
#include <cstdio>
#include <string.h>
#include <algorithm>
#include <vector>
#include <deque>
#include <queue>
#include <map>
#include <iomanip>
#include <cmath>
#include <stack>
#include <set>
#include <regex>


typedef long long ll;
using namespace std;
const int MAXX = 1e9;
const int INF = 0x3f3f3f3f;
const int mod = 998244353;
ll arr[1000005];
ll brr[1000005];
int main() {
#ifdef acm
    freopen("input.txt", "r", stdin);
#endif
    int n;
    cin>>n;
    ll sum=1;
    for(int i=1;i<=n;i++){
        sum*=i;
        sum%=mod;
        arr[i]=sum;
    }
    brr[1]=brr[2]=0;
    brr[3]=3;
    for(int i=4;i<=n;i++){
        brr[i]=((brr[i-1]+arr[i-1]-1)%mod)*i%mod;
        brr[i]%=mod;
    }
    cout<<(arr[n]+brr[n])%mod;
}
```

