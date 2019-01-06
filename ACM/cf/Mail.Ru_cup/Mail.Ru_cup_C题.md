# Mail.Ru cup C题

---

[题目链接]（http://codeforces.com/contest/1054/problem/C）

​	题目大意：老师给N个学生分糖果，分完后告诉你每个学生左右两边有多少人的糖果比当前学生多。问是否存在一种分法使之成立。若存在输出一种分法。

​	思路：就1000个学生，暴力！a[i]:学生i左边人数,b[i]:学生i右边人数,每次找到左右两边糖果都少于自己的学生(a[i]=bi[i]=0)，然后将i的左边学生的b[j]-1，右边学生的b[j]-1;若所有学生最后都的b[i]=a[i]=0,则存在一种分法。分法只要标记每次循环找到的a[i]=b[i]=0，越早循环找到的分得的糖果越多。

### ac代码如下：

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
#include <stack>

#define esp 1e-8
using namespace std;
int a[1005], b[1005];
int c[1005];
bool vis[1005];
vector<int> arr;

int main() {
    int n;
    cin>>n;
    for (int i = 0; i < n; i++) {
        cin >> a[i];
    }
    for (int i = 0; i < n; i++) {
        cin >> b[i];
    }
    memset(vis, false, sizeof(vis));
    int index = 0, cnt = 0;
    while (cnt < n) {
        bool flag = false;
        arr.clear();
        for (int i = 0; i < n; i++) {
            if (!vis[i] && a[i] == 0 && b[i] == 0) {
                c[i] = index;
                arr.push_back(i);
                vis[i] = true;
                flag = true;
                cnt++;
            }
        }
        if (!flag){
            break;
        }
        index++;
        for (int i = 0; i < arr.size(); i++) {
            for (int j = 0; j < arr[i]; j++) {
                if (!vis[j])
                    b[j]--;
            }
            for (int j = arr[i] + 1; j < n; j++) {
                if (!vis[j])
                    a[j]--;
            }
        }
    }
    if(cnt<n){
        cout<<"NO";
    }
    else{
        cout<<"YES"<<endl;
        for(int i=0;i<n;i++){
            cout<<index-c[i]<<" ";
        }
    }
    return 0;
}
```

