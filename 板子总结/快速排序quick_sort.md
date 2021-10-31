// 快速排序quick_sort

~~~c++
int q[N]
void q_sort(int q[], int l, int r){
    if(l >= r) return;
    int i = l - 1, j = r + 1, x = q[l + r >> 1];
    while(i < j){
        do i++; while(q[i] < x);
        do j--; while(q[j] > x);
        if(i < j) swap(q[i], q[j]);
    }
    q_sort(q, l, j), q_sort(q, j + 1, r);
}
~~~

