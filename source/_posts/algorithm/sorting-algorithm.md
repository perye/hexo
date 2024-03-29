---
title: 十大经典排序算法动画与解析
toc: true
mathjax: false
summary: 插入排序、希尔排序、选择排序、冒泡排序、归并排序、快速排序、堆排序、基数排序
categories: 算法
tags:
  - 算法
  - 排序
abbrlink: '88664517'
date: 2020-11-05 14:02:23
author:
img:
coverImg:
password:
---

## 排序算法

排序算法是《数据结构与算法》中最基本的算法之一。

排序算法可以分为内部排序和外部排序。

内部排序是数据记录在内存中进行排序。

而外部排序是因排序的数据很大，一次不能容纳全部的排序记录，在排序过程中需要访问外存。

常见的内部排序算法有：插入排序、希尔排序、选择排序、冒泡排序、归并排序、快速排序、堆排序、基数排序等。

![时间复杂度与空间复杂度](https://perye.oss-cn-shenzhen.aliyuncs.com/blog/algorithm/%E6%97%B6%E9%97%B4%E5%A4%8D%E6%9D%82%E5%BA%A6%E4%B8%8E%E7%A9%BA%E9%97%B4%E5%A4%8D%E6%9D%82%E5%BA%A6.png)

**关于时间复杂度**
1. 平方阶 (O(n<sup>2</sup>)) 排序 各类简单排序：直接插入、直接选择和冒泡排序。
2. 线性对数阶 (O(nlog<sub>2</sub>n)) 排序 快速排序、堆排序和归并排序；
3. O(n1+§)) 排序，§ 是介于 0 和 1 之间的常数。 希尔排序
4. 线性阶 (O(n)) 排序 基数排序，此外还有桶、箱排序。

**关于稳定性** 
1. 稳定的排序算法：冒泡排序、插入排序、归并排序和基数排序。
2. 不是稳定的排序算法：选择排序、快速排序、希尔排序、堆排序。

## 冒泡排序

### 算法步骤

- 比较相邻的元素。如果第一个比第二个大，就交换他们两个。
- 对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对。这步做完后，最后的元素会是最大的数。
- 针对所有的元素重复以上的步骤，除了最后一个。
- 持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较。
  
