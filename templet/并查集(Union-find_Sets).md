## 并查集

---

用于快速合并集合,判断某个元素是否属于某个集合

```
int find(int x) {
    int p, tmp;
    p = x;
    while (x != pre[x]) x = pre[x];
    //路径压缩
    while (p != x) {
        tmp = pre[p];
        pre[p] = x;
        p = tmp;
    }
    return x;
}
//合并x和y所在的集合 并选x的根为集合的代表元素(根元素)
void join(int x, int y) {
    int fx = find(x);
    int fy = find(y);
    if (fx != fy) pre[fy] = fx;
}
//判断x和y是否在同一个集合
bool Same(int x, int y) { return find(x) == find(y); }

//初始化,[0,r)
void init(int r){
    for(int i=0;i<r;i++){
        pre[i]=i;
    }
}
```

