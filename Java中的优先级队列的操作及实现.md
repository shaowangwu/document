# Java中的优先级队列的操作及实现

Java中的优先级队列可以利用数组完成优先级队列的一些操作。

首先，我们要给出数组存放数据，再给一个size保存数组的长度。（这里数组的长度可以自己设置一个，因为要构建出数组，在插入的操作过程中也可以对原先的数组进行扩容）

int[] arr = new int[10];
int size;

在每个操作的实现过程中，需要一些其他的方法来辅助各种操作的实现，需要利用堆中的向上调整、向下调整，还用交换数组元素的方法。代码如下：以小堆为例

//交换
public void swap(int[] arr,int i, int j) {
    int tmp = arr[i];
    arr[i] = arr[j];
    arr[j] = tmp;
}

//向上调整
public void shiftUp(int[] arr,int sz,int child) {
    int parent = (child - 1)/2;
    while (child > 0) {
        if (arr[child] < arr[parent]) {
            swap(arr, child, parent);
            child = parent;
            parent = (child - 1) / 2;
        } else {
            break;
        }
    }
}

//向下调整
public void shiftDown(int[] arr,int sz,int parent) {
    int child = 2 * parent + 1;
    while (child < sz) {
        if (child + 1 < sz && arr[child + 1] < arr[child]) {
            child++;
        }
        if (arr[child] < arr[parent]) {
            swap(arr,child,parent);
            parent = child;
            child = 2 * parent + 1;
        } else {
            break;
        }
    }
}

作为队列，是可以实现队列的操作的，下面是代码实现

入队
//入队
public void offer(int value) {
   if (size == arr.length) {
       arr = Arrays.copyOf(arr,arr.length*2);
   }
   arr[size++] = value;    //尾插
   shiftUp(arr,size,size-1);   //向上调整
}

出队
public int poll() {
   if (size > 0) {
       int peek = arr[0];
       swap(arr,0,size-1);
       size--;
       shiftDown(arr,size,0);
       return peek;
   }
   return -1;
}

取队顶元素
public int peek() {
    return arr[0];
}

判断是否为空
public boolean isEmpty() {
    return size == 0;
}
优先级队列是堆的应用，也可以完成队列的操作
————————————————
版权声明：本文为CSDN博主「weixin_45646896」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_45646896/article/details/104900738





华为2019牛客网华为研发工程师编程题



[编程题]汽水瓶

时间限制：C/C++ 1秒，其他语言2秒

空间限制：C/C++ 32M，其他语言64M

某商店规定：三个空汽水瓶可以换一瓶汽水，允许向老板借空汽水瓶（但是必须要归还）。

小张手上有n个空汽水瓶，她想知道自己最多可以喝到多少瓶汽水。

数据范围：输入的正整数满足 ![img](https://www.nowcoder.com/equation?tex=1%20%5Cle%20n%20%5Cle%20100%20%5C)

注意：本题存在多组输入。输入的 0 表示输入结束，并不用输出结果。



##### **输入描述:**

```
输入文件最多包含 10 组测试数据，每个数据占一行，仅包含一个正整数 n（ 1<=n<=100 ），表示小张手上的空汽水瓶数。n=0 表示输入结束，你的程序不应当处理这一行。
```



##### **输出描述:**

```
对于每组测试数据，输出一行，表示最多可以喝的汽水瓶数。如果一瓶也喝不到，输出0。
```



##### **输入例子1:**

```
3
10
81
0
```



##### **输出例子1:**

```
1
5
40
```



##### **例子说明1:**

```
样例 1 解释：用三个空瓶换一瓶汽水，剩一个空瓶无法继续交换
样例 2 解释：用九个空瓶换三瓶汽水，剩四个空瓶再用三个空瓶换一瓶汽水，剩两个空瓶，向老板借一瓶汽水喝完得三个空瓶换一瓶汽水还给老板 
```





[编程题]明明的随机数

时间限制：C/C++ 1秒，其他语言2秒

空间限制：C/C++ 32M，其他语言64M

明明生成了![N](https://www.nowcoder.com/equation?tex=N)个1到500之间的随机整数。请你删去其中重复的数字，即相同的数字只保留一个，把其余相同的数去掉，然后再把这些数从小到大排序，按照排好的顺序输出。

数据范围： ![img](https://www.nowcoder.com/equation?tex=1%20%5Cle%20n%20%5Cle%201000%20%5C) ，输入的数字大小满足 ![img](https://www.nowcoder.com/equation?tex=1%20%5Cle%20val%20%5Cle%20500%20%5C)



##### **输入描述:**

```
第一行先输入随机整数的个数 N 。
接下来的 N 行每行输入一个整数，代表明明生成的随机数。
具体格式可以参考下面的"示例"。
```



##### **输出描述:**

```
输出多行，表示输入数据处理后的结果
```



##### **输入例子1:**

```
3
2
2
1
```



##### **输出例子1:**

```
1
2
```



##### **例子说明1:**

```
输入解释：
第一个数字是3，也即这个小样例的N=3，说明用计算机生成了3个1到1000之间的随机整数，接下来每行一个随机数字，共3行，也即这3个随机数字为：
2
2
1
所以样例的输出为：
1
2   
```



[编程题]进制转换

时间限制：C/C++ 1秒，其他语言2秒

空间限制：C/C++ 32M，其他语言64M

写出一个程序，接受一个十六进制的数，输出该数值的十进制表示。

数据范围：保证结果在 ![img](https://www.nowcoder.com/equation?tex=1%20%5Cle%20n%20%5Cle%202%5E%7B31%7D-1%20%5C)



##### **输入描述:**

```
输入一个十六进制的数值字符串。
```



##### **输出描述:**

```
输出该数值的十进制字符串。不同组的测试用例用\n隔开。
```



##### **输入例子1:**

```
0xAA
```



##### **输出例子1:**

```
170
```



【华为社招】
完全二叉树非叶子部分后序遍历
查找接口成功率最优时间段
斗地主之顺子
运维日志排序
数组二叉树
数据分类



