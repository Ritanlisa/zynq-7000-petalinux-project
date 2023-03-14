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

## 冒泡排序
~~~ C++
void bubbleSort(int a[], int n) {
  for (int i = 0; i &lt; n - 1; i++) {
    for (int j = 0; j &lt; n - i - 1; j++) {
      if (a[j] &gt; a[j + 1]) {
        int temp = a[j];
        a[j] = a[j + 1];
        a[j + 1] = temp;
      }
    }
  }
}
~~~

## 树形选择排序
~~~ C++
void treeSelectionSort(int arr[], int n) {
  int *tree = new int[2 * n - 1]; // 构建一个完全二叉树，用数组存储
  for (int i = n - 1; i &lt; 2 * n - 1; i++) { // 将数组元素放入叶子节点
    tree[i] = arr[i - (n - 1)];
  }
  for (int k = n - 2; k &gt;= 0; k--) { // 自底向上构建初始树
    tree[k] = min(tree[2 * k + 1], tree[2 * k + 2]); // 父节点为左右子节点中较小者
  }
  for (int j = 0; j &lt; n; j++) { // 进行n次选择，每次选出最小值放入结果数组
    arr[j] = tree[0]; // 最小值为根节点
    int index;
    for (index = n - 1; index &lt; 2 * n - 1 && tree[index] != arr[j]; index++); // 找到最小值所在的叶子节点索引
    tree[index] = INT_MAX; // 将该叶子节点置为无穷大，表示已经被选过
    while ((index - 1) / 2 &gt;=0) { // 自底向上更新父节点的值，保持最小值在根节点
      index = (index - 1) / 2;
      tree[index] = min(tree[2 * index + 1], tree[2 * index + 2]);
    }
  }
}
~~~

## 快速排序
~~~ C++
void quickSort(int a[], int left, int right) {
  if (left &gt;= right) return; // 递归终止条件
    int i = left; // 左指针
    int j = right; // 右指针
    int key = a[left]; // 基准值，一般取左边第一个元素
    while (i &lt; j) { // 当左右指针未相遇时循环
      while (i &lt; j && a[j] &gt;= key) j--; // 从右向左找到第一个小于基准值的元素
      a[i] = a[j]; // 将该元素放到左边空位上
      while (i &lt; j && a[i] &lt;= key) i++; // 从左向右找到第一个大于基准值的元素
      a[j] = a[i]; // 将该元素放到右边空位上
    }
  a[i] = key; // 将基准值放到最终位置上
  quickSort(a, left, i - 1); // 对左半部分递归排序
  quickSort(a, i + 1, right); // 对右半部分递归排序
}
~~~

## 归并排序
~~~ C++
void merge(int arr[], int left, int mid, int right) { // 合并两个有序数组的函数，left和mid为第一个数组的起止索引，mid+1和right为第二个数组的起止索引
  int *temp = new int[right - left + 1]; // 创建一个临时数组，用来存储合并后的结果
  int i = left; // 第一个数组的起始位置
  int j = mid + 1; // 第二个数组的起始位置
  int k = 0; // 临时数组的起始位置
  while (i &lt;= mid && j &lt;= right) { // 当两个数组都有剩余元素时，比较大小并放入临时数组中
    if (arr[i] &lt;= arr[j]) {
      temp[k++] = arr[i++];
    } else {
      temp[k++] = arr[j++];
    }
  }
  while (i &lt;= mid) { // 当第一个数组有剩余元素时，直接放入临时数组中
    temp[k++] = arr[i++];
  }
  while (j &lt;= right) { // 当第二个数组有剩余元素时，直接放入临时数组中 
    temp[k++] = arr[j++];
  }
  for (int p = 0; p &lt; k; p++) { // 将临时数组中的结果复制回原始数组中 
    arr[left + p] = temp[p];
  }
}

void mergeSort(int arr[], int left, int right) { 
  // 归并排序函数，left和right为待排序区间的起止索引 
  if (left == right) return; // 如果left==right，则表示区间只有一个元素，无需排序 
  int mid = (left + right) / 2; // 否则将区间分成两部分，分别进行归并排序，然后合并 
  mergeSort(arr, left, mid);
  mergeSort(arr, mid + 1, right);
  merge(arr, left, mid ,right);
}
~~~
| 排序算法 | 平均时间复杂度 | 最好时间复杂度 | 最坏时间复杂度 |
| :------: | :------------: | :------------: | :------------: |
| 插入排序 |    O(n^2)     |     O(n)      |    O(n^2)     |
| 折半排序|    O(n^2)    |    O(nlogn)   |    O(n^2)       |
| shell排序 |  O(nlogn)~O(n^2)|   O(nlogn)   |   O(n^2logn)  |
| 选择排序 |    O(n^2)     |    O(n^2)     |    O(n^2)     |
| 冒泡排序 |    O(n^2)     |     O(n)      |    O(n^2)     |
| 树形选择排序|    O (n)   |   O (n)    |  O (n)      |
| 快速排序 |   O(nlogn)   |   O(nlogn)   |    O(n^2)     |
| 归并排序 |   O(nlogn)   |   O(nlogn)   |   O(nlogn)   |
