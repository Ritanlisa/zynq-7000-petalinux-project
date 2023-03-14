# C++排序算法分析

## 插入排序
```C++
void insertSort(int arr[], int n) {
  for (int i = 1; i &lt; n; i++) {
    int key = arr[i];
    int j = i - 1;
    while (j &gt;= 0 && arr[j] &gt; key) {
      arr[j + 1] = arr[j];
      j--;
    }
  arr[j + 1] = key;
  }
}
```

## 折半插入排序
```C++
void binaryInsertSort(int a[], int n) {
  for (int i = 1; i &lt; n; ++i) {
    if (a[i - 1] &gt; a[i]) {
      int low = 0, high = i - 1;
      int x = a[i];
      while (low &lt;= high) {
        int mid = (low + high) / 2;
        if (a[mid] &gt; x)
          high = mid - 1;
        else
          low = mid + 1;
       }
     for (int j = i - 1; j &gt;= high + 1; --j)
     a[j + 1] = a[j];
     a[high + 1] = x;
     }
   }
}
```

## Shell排序
~~~ C++
void shellSort(int a[], int n) {
  int gap = n / 2;
  while (gap &gt; 0) {
    for (int i = gap; i &lt; n; i++) {
      int temp = a[i];
      int j = i - gap;
      while (j &gt;= 0 && a[j] &gt; temp) {
        a[j + gap] = a[j];
        j -= gap;
      }
      a[j + gap] = temp;
     }
  gap /= 2;
  }
}
~~~

## 选择排序
~~~ C++
void selectionSort(int arr[], int len) {
  for (int i = 0; i &lt; len - 1; i++) {
    int min = i;
    for (int j = i + 1; j &lt; len; j++)
    if (arr[min] &gt; arr[j])
      min = j;
    int temp = arr[min];
  arr[min] = arr[i];
  arr[i] = temp;
  }
}
~~~
