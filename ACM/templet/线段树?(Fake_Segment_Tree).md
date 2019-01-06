## 线段树("Fake" Segment Tree)

----

[题目链接](http://acm.hdu.edu.cn/showproblem.php?pid=1754) 区间最小模板题

线段树是一个区间查询,修改logN,建树N的一个数据结构.

### 建树:

```
int m[MAXX<<2];//区间要开规模的4倍
void inline pushup(int x) {
    m[x] = max(m[x << 1], m[x << 1 | 1]);//更新节点(区间)最值,可以改成求和,最小
}

void build(int l, int r, int rt) {
//[l,r]表示当前节点的区间,rt表示当前节点的实际存储位置(从树的角度看rt是从树根节点层次遍历的值)
    if (l == r) {
        scanf("%d", &m[rt]);
        return;
    }
    int m = (l + r) >> 1;
    build(l, m, rt << 1);
    build(m + 1, r, rt << 1 | 1);
    pushup(rt);//左右儿子建立好了,维护最值
}
//build(1,n,1); n为区间大小 范围[1-n] 建树
```

### 更新:

```
void update(int index, int val, int l, int r, int rt) {
//[l,r]表示当前区间,rt表示当前区间编号,index表示要修改的位置,val是要改成的数值
    if (l == r) {
        m[rt] = val;
        return;
    }
    int m = (l + r) >> 1;
    if (index <= m)//判断目标位置在当前区间的做还是右
        update(index, val, l, m, rt << 1);
    else
        update(index, val, m + 1, r, rt << 1 | 1);
    pushup(rt);//维护最值
}
//update(a, b, 1, n, 1);更新下标a的值为b
```

### 查询:

```

int query(int L, int R, int l, int r, int rt) {//L,R为要查询的区间,[l,r]当前区间
    if (L <= l && r <= R) {//在区间内直接返回
        return m[rt];
    }
    int m = (l + r) >> 1;
    int m1 = 0, m2 = 0;
    if (L <= m)
        m1 = query(L, R, l, m, rt << 1);
    if (R > m)
        m2 = query(L, R, m + 1, r, rt << 1 | 1);
    return max(m1, m2);
}
//query(a, b, 1, n, 1); 查询a-b区间的最值
```

