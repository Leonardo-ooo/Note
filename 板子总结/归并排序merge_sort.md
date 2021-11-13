// 归并排序

~~~c++
int a[N], tmp[N];
void m_sort(int l, int r){
    if(l >= r) return;
    int mid = l + r >> 1;
    m_sort(l, mid), m_sort(mid + 1, r);
    int i = l, j = mid + 1, k = 0;
    while(i <= mid && j <= r){
        if(a[i] <= a[j]) tmp[k++] = a[i++];
        else tmp[k++] = a[j++];
    }
    while(i<=mid) tmp[k++] = a[i++];
    while(j <= r) tmp[k++] = a[j++];
    for(int i = 0; i < k; i ++) a[l + i] = tmp[i];
}
~~~

