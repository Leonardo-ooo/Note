//Dijkstra(链式前向星)

~~~c++
int n; //n为顶点个数
struct edge{
    int to, ne, w;
}e[N];
int idx, h[505];
void add(int u, int v, int w){
    e[idx].to = v, e[idx].w = w, e[idx].ne = h[u], h[u] = idx++;
}
//以上为链式前向星建图
int d[505];
bool st[505];
void dijkstra(int x){	//Dijkstra求顶点x到其他点的最短路
    memset(d, 0x3f3f, sizeof d);	//初始化距离为无限
    d[x] = 0;	//初始化x到自身距离为0
    for(int i = 0; i < n - 1; i ++){
        int t = -1;		
        for(int j = 1; j <= n; j ++)	//找到当前距离最小的点t
            if(!st[j] && (t == -1 || d[t] > d[j])) t = j;
        st[t] = 1;		//t的最短路确定
        for(int j = h[t]; j != -1; j = e[j].ne)		//用t更新其他点的距离
            d[e[j].to] = min(d[e[j].to], d[t] + e[j].w);
    }
}
~~~

