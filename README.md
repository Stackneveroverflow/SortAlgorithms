九大排序算法总结
====
**排序算法，看的是《数据结构与算法分析（Java描述版）(第四版)》，与C描述版还是有些不一样的地方.**

- 插入排序
    > **直接插入排序**
    > **希尔排序**
- 选择排序
    > **直接选择排序**
    > **堆排序**
- 交换排序
    > **冒泡排序**
    > **快速排序**
- **归并排序**
- **基数排序**
- **外部排序**
****	

####多种排序算法集合
为什么快排在实际使用中通常优于堆排序？
局部性原理，越靠近的数据比较和交换用时越少，而且CPU的Cache中缓存了最近频繁读写的数据。
在堆排中，每一个操作都是不利于程序的局部性原理的，每次元素间的比较、数的调整等，
最大堆调整每次都从堆底拿元素换到堆顶然后又下滤下去，在堆底一般都比较小，很大可能再次下滤到底层，
这个过程做了很多无用功，需要不断地跨度大地读写数据。
反观快速排序和归并排序，利用分而治之的方法，元素间的比较都在某个段内，操作比较集中，局部性相当好。

**测试效果**：`快排`<`归并`<`堆排`<`希尔`<<<`插入`<`选择`<`冒泡`

* **Simple insertion sort 直接插入排序**
每步将一个待排序的元素，按大小插入前面已经排序的序列中适当位置上，直到全部插入完为止 `时间复杂度O(n^2)，空间复杂度O(1)，稳定`
> 适用场合：数据量不大，对算法的稳定性有要求，且数据局部或者整体有序的情况，小规模如10个数平均时间最快，可以在快排中调用

* **ShellSort 希尔排序** 
是插入排序的一种又称"缩小增量排序"（Diminishing Increment Sort） 使用简单的希尔增量序列，复杂的增量序列中Sedgewick 增量序列最坏时间复杂度达到O(n^1.3) `时间复杂度取决于增量序列，空间复杂度O(1)，不稳定！！！` 
>适用场合：数据量较大，不要求稳定性

* **SelectionSort 直接选择排序**
 每一次从待排序的数据元素中选出最小的一个元素，存放在序列的起始位置，直到全部待排序的数据元素排完 `时间复杂度O(n^2)，空间复杂度O(1)，不稳定`
 > 适用场合：当数据量不大，且对稳定性没有要求的时候

* **HeapSort 堆排序**
 升序 用最大堆 它是选择排序的一种。可以利用数组的特点快速定位指定索引的元素。 `时间复杂度O(n log n)，空间复杂度O(1)，不稳定` 
 >适用场合：数据量较大，且对稳定性无要求，不如用快排或归并，但取前几个最值时可以不用排序完，奇效

* **BubbleSort 冒泡排序**
 重复地走访过要排序的数列，一次比较两个元素，如果他们的顺序错误就把他们交换过来 `时间复杂度O(n^2)，空间复杂度O(1)，稳定`
 > 适用场合：数据量量不大，对稳定性有要求，且数据基本有序的情况下

* **QuickSort 快速排序**
是对冒泡排序的一种改进。通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。`时间复杂度O(n log n)，空间复杂度O(n log n)，不稳定`，选好枢纽元是使坏情况发生的关键截断范围选10比较合适，进入截断范围改用小规模高效率算法对小片段排序 
>适用场合：数值范围较大，相同值的概率较小，数据量大且不考虑稳定性的情况，数值远大于数据量时威力更大

 * **MergeSort 归并排序**
  比较次数最少，Arrays.sort()调用该算法 `时间复杂度O(n log n)，空间复杂度O(n)，稳定！！！`
  >适用场合：数据规模较大，对稳定性有要求，一般用于总体无序，但是各子项相对有序的数列

* **CountingRadixSort 计数基数排序**
 线性时间复杂度 基数排序（radix sort）属于“分配式排序”（distribution sort），又称“桶子法”（bucket sort） 最高位优先法 MSD 和最低位优先 LSD，d个关键码，n个数据，r是基数 LSD的基数排序适用于位数小的数列，如果位数多的话，使用MSD的效率会比较好。MSD的方式与LSD相反， 是由高位数为基底开始进行分配，但在分配之后并不马上合并回一个数组中，而是在每个“桶子”中建立“子桶”， 将每个桶子中的数值按照下一数位的值分配到“子桶”中。在进行完最低位数的分配后再合并回单一的数组中。 `时间复杂度O(d(r+n))，空间复杂度O(rd+n)，稳定`
 > 适用场合：数值都是非负整数，且范围较小的情况，尤其适用于256位的ASCII码，用作字符串的字典顺序排序

* **外部排序**
 用了归并算法的思路 在主存中最大限度地创建三块等长的空间，将辅存中的数据分割成该长度的小片段，第一次导入主存时，将两个小片段各自排序 然后两个小片段就可以归并了，第三块空间存放结果，分两次向辅存输回结果。之后数据一边进来，一边归并，一边传输结果回去


----------
测试方案：用多组完全相同的数组让各种排序算法独立排序，多次改变数组规模及随机值范围后测试，观察效果
```Java
public class Main {
    public static void main(String[] args) {
        Integer[] a = new Integer[10000000];
        Random rand = new Random(System.currentTimeMillis());
        // 伪随机数填充数组
        for (int i = 0; i < a.length; i++) {
            a[i] = rand.nextInt(99999999);
        }
        //        复制多组相同的原始伪随机序列
        Integer[][] aa = new Integer[10][a.length];
        for (int i = 0; i < aa.length; i++) {
        //      System.arraycopy方法是native方法，比clone()更高效，Arrays.copyOf调用该方法
        //      传入参数（源数组，源数组起始位置，目的数组，目的数组起始位置，复制长度）都是浅拷贝
            System.arraycopy(a, 0, aa[i], 0, a.length);
        }
        try (
                PrintWriter sortResult = new PrintWriter(new FileOutputStream("SortResult.txt"));
        ) {
            SortDemo.print(sortResult, aa);
        } catch (IOException ioe) {
            ioe.printStackTrace();
        }
    }
}
```
一次不全面测试（规模一亿个数时，可能堆内存不足，需要设置JVM）
*数值范围一亿，非负整数*

|算法|规模|耗时/ms|
|-----  |:----:|:---:|
|希尔排序 |1千万|32402|
|堆排序  |1千万|43526|
|快速排序|1千万|7183|
|归并排序|1千万|9753|
|基数排序|1千万|7067|
----------

|Author|Macer|
|---|---
|E-mail|yanggenggang@qq.com
