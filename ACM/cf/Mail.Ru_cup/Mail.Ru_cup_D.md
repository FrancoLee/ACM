## Changing Array

---

[题目链接](http://codeforces.com/contest/1054/problem/D)

​	题意：给N个数，范围在K以内，可以对每个的数的每一位取反或者不进行操作，问最多的段（连续且将每个数异或的结果不为0）.

​	思路：求连续不为0的段不好求，转换问题为求最少连续异或结果0的段个数。用总段数减去最少连续异或为0的段就是最多连续不为0的个数。将一个不熟悉的问题转成自己熟悉的问题很重要！ 

​	求连续异或结果为0的段，从第一个数开始异或，若异或后的结果X在之前出现过，说明当前位置i到之前出现过结果为X的位置，这一段连续异或的结果为0.由于每次可以选择对每个位取反或者不取反，取反就等于异或b=2^k-1,异或满足结合律和交换率(这很重要),所以a[i]^b^a[i+1]^b=a[i]^a[i+1],取反2次等于没取反，所以每次只要计算a[1]^a[2]^..^a[n]^K与a[1]^a[2]^..^a[n]的值就行了。

---

AC代码：

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
map<int, int> m;

int main() {

    int k, t, x, pre = 0;
    long long n;
    cin >> n >> k;
    x = (1 << k) - 1;
    m[0] = 1;
    long long ans = 0;
    for (int i = 0; i < n; i++) {
        cin >> t;
        pre ^= t;
        if (m[pre ^ x] < m[pre]) {
            ans += m[pre ^ x];
            m[pre ^ x]++;
        } else {
            ans += m[pre];
            m[pre]++;
        }
    }
    cout << (n * n + n) / 2 - ans << endl;
    return 0;
}

```