### 动画演示
![冒泡排序动画演示](https://perye.oss-cn-shenzhen.aliyuncs.com/blog/algorithm/%E5%86%92%E6%B3%A1%E6%8E%92%E5%BA%8F%E5%8A%A8%E7%94%BB%E6%BC%94%E7%A4%BA.gif)

### 参考代码
```java
public class BubbleSort {
    public int[] sort(int[] sourceArray) {
        // 对 arr 进行拷贝，不改变参数内容
        int[] arr = Arrays.copyOf(sourceArray, sourceArray.length);
        for (int i = 0; i < arr.length - 1; i++) {
            // 设定一个标记，若为true，则表示此次循环没有进行交换，也就是待排序列已经有序，排序已经完成。
            boolean flag = true;
            for (int j = 0; j < arr.length - 1 - i; j++) {
                if (arr[j] > arr[j + 1]) {
                    int tmp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = tmp;
                    flag = false;
                }
            }
            if (flag) {
                break;
            }
        }
        return arr;
    }
}
```

## 选择排序
### 算法步骤
- 首先在未排序序列中找到最小（大）元素，存放到排序序列的起始位置
- 再从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序序列的末尾。
- 重复第二步，直到所有元素均排序完毕。

### 动画演示
![选择排序动画演示](https://perye.oss-cn-shenzhen.aliyuncs.com/blog/algorithm/%E9%80%89%E6%8B%A9%E6%8E%92%E5%BA%8F%E5%8A%A8%E7%94%BB%E6%BC%94%E7%A4%BA.gif)

### 参考代码
```java
public class SelectionSort {
    public int[] sort(int[] sourceArray) {
        // 对 arr 进行拷贝，不改变参数内容
        int[] arr = Arrays.copyOf(sourceArray, sourceArray.length);
        // 总共要经过 N-1 轮比较
        for (int i = 0; i < arr.length - 1; i++) {
            int min = i;
            // 每轮需要比较的次数 N-i
            for (int j = i + 1; j < arr.length; j++) {
                if (arr[j] < arr[min]) {
                    // 记录目前能找到的最小值元素的下标
                    min = j;
                }
            }
            // 将找到的最小值和i位置所在的值进行交换
            if (i != min) {
                int tmp = arr[i];
                arr[i] = arr[min];
                arr[min] = tmp;
            }
        }
        return arr;
    }
}
```
## 插入排序
### 算法步骤
- 将第一待排序序列第一个元素看做一个有序序列，把第二个元素到最后一个元素当成是未排序序列。
- 从头到尾依次扫描未排序序列，将扫描到的每个元素插入有序序列的适当位置。（如果待插入的元素与有序序列中的某个元素相等，则将待插入元素插入到相等元素的后面。）

### 动画演示
![插入排序动画演示](https://perye.oss-cn-shenzhen.aliyuncs.com/blog/algorithm/%E6%8F%92%E5%85%A5%E6%8E%92%E5%BA%8F%E5%8A%A8%E7%94%BB%E6%BC%94%E7%A4%BA.gif)

### 参考代码
```java
public class InsertSort {
    public int[] sort(int[] sourceArray) {
        // 对 arr 进行拷贝，不改变参数内容
        int[] arr = Arrays.copyOf(sourceArray, sourceArray.length);
        // 从下标为1的元素开始选择合适的位置插入，因为下标为0的只有一个元素，默认是有序的
        for (int i = 1; i < arr.length; i++) {
            // 记录要插入的数据
            int tmp = arr[i];
            // 从已经排序的序列最右边的开始比较，找到比其小的数
            int j = i;
            while (j > 0 && tmp < arr[j - 1]) {
                arr[j] = arr[j - 1];
                j--;
            }
            // 存在比其小的数，插入
            if (j != i) {
                arr[j] = tmp;
            }
        }
        return arr;
    }
}
```

## 希尔排序
### 算法步骤
- 选择一个增量序列 t<sub>1</sub>，t<sub>2</sub>，……，t<sub>k</sub>，其中 t<sub>i</sub> > t<sub>j</sub>, t<sub>k</sub> = 1；
- 按增量序列个数 k，对序列进行 k 趟排序；
- 每趟排序，根据对应的增量 t<sub>i</sub>，将待排序列分割成若干长度为 m 的子序列，分别对各子表进行直接插入排序。仅增量因子为 1 时，整个序列作为一个表来处理，表长度即为整个序列的长度。

### 动画演示
![希尔排序动画演示](https://perye.oss-cn-shenzhen.aliyuncs.com/blog/algorithm/%E5%B8%8C%E5%B0%94%E6%8E%92%E5%BA%8F%E5%8A%A8%E7%94%BB%E6%BC%94%E7%A4%BA.gif)
###  参考代码
```java
public class ShellSort {
    public static int[] sort(int[] sourceArray) {
        // 对 arr 进行拷贝，不改变参数内容
        int[] arr = Arrays.copyOf(sourceArray, sourceArray.length);
        int gap = 1;
        while (gap < arr.length) {
            gap = gap * 3 + 1;
        }
        while (gap > 0) {
            for (int i = gap; i < arr.length; i++) {
                int tmp = arr[i];
                int j = i - gap;
                while (j >= 0 && arr[j] > tmp) {
                    arr[j + gap] = arr[j];
                    j -= gap;
                }
                arr[j + gap] = tmp;
            }
            gap = gap / 3;
        }
        return arr;
    }
}
```
## 归并排序
### 算法步骤
- 申请空间，使其大小为两个已经排序序列之和，该空间用来存放合并后的序列；
- 设定两个指针，最初位置分别为两个已经排序序列的起始位置；
- 比较两个指针所指向的元素，选择相对小的元素放入到合并空间，并移动指针到下一位置；
- 重复步骤 3 直到某一指针达到序列尾；
- 将另一序列剩下的所有元素直接复制到合并序列尾。
  
### 动画演示
![归并排序动画演示](https://perye.oss-cn-shenzhen.aliyuncs.com/blog/algorithm/%E5%BD%92%E5%B9%B6%E6%8E%92%E5%BA%8F%E5%8A%A8%E7%94%BB%E6%BC%94%E7%A4%BA.gif)

### 参考代码
```java
public class MergeSort {
    public int[] sort(int[] sourceArray) {
        // 对 arr 进行拷贝，不改变参数内容
        int[] arr = Arrays.copyOf(sourceArray, sourceArray.length);
        if (arr.length < 2) {
            return arr;
        }
        int middle = arr.length / 2;
        int[] left = Arrays.copyOfRange(arr, 0, middle);
        int[] right = Arrays.copyOfRange(arr, middle, arr.length);
        return merge(sort(left), sort(right));
    }
    protected int[] merge(int[] left, int[] right) {
        int[] result = new int[left.length + right.length];
        int i = 0;
        while (left.length > 0 && right.length > 0) {
            if (left[0] <= right[0]) {
                result[i++] = left[0];
                left = Arrays.copyOfRange(left, 1, left.length);
            } else {
                result[i++] = right[0];
                right = Arrays.copyOfRange(right, 1, right.length);
            }
        }
        while (left.length > 0) {
            result[i++] = left[0];
            left = Arrays.copyOfRange(left, 1, left.length);
        }
        while (right.length > 0) {
            result[i++] = right[0];
            right = Arrays.copyOfRange(right, 1, right.length);
        }
        return result;
    }
}
```

## 快速排序
### 算法步骤
- 从数列中挑出一个元素，称为 “基准”（pivot）;
- 重新排序数列，所有元素比基准值小的摆放在基准前面，所有元素比基准值大的摆在基准的后面（相同的数可以到任一边）。在这个分区退出之后，该基准就处于数列的中间位置。这个称为分区（partition）操作；
- 递归地（recursive）把小于基准值元素的子数列和大于基准值元素的子数列排序；

### 动画演示
![快速排序动画演示](https://perye.oss-cn-shenzhen.aliyuncs.com/blog/algorithm/%E5%BF%AB%E9%80%9F%E6%8E%92%E5%BA%8F%E5%8A%A8%E7%94%BB%E6%BC%94%E7%A4%BA.gif)
### 参考代码
```java
public class QuickSort {
    public int[] sort(int[] sourceArray) {
        // 对 arr 进行拷贝，不改变参数内容
        int[] arr = Arrays.copyOf(sourceArray, sourceArray.length);
        return quickSort(arr, 0, arr.length - 1);
    }
    private int[] quickSort(int[] arr, int left, int right) {
        if (left < right) {
            int partitionIndex = partition(arr, left, right);
            quickSort(arr, left, partitionIndex - 1);
            quickSort(arr, partitionIndex + 1, right);
        }
        return arr;
    }
    private int partition(int[] arr, int left, int right) {
        // 设定基准值（pivot）
        int index = left + 1;
        for (int i = index; i <= right; i++) {
            if (arr[i] < arr[left]) {
                swap(arr, i, index);
                index++;
            }
        }
        swap(arr, left, index - 1);
        return index - 1;
    }
    private void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
```

## 堆排序
### 算法步骤
- 创建一个堆 H[0……n-1]；
- 把堆首（最大值）和堆尾互换；
- 把堆的尺寸缩小 1，并调用 shift_down(0)，目的是把新的数组顶端数据调整到相应位置；
- 重复步骤 2，直到堆的尺寸为 1。
### 动画演示
![堆排序动画演示](https://perye.oss-cn-shenzhen.aliyuncs.com/blog/algorithm/%E5%A0%86%E6%8E%92%E5%BA%8F%E5%8A%A8%E7%94%BB%E6%BC%94%E7%A4%BA.gif)
### 参考代码
```java
public class HeapSort  {
    public int[] sort(int[] sourceArray) {
        // 对 arr 进行拷贝，不改变参数内容
        int[] arr = Arrays.copyOf(sourceArray, sourceArray.length);
        int len = arr.length;
        buildMaxHeap(arr, len);
        for (int i = len - 1; i > 0; i--) {
            swap(arr, 0, i);
            len--;
            heapify(arr, 0, len);
        }
        return arr;
    }

    private void buildMaxHeap(int[] arr, int len) {
        for (int i = len / 2; i >= 0; i--) {
            heapify(arr, i, len);
        }
    }

    private void heapify(int[] arr, int i, int len) {
        int left = 2 * i + 1;
        int right = 2 * i + 2;
        int largest = i;
        if (left < len && arr[left] > arr[largest]) {
            largest = left;
        }
        if (right < len && arr[right] > arr[largest]) {
            largest = right;
        }
        if (largest != i) {
            swap(arr, i, largest);
            heapify(arr, largest, len);
        }
    }

    private void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
```

## 计数排序

### 算法步骤
- 花O(n)的时间扫描一下整个序列 A，获取最小值 min 和最大值 max
- 开辟一块新的空间创建新的数组 B，长度为 ( max - min + 1)
- 数组 B 中 index 的元素记录的值是 A 中某元素出现的次数
- 最后输出目标整数序列，具体的逻辑是遍历数组 B，输出相应元素以及对应的个数
### 动画演示
![计数排序动画演示](https://perye.oss-cn-shenzhen.aliyuncs.com/blog/algorithm/%E8%AE%A1%E6%95%B0%E6%8E%92%E5%BA%8F%E5%8A%A8%E7%94%BB%E6%BC%94%E7%A4%BA.gif)
### 参考代码
```java
public class CountingSort {
    public int[] sort(int[] sourceArray) {
        // 对 arr 进行拷贝，不改变参数内容
        int[] arr = Arrays.copyOf(sourceArray, sourceArray.length);
        int maxValue = getMaxValue(arr);
        return countingSort(arr, maxValue);
    }

    private int[] countingSort(int[] arr, int maxValue) {
        int bucketLen = maxValue + 1;
        int[] bucket = new int[bucketLen];
        for (int value : arr) {
            bucket[value]++;
        }
        int sortedIndex = 0;
        for (int j = 0; j < bucketLen; j++) {
            while (bucket[j] > 0) {
                arr[sortedIndex++] = j;
                bucket[j]--;
            }
        }
        return arr;
    }

    private int getMaxValue(int[] arr) {
        int maxValue = arr[0];
        for (int value : arr) {
            if (maxValue < value) {
                maxValue = value;
            }
        }
        return maxValue;
    }
}
```

## 桶排序

### 算法步骤
- 设置固定数量的空桶。
- 把数据放到对应的桶中。
- 对每个不为空的桶中数据进行排序。
- 拼接不为空的桶中数据，得到结果
### 动画演示
![桶排序动画演示](https://perye.oss-cn-shenzhen.aliyuncs.com/blog/algorithm/%E6%A1%B6%E6%8E%92%E5%BA%8F%E5%8A%A8%E7%94%BB%E6%BC%94%E7%A4%BA.gif)

### 参考代码
```java
public class BucketSort {
    public int[] sort(int[] sourceArray) {
      // 对 arr 进行拷贝，不改变参数内容
      int[] arr = Arrays.copyOf(sourceArray, sourceArray.length);
      return bucketSort(arr, 5);
    }
    private int[] bucketSort(int[] arr, int bucketSize) {
        if (arr.length == 0) {
            return arr;
        }
        int minValue = arr[0];
        int maxValue = arr[0];
        for (int value : arr) {
            if (value < minValue) {
                minValue = value;
            } else if (value > maxValue) {
                maxValue = value;
            }
        }
        int bucketCount = (maxValue - minValue) / bucketSize + 1;
        int[][] buckets = new int[bucketCount][0];
        // 利用映射函数将数据分配到各个桶中
        for (int i = 0; i < arr.length; i++) {
            int index = (arr[i] - minValue) / bucketSize;
            buckets[index] = arrAppend(buckets[index], arr[i]);
        }
        int arrIndex = 0;
        for (int[] bucket : buckets) {
            if (bucket.length <= 0) {
                continue;
            }
            // 对每个桶进行排序，这里使用了插入排序
            bucket = insertSort.sort(bucket);
            for (int value : bucket) {
                arr[arrIndex++] = value;
            }
        }
        return arr;
    }
    /**
    * 自动扩容，并保存数据
    */
    private int[] arrAppend(int[] arr, int value) {
        arr = Arrays.copyOf(arr, arr.length + 1);
        arr[arr.length - 1] = value;
        return arr;
    }
}
```

## 基数排序
### 算法步骤
- 将所有待比较数值（正整数）统一为同样的数位长度，数位较短的数前面补零
- 从最低位开始，依次进行一次排序
- 从最低位排序一直到最高位排序完成以后, 数列就变成一个有序序列
 
### 动画演示
![基数排序动画演示](https://perye.oss-cn-shenzhen.aliyuncs.com/blog/algorithm/%E5%9F%BA%E6%95%B0%E6%8E%92%E5%BA%8F%E5%8A%A8%E7%94%BB%E6%BC%94%E7%A4%BA.gif)

### 参考代码
```java
public class RadixSort {
    public int[] sort(int[] sourceArray) {
      // 对 arr 进行拷贝，不改变参数内容
      int[] arr = Arrays.copyOf(sourceArray, sourceArray.length);
      int maxDigit = getMaxDigit(arr);
      return radixSort(arr, maxDigit);
    }
    /**
    * 获取最高位数
    */
    private int getMaxDigit(int[] arr) {
      int maxValue = getMaxValue(arr);
      return getNumLenght(maxValue);   
    }
    private int getMaxValue(int[] arr) {
        int maxValue = arr[0];
        for (int value : arr) {
            if (maxValue < value) {
                maxValue = value;
            }
        }
        return maxValue;
    }
    protected int getNumLenght(long num) {
        if (num == 0) {
            return 1;
        }
        int lenght = 0;
        for (long temp = num; temp != 0; temp /= 10) {
            lenght++;
        }
        return lenght;
    }
    private int[] radixSort(int[] arr, int maxDigit) {
        int mod = 10;
        int dev = 1;
        for (int i = 0; i < maxDigit; i++, dev *= 10, mod *= 10) {
            // 考虑负数的情况，这里扩展一倍队列数，其中 [0-9]对应负数，[10-19]对应正数 (bucket + 10)
            int[][] counter = new int[mod * 2][0];
            for (int j = 0; j < arr.length; j++) {
                int bucket = ((arr[j] % mod) / dev) + mod;
                counter[bucket] = arrayAppend(counter[bucket], arr[j]);
            }
            int pos = 0;
            for (int[] bucket : counter) {
                for (int value : bucket) {
                    arr[pos++] = value;
                }
            }
        }
        return arr;
    }
    private int[] arrayAppend(int[] arr, int value) {
        arr = Arrays.copyOf(arr, arr.length + 1);
        arr[arr.length - 1] = value;
        return arr;
    }
    
}
```