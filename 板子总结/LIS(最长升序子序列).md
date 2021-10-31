//	LIS(最长升序子序列)

```c++
// lower_bound(q, q + len, val); 返回非递减序列q到q + len的第一个大于等于val的元素的迭代器
// upper_bound(q, q + len, val); 返回非递减序列q到q + len的第一个大于val的元素的迭代器
int n, a[1005], idx ;
int lis(){
    for(int i = 0; i < n; i ++)
    if(idx == 0 ||a[i] > a[idx - 1]) a[idx++] = a[i];
    else *lower_bound(a , a + idx , a[i]) = a[i];
    return idx;
}
```

// 手动二分版

```c++
int lis(){
    for(int i = 0; i < n; i ++)
    if(idx == 0 ||a[i] > a[idx - 1]) a[idx++] = a[i];
    else {
        int l = 0, r = idx;
        while(l < r){
            int mid = l + r >> 1;
            if(a[mid] >= a[i]) r = mid;
            else l = mid + 1;
        }
        a[r] = a[i];
    }
    return idx;
}
```

