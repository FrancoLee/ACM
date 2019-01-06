## Vasya and Robot

---

[题目链接](http://codeforces.com/contest/1073/problem/C)

题目大意:给定一个移动序列,问从起点(0,0)到达目的(x,y)最小的改动间隔(最后次改动-第一次改动+1,不改动为0)的是多少

分析:

​	由于解空间是连续的,即存在一个最小改动间隔,在间隔点左边的修改间隔都无法到达终点,间隔点右边的修改间隔都能到达终点.故二分答案.

​	考虑一个修改间隔是否能到达终点,由于间隔内每个移动都能修改成任意方向,故只要判定当前位置(x,y)-(间隔内的移动)与目的相差的所需的移动数是否小于间隔长度.

​	为了快速计算当前位置,设px[i]表示第i次移动后对于起点(0,0)的x偏移,py[i]表示第i次移动后对于起点(0,0)的y偏移.那么当前位置就是(px[n],py[n]),减去间隔[i-j]内的移动后所在位置: **(px[n]-(px[j]-px[i-1]),py[n]-(py[j]+py[i-1]))** ,最比较(endx,endy)-(减去间隔后所在位置) <=len(间隔长度),为真表示能到.

​	最后要考虑到不了的情况:

 * 目的位置对于起点的偏移量大于总移动步数(步数不够,怎么改都走不到)

 * 移动后所在的位置和目的位置的偏移和是否是偶数,若是奇数则不可能到(因为修改一个方向必然会使得当前位置与修改前位置相差2的偏移量)	

   AC代码如下:

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
   
   #define INF 0x3f3f3f;
   #define esp 1e-8
   const int MAXX = 200005;
   using namespace std;
   int px[MAXX], py[MAXX];
   int n, endx, endy;
   char c[MAXX];
   int check(int len){
       for(int lo=1,hi=len;hi<=n;lo++,hi++){
           int xx=px[n]-(px[hi]-px[lo-1]);
           int yy=py[n]-(py[hi]-py[lo-1]);
       //    printf("%d %d\n",xx,yy);
           if((abs(endx-xx)+abs(endy-yy))<=len)
               return true;
       }
       return false;
   }
   int main() {
       scanf("%d",&n);
       scanf("%s",c);
       scanf("%d %d",&endx,&endy);
       for(int i=0;i<n;i++){
           px[i+1]=px[i];
           py[i+1]=py[i];
           if(c[i]=='R'){
               px[i+1]++;
           }else if(c[i]=='L'){
               px[i+1]--;
           }else if(c[i]=='U'){
               py[i+1]++;
           }else{
               py[i+1]--;
           }
       }
       if((abs(endx-px[n])+abs(endy-py[n]))%2!=0||(abs(endx)+abs(endy))>n){
           printf("-1\n");
           return 0;
       }
       int lo=0,hi=n,ans=-1;
       while(lo<=hi){
           int mid=(lo+hi)/2;
           if(check(mid)){
               hi=mid-1;
               ans=mid;
           }
           else {
               lo = mid+1;
           }
       }
       printf("%d\n",ans);
       return 0;
   }
   ```


