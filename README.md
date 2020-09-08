

- Attention please: 

- **If you want to reprint my article, please mark the original address and author(刘书裴).**

- **If you are puzzled about a certain part or have some better suggestions, you can contact me: [3017218062@tju.edu.cn]()/[1005968086@qq.com]()**

- **If my blog has some mistakes, I'm so sorry!**

- **Thanks for watching!**

|   item   |   tool   |
| :------: | :------: |
|  image   | mspaint  |
| formula  |  LaTeX   |
| language |   C++    |
|   date   | 2020.9.6 |
|  author  |  刘书裴  |

# Directory

1.  [线性表](#1)
2.  [栈和队列](#2)
3.  [字符串](#3)
4.  [数组与广义表](#4)
5.  [树与二叉树](#5)
6.  [图与搜索](#6)
7.  [查找](#7)
8.  [排序](#8)
	1.  [插入排序](#8.1)
		1.  [直接插入排序](#8.1.1)
		2.  [折半插入排序](#8.1.2)
		3.  [2-路插入排序](#8.1.3)
		4.  [希尔排序](#8.1.4)
	2.  [快速排序](#8.2)
		1.  [起泡排序](#8.2.1)
		2.  [快速排序](#8.2.2)
	3.  [选择排序](#8.3)
		1.  [直接选择排序](#8.3.1)
		2.  [树形选择排序](#8.3.2)
		3.  [堆排序](#8.3.3)
	4.  [归并排序](#8.4)
	5.  [基数排序](#8.5)
	6.  [排序方法总结](#8.6)

# 线性表<a id="1"/>

- 同一线性表中元素具有相同特性。
- 相邻数据元素之间存在序偶关系。
- 除第一个元素外，其他每一个元素有一个且仅有一个直接前驱。
- 除最后一个元素外，其他每一个元素有一个且仅有一个直接后继。

## 顺序表<a id="1.1"/>

- 定义：将线性表中的元素相继存放在一个**连续**的存储空间中。

- 存储结构：数组。

- 特点：线性表的顺序存储方式。

- 存取方式：顺序存取，随机存取。

## 链表<a id="1.2"/>

### 单链表<a id="1.2.1"/>

- 定义：用一组地址任意的存储单元存放线性表中的数据元素。

- 结构：每个元素由结点(Node)构成,	它包括两个域：数据域Data和指针域Link。

![](./images/1.png)

- 存储结构：链式存储结构。
- 特点：存储单元可以不连续。
- 存取方式：顺序存取。
- 类型定义

```c++
struct Node{
    int data;
    Node* link;
};
Node* head = new Node;
```

- 初始化

```c++
void Create(Node* head, int* initArray, int l){
    cout << "Create a array of size " << l << endl;
    Node* p, * t = head;
    for(int i = 0; i < l; i++){
        p = new Node;
        p->data = initArray[i];
        t->link = p;
        t = p;
    }
    t->link = nullptr;
}
```

- 增删改查

```c++
void Insert(Node* head, int value, int index){
    cout << "Insert " << value << " to index " << index << endl;
    if(index < 0){
        cout << "Index is invalid!" << endl;
        return;
    }
    Node* p, * t = head;
    while(t->link && index){
        t = t->link;
        index--;
    }
    if(index > 0){
        cout << "Index is invalid!" << endl;
        return;
    }
    p = new Node;
    p->data = value;
    p->link = t->link;
    t->link = p;
}

void Delete(Node* head, int index){
    cout << "Delete value of index " << index << endl;
    if(index < 0){
        cout << "Index is invalid!" << endl;
        return;
    }
    Node* p, * t = head;
    while(t->link && index){
        t = t->link;
        index--;
    }
    if(index > 0 || !t->link){
        cout << "Index is invalid!" << endl;
        return;
    }
    p = t->link;
    t->link = p->link;
    delete p;
}

void Update(Node* head, int value, int index){
    cout << "Update value of index " << index << endl;
    if(index < 0){
        cout << "Index is invalid!" << endl;
        return;
    }
    Node* p = head->link;
    while(p->link && index){
        p = p->link;
        index--;
    }
    if(index > 0){
        cout << "Index is invalid!" << endl;
        return;
    }
    p->data = value;
}

int Find(Node* head, int index){
    cout << "Find value of index " << index << endl;
    if(index < 0){
        cout << "Index is invalid!" << endl;
        return -1;
    }
    Node* p = head->link;
    while(p->link && index){
        p = p->link;
        index--;
    }
    if(index > 0){
        cout << "Index is invalid!" << endl;
        return -1;
    }
    return p->data;
}
```

- 长度

```c++
int Length(Node* head){
    int len = 0;
    Node* p = head;
    while(p->link){
        p = p->link;
        len++;
    }
    return len;
}
```

- 清空

```c++
void Clear(Node* head){
    cout << "Clear the array" << endl;
    Node* p;
    while(head->link){
        p = head->link;
        head->link = p->link;
        delete p;
    }
    head->link = nullptr;
}
```

### 静态链表 <a id="1.2.2"/>

- 用一维数组描述线性链表

### 循环链表<a id="1.2.3"/>

- 特点：最后一个结点的 link 指针不为NULL，而是指向头结点。只要已知表中某一结点的地址，就可搜寻所有结点的地址。
- 存储结构：链式存储结构。
- 约瑟夫问题：n 个人围成一个圆圈，首先第1个人从1开始一个人一个人顺时针报数,  报到第m个人，令其出列。然后再从下一个人开始，从1顺时针报数，报到第m个人，再令其出列，…，如此下去,  直到圆圈中只剩一个人为止。此人即为优胜者。

![](./images/2.png)

```c++
void Josephus(int n, int m){
    Node* head = new Node; // 头节点
    head->data = 1; // 赋值创建循环链表
    Node* p, * t = head;
    for(int i = 2; i <= n; i++){
        p = new Node;
        p->data = i;
        t->link = p;
        t = p;
    }
    t->link = head;

    t = head; // 从头节点开始
    for(int i = 1; i < n; i++){ // 依次删除n-1个节点
        for(int j = 0; j < m - 2; j++) // 移动m-2次，不用m-1是为了方便删除节点
            t = t->link;
        cout << i << ": " << t->link->data << endl;
        p = t->link; // 删除节点
        t->link = p->link;
        t = t->link; // 将下一个节点作为开始
        delete p;
    }
    cout << "result: " << t->data << endl;
}
```

### 双向链表<a id="1.2.4"/>

- 特点：在单链表的基础上，对每个节点添加了一个前驱指针。
- 结构：

![](./images/3.png)

- 类型定义

```c++
struct Node{
    int data;
    Node* prior, * next;
};
Node* head = new Node;
```

## 顺序表与链表的比较<a id="1.3"/>

- 基于空间的比较
  - 存储分配的方式
    - 顺序表的存储空间是静态分配的
    - 链表的存储空间是动态分配的
  - 存储密度 = 结点数据本身所占的存储量/结点结构所占的存储总量
    - 顺序表的存储密度 = 1
    - 链表的存储密度 < 1
- 基于时间的比较
  - 存取方式
    - 顺序表可以随机存取，也可以顺序存取
    - 链表是顺序存取的
  - 插入/删除时移动元素个数
    - 顺序表平均需要移动近一半元素
    - 链表不需要移动元素，只需要修改指针

# 排序<a id="8"/>

- **排序**

将一个数据元素的任意序列，重新排列成一个按关键字有序的序列。 

- **数据表**

它是待排序数据对象的有限集合。

- **主关键字**

数据对象有多个属性域, 即多个数据成员组成, 其中有一个属性域可用来区分对象, 作为排序依据，称为关键字。也称为排序码。

- **排序方法的稳定性**

如果在对象序列中有两 个对象r[i]和r[j], 它们的排序码 k[i] == k[j] , 且在排序之前, 对象r[i]排在r[j]前面。如果在排序之后, 对象r[i]仍在对象r[j]的前面,  则称这个排序方法是稳定的, 否则称这个排序方法是不稳定的。

- **内排序与外排序**

内排序是指在排序期间数据对象全部存放在内存的排序；外排序是指在排序期间全部对象个数太多，不能同时存放在内存，必须根据排序过程的要求，不断在内、外存之间移动的排序。

- **排序的时间开销**

排序的时间开销是衡量算法好坏的最重要的标志。排序的时间开销可用算法执行中的数据比较次数与数据移动次数来衡量。

## 插入排序<a id="8.1"/>

每步将一个待排序的对象, 按其排序码大小,  插入到前面已经排好序的一组对象的适当位置上, 直到对象全部插入为止。（假设升序，举例为49、38、65、97、76、13、27、[49]）

### 直接插入排序<a id="8.1.1"/>

#### 1. 简单理解

从插入第二个元素开始，将插入元素与之前插入的元素进行比较，小于就交换，大于就进行下一个元素的插入，直到结束。

#### 2. 排序演示

49、38、65、97、76、13、27、[49]

- 插入49，无前置元素，得49
- 插入38，38<49，无前置元素，得38、49
- 插入65，65>49，停止，得38、49、65
- 插入97，97>65，停止，得38、49、65、97
- 插入76，65<76<97，停止，得38、49、65、76、97
- 插入13，13<38，无前置元素，得13、38、49、65、76、97
- 插入27，13<27<38，无前置元素，得13、27、38、49、65、76、97
- 插入[49]，49=[49]<65，停止，得13、27、38、49、[49]、65、76、97

#### 3. 代码实现

```c++
void InsertSort(int* ARRAY, int n){
    for(int i = 1; i < n; i++){ // 从第二个元素开始一次插入
        int temp = ARRAY[i]; // 记录插入值
        int j = i - 1; // 向前依次比较
        while(j >= 0 && ARRAY[j] > temp){ // 插入值小于前元素
            ARRAY[j + 1] = ARRAY[j]; // 交换
            j--; // 继续向前
        }
        ARRAY[j + 1] = temp; // 在最后的交换位置插入值
    }
}
```

#### 4. 算法分析

- 设待排序对象个数为n, 则该算法的主程序执行n-1趟。
- 排序码比较次数和对象移动次数与对象排序码的初始排列有关。
- 最好情况下,  排序前对象已按排序码从小到大有序,  每趟只需与前面有序对象序列的最后一个对象比较1次, 总的排序 码比较次数为n-1, 不需移动记录。直接插入排序的时间复杂度为O(n^2)。
- 最坏情况下,待排记录按关键字非递增有序排列（逆序）时，第i趟时第i+1个对象必须与前面i个对象都做排序码比较, 并且每做1次比较就要做1次数据移动。总比较次数为(n+2)(n-1)/2次，总移动次数为(n+4)(n-1)/2。
- 在平均情况下的排序码比较次数和对象移动次数约为n^2/4。因此，直接插入排序的时间复杂度为**O(n^2)**。
- 直接插入排序是一种**稳定**的排序方法。

### 折半插入排序<a id="8.1.2"/>

### 2-路插入排序<a id="8.1.3"/>

### 希尔排序（缩小增量排序）<a id="8.1.4"/>

#### 1. 简单理解

先将整个待排记录序列分割成为若干子序列分别进行直接插入排序，待整个序列中的记录基本有序时，再对全体记录进行一次直接插入排序。

首先取一个整数gap<n作为间隔,  将全部对象分为gap个子序列,  所有距离为gap的对象放在同一个子序列中,  在每一个子序列中分别施行直接插入排序。然后缩小间隔gap, 例如取gap=gap/2，重复上述的子序列划分和排序工作。直到最后取gap=1, 将所有对象放在同一个序列中排序为止。

#### 2. 排序演示

49、38、65、97、76、13、27、[49]

- 取gap=4：
  - 对49、76，排序得49、76
  - 对38、13，排序得13、38
  - 对65、27，排序得27、65
  - 对97、[49]，排序得[49]、97
  - 得49、13、27、[49]、76、38、65、97
- 取gap=2：
  - 对49、27、76、65，排序得27、49、65、76
  - 对13、[49]、38、97，排序得13、38、[49]、97
  - 得27、13、49、38、65、[49]、76、97
- 取gap=1：
  - 得13、27、38、49、[49]、65、76、97

#### 3. 代码实现

```c++
void InsertSort(int* ARRAY, int n, int d=1){
    for(int i = d; i < n; i++){
        int temp = ARRAY[i];
        int j = i - d;
        while(j >= 0 && ARRAY[j] > temp){
            ARRAY[j + d] = ARRAY[j];
            j -= d;
        }
        ARRAY[j + d] = temp;
    }
}

void ShellSort(int* ARRAY, int n){
	for(int i = n / 2; i > 0; i /= 2) // 初始gap取n/2，逐渐减小
        InsertSort(ARRAY, n, i); // 对每个子序列进行直接插入排序
}
```

#### 4. 算法分析

- 开始时gap的值较大, 子序列中的对象较少, 排序速度较快;  随着排序进展,  gap 值逐渐变小, 子序列中对象个数逐渐变多,  由于前面大多数对象已基本有序, 所以排序速度仍然很快。
- gap的取法有多种。 Shell提出取gap=n/2，gap=gap/2，直到gap=1。
  对特定的待排序对象序列，可以准确地估算排序码的比较次数和对象移动次数。
- 希尔排序所需的比较次数和移动次数约为**n^1.3**，当n趋于无穷时可减少到**n(log2n)^2**
- 希尔排序是一种**不稳定**的排序方法。

## 快速排序<a id="8.2"/>

两两比较待排序对象的排序码，如发生逆序(即排列顺序与排序后的次序正好相反)，则交换之，直到所有对象都排好序为止。

### 起泡排序<a id="8.2.1"/>

#### 1. 简单理解

对第一个到第n-1个元素，进行n-1次排序，每次排序过程中，从左到右，将相邻元素比较，逆序则交换，直到结束。

#### 2. 排序演示

49、38、65、97、76、13、27、[49]

- 第一次排序：
  - 38、49、65、97、76、13、27、[49]
  - 38、49、65、76、97、13、27、[49]
  - 38、49、65、76、13、97、27、[49]
  - 38、49、65、76、13、27、97、[49]
  - 38、49、65、76、13、27、[49]、97
- 第二次排序：
  - 38、49、65、13、76、27、[49]、97
  - 38、49、65、13、27、76、[49]、97
  - 38、49、65、13、27、[49]、76、97
- 第三次排序：
  - 38、49、13、65、27、[49]、76、97
  - 38、49、13、27、65、[49]、76、97
  - 38、49、13、27、[49]、65、76、97
- 第四次排序：
  - 38、13、49、27、[49]、65、76、97
  - 38、13、27、49、[49]、65、76、97
- 第五次排序：
  - 13、38、27、49、[49]、65、76、97
  - 13、27、38、49、[49]、65、76、97
  - 无交换，停止，得13、27、38、49、[49]、65、76、97

#### 3. 代码实现

```c++
void BubbleSort(int* ARRAY, int n){
    for(int i = 0; i < n - 1; i++){ // n-1次排序
        for(int j = 0; j < n - 1 - i; j++) // 依次比较相邻的元素
            if(ARRAY[j] > ARRAY[j + 1]){ // 逆序则交换
                int temp = ARRAY[j];
                ARRAY[j] = ARRAY[j + 1];
                ARRAY[j + 1] = temp;
            }
    }
}

void BubbleSortV2(int* ARRAY, int n){
    for(int i = 0; i < n - 1; i++){
        int flag = 1; // 第一次优化，设置标志位记录是否发生交换
        for(int j = 0; j < n - 1 - i; j++)
            if(ARRAY[j] > ARRAY[j + 1]){
                int temp = ARRAY[j];
                ARRAY[j] = ARRAY[j + 1];
                ARRAY[j + 1] = temp;
                flag = 0; // 第一次优化，发生交换
            }
        if(flag) break; // 第一次优化，若没有发生交换，则表示已有序
    }
}

void BubbleSortV3(int* ARRAY, int n){
    int pos = n - 1, exc = n - 1; // 第二次优化，设置标志位限制下次排序的范围和本次排序最后一次比较的位置
    for(int i = 0; i < n - 1; i++){
        int flag = 1;
        for(int j = 0; j < pos; j++)
            if(ARRAY[j] > ARRAY[j + 1]){
                int temp = ARRAY[j];
                ARRAY[j] = ARRAY[j + 1];
                ARRAY[j + 1] = temp;
                flag = 0;
                exc = j; // 第二次优化，改变标志位
            }
        pos = exc; // 第二次优化，设置下次排序的范围为本次排序的最后一次交换位
        if(flag) break;
    }
}
```

#### 4. 算法分析

- 最多做n-1趟起泡就能把所有对象排好序。

- 在对象的初始排列已经按排序码从小到大排好序时，此算法只执行一趟起泡，做n-1次排序码比较，不移动对象。这是最好的情形。

- 最坏的情形是算法执行n-1趟起泡,第i趟 (1<= i<= n) 做n-i次排序码比较, 执行n-i次对象交换。这样在最坏情形下总的排序码比较次数KCN和对象移动次数RMN为：
  $$
  KCN=\sum_{i=1}^{n-1}(n-i)=\frac{1}{2}n(n-1)\\
  RMN=3\sum_{i=1}^{n-1}(n-i)=\frac{3}{2}n(n-1)
  $$

- 起泡排序是一个**稳定**的排序方法。时间复杂度为**O(n^2)**。

### 快速排序<a id="8.2.2"/>

#### 1. 简单理解

任取待排序序列中的某个元素(例如取第一个元素) 作为基准, 按照该元素的大小,将整个序列划分为左右两个子序列，一个全大于等于该元素，一个全小于等于该元素。

然后分别对这两个子序列重复施行上述方法，直到所有的元素都排在相应位置上为止。

#### 2. 排序演示

49、38、65、97、76、13、27、[49]

- 以49为基准：
  - 左38、13、27、[49]，以38为基准：
    - 左13、27，以13为基准：
      - 左无
      - 右27
      - 得13、27
    - 右[49]
    - 得13、27、38、[49]
  - 右65、97、76，以65为基准：
    - 左无
    - 右97、76，以97为基准：
      - 左76
      - 右无
      - 得76、97
    - 得65、76、97
  - 得13、27、38、[49]、49、65、76、97

#### 3. 代码实现

```c++
int Partition(int* ARRAY, int left, int right) {
	int key = ARRAY[left]; // 取子序列第一个元素为基准
    while(left < right){ // 遍历子序列所有元素
        while(left < right && ARRAY[right] >= key) // 右边的大于等于基准
            right--; // 指针左移
        if(left < right) // 未遍历结束，则是右指针逆序
            ARRAY[left++] = ARRAY[right]; // 交换
        while(left < right && ARRAY[left] <= key) // 左边的小于等于基准
            left++; // 指针右移
        if(left < right) // 未遍历结束，则是左指针逆序
            ARRAY[right--] = ARRAY[left]; // 交换
    }
    ARRAY[left] = key; // 填充基准
    return left; // 返回基准位置
}

void QuickSort(int* ARRAY, int left, int right) {
	if(left < right){
        int p = Partition(ARRAY, left, right); // 划分为两部分
		QuickSort(ARRAY, left, p - 1); // 左边子序列排序
		QuickSort(ARRAY, p + 1, right); // 右边子序列排序
	}
}
```

#### 4. 算法分析

- 快速排序的趟数取决于递归树的高度。

- 如果每次划分对一个对象定位后，该对象的左侧子序列与右侧子序列的长度相同，则下一步将是对两个长度减半的子序列进行排序，这是最理想的情况。

- 在 n个元素的序列中,  对一个对象定位所需时间为O(n)。若设t(n)是对n个元素的序列进行排序所需的时间，而且每次对一个对象正确定位后，正好把序列划分为长度相等的两个子序列，此时，总的计算时间为：
  $$
  T(n)\leq cn+2T(n/2)\\
  \leq cn+2(cn/2+2T(n/4))=2cn+4T(n/4)\\
  \leq 2cn+4(cn/4+2T(n/8))=3cn+8T(n/8)\\
  ......\\
  \leq cn\log_2n+nT(1)=O(nlog_2n)
  $$

- 可以证明，函数quicksort的平均计算时间也是**O(nlog2n)**。实验结果表明：**就平均计算时间而言，快速排序是所有内排序方法中最好的一个。**

- 快速排序是递归的，需要有一个栈存放每层递归调用时的指针和参数。

- 最大递归调用层次数与递归树的高度一致,理想情况为 log2(n+1) 。因此，要求存储开销为 O(log2n)。

- 在最坏的情况, 即待排序对象序列已经按其排序码从小到大排好序的情况下, 其递归树成为单支树, 每次划分只得到一个比上一次少一个对象的子序列。总的排序码比较次数将达
  $$
  \sum_{i=1}^{n-1}(n-i)=\frac{1}{2}n(n-1)\approx\frac{n^2}{2}
  $$

- 快速排序是一种**不稳定**的排序方法。

## 选择排序<a id="8.3"/>

每一次在后面的待排序元素中选出排序码最小的元素。待到第n-2次作完，待排序记录只剩下1个，就不用再选了。

### 直接选择排序<a id="8.3.1"/>

#### 1. 简单理解

进行n-1次选择最值，直到选出前n-1个最值。

#### 2. 排序演示

49、38、65、97、76、13、27、[49]

- 第一次：**13**、38、65、97、76、**49**、27、[49]
- 第二次：13、**27**、65、97、76、49、**38**、[49]
- 第三次：13、27、**38**、97、76、49、**65**、[49]
- 第四次：13、27、38、**49**、76、**97**、65、[49]
- 第五次：13、27、38、49、**[49]**、97、65、**76**
- 第六次：13、27、38、49、[49]、**65**、**97**、76
- 第七次：13、27、38、49、[49]、65、**76**、**97**

#### 3. 代码实现

```c++
void SelectSort(int* ARRAY, int n){
    for(int i = 0; i < n - 1; i++){ // 选择n-1次最值
        int k = i; // 最值的下标
        for(int j = i + 1; j < n; j++) // 依次比较
            k = ARRAY[j] > ARRAY[k] ? k : j;
        if(k != i){ // 如果最值不在当前位置，交换
            int temp = ARRAY[k];
            ARRAY[k] = ARRAY[i];
            ARRAY[i] = temp;
        }
    }
}
```

#### 4. 算法分析

- 直接选择排序的排序码比较次数KCN与对象的初始排列无关。设整个待排序对象序列有n个对象,   则第i趟选择具有最小排序码对象所需的比较次数总是n-i-1次。总的排序码比较次数为
  $$
  KCN=\sum_{i=0}^{n-2}(n-i-1)=\frac{n(n-1)}{2}
  $$

- 对象的移动次数与对象序列的初始排列有关。当这组对象的初始状态是按其排序码从小到大有序的时候,  对象的移动次数RMN=0，达到最少。

- 最坏情况是每一趟都要进行交换，总的对象移动次数为RMN=3(n-1)。

- 直接选择排序是一种**不稳定**的排序方法。

### 树形选择排序<a id="8.3.2"/>

### 堆排序<a id="8.3.3"/>

#### 1. 简单理解

(1) Ri <= R2i+1且 Ri <= R2i+2 (小顶堆)

(2) Ri >= R2i+1且 Ri >= R2i+2 (大顶堆)

升序----使用大顶堆，降序----使用小顶堆。

大顶堆的特点：每个结点的值都大于或等于其左右孩子结点的值，我们把大顶堆构建完毕后根节点的值一定是最大的，然后把根节点和最后一个元素（也可以说最后一个节点）交换位置，那么末尾元素此时就是最大元素了。

根据初始输入数据，利用堆的调整算法形成初始堆;

通过一系列的对象交换和重新调整堆进行排序。

#### 2. 排序演示

49、38、65、97、76、13、27、[49]

- 建堆：97|76、65|[49]、49、13、27|38
- 互换97和38，建堆：76|[49]、65|38、49、13、27
- 互换76和27，建堆：65|[49]、27|38、49、13
- 互换65和13，建堆：[49]|49、27|38、13
- 互换[49]和13，建堆：49|38、27|13
- 互换49和13，建堆：38|13、27
- 互换38和27，建堆：27|13
- 互换13和27，建堆：13
- 得13、27、38、49、[49]、65、76、97

#### 3. 代码实现

```c++
void Adjust(int* ARRAY, int left, int right){
    int parent = ARRAY[left]; // 记录父节点的值
    for(int i = left * 2 + 1; i <= right; i = i * 2 + 1){ // i*2+1是第一个子节点
        if(i < right && ARRAY[i] < ARRAY[i + 1]) // i*2+2是第二个子节点
            i++; // 选择值最大的那个儿子
        if(parent >= ARRAY[i]) // 无需调整
            break;
        ARRAY[left] = ARRAY[i]; // 父子交换值
        left = i;
    }
    ARRAY[left] = parent;
}

void HeapSort(int* ARRAY, int n){
    int i, temp = 0;
    // 建堆
    for(i = n / 2 - 1; i >= 0; i--) // n/2-1为倒数第一个非叶子节点
        Adjust(ARRAY, i, n - 1); // 初始化调整
    // 调整
    for(i = n - 1; i > 0; i--){ // 对于每一个非根节点
        temp = ARRAY[i]; // 交换根节点和当前节点
        ARRAY[i] = ARRAY[0];
        ARRAY[0] = temp;
        Adjust(ARRAY, 0, i - 1); // 重新调整堆
    }
}
```

#### 4. 算法分析

- 堆排序的时间复杂性为**O(nlog2n)**。
- 该算法的附加存储主要是在第二个for循环中用来执行对象交换时所用的一个临时空间。因此，该算法的空间复杂性为O(1)。
- 堆排序是一个**不稳定**的排序方法。

## 归并排序<a id="8.4"/>

#### 1. 简单理解

先递归划分子问题，然后合并结果。把待排序列看成由两个有序的子序列，然后合并两个子序列，然后把子序列看成由两个有序序列。

快速排序和归并的区别就在于它正好和递归的排序反过来。快速排序先排序再递归细分，排序是从上到下的。归并排序先递归细分再排序，排序是从下到上的。

#### 2. 排序演示

49、38、65、97、76、13、27、[49]

- 递归划分后进行排序
- 得49|38|65|97|76|13|27|[49]
- 得38、49|65、97|13、76|27、[49]
- 得38、49、65、97|13、27、[49]、76
- 得13、27、38、49、[49]、65、76、97

#### 3. 代码实现

```c++
void Merge(int* ARRAY, int left, int mid, int right){
    int num = right - left + 1; // 子序列大小
    int* merged = new int[num]; // 申请额外空间

    int i = left, j = mid + 1, k = 0; // 设置左右子序列的起始指针
    while(i <= mid && j <= right) // 遍历左序列所有元素或右序列所有元素
        if(ARRAY[i] <= ARRAY[j]) // 比较后填入
            merged[k++] = ARRAY[i++];
        else
            merged[k++] = ARRAY[j++];
    while(i <= mid) // 填入未遍历完的元素
        merged[k++] = ARRAY[i++];
    while(j <= right)
        merged[k++] = ARRAY[j++];

    for(k = 0; k < num; k++) // 将合并后的元素赋值到原数组中
        ARRAY[k + left] = merged[k];
    delete []merged; // 释放内存
}

void MergeSort(int* ARRAY, int left, int right) {
	if(left < right){
		int mid = (left + right) / 2; // 序列均分
		MergeSort(ARRAY, left, mid); // 左边子序列排序
		MergeSort(ARRAY, mid + 1, right); // 右边子序列排序
		Merge(ARRAY, left, mid, right); // 合并左右子序列
	}
}
```

```c++
void Merge(int* ARRAY, int* merged, int left, int mid, int right) {
	int i = left, j = mid + 1, k = left; // 设置左右子序列的起始指针
	while(i <= mid && j <= right) // 遍历左序列所有元素或右序列所有元素
		if(ARRAY[i] <= ARRAY[j]) // 比较后填入
            merged[k++] = ARRAY[i++];
		else
            merged[k++] = ARRAY[j++];
    while(i <= mid) // 填入未遍历完的元素
        merged[k++] = ARRAY[i++];
    while(j <= right)
        merged[k++] = ARRAY[j++];
    while(left <= right){ // 将合并后的元素赋值到原数组中
        ARRAY[left] = merged[left];
        left++;
    }
}

void MergeSort(int* ARRAY, int* merged, int left, int right) {
	if (right > left) {
		int mid = (left + right) / 2; // 序列均分
		MergeSort(ARRAY, merged, left, mid); // 左边子序列排序
		MergeSort(ARRAY, merged, mid + 1, right); // 右边子序列排序
		Merge(ARRAY, merged, left, mid, right); // 合并左右子序列
	}
}
```

#### 4. 算法分析

- 算法总的时间复杂度为**O(nlog2n)**。
- 归并排序占用附加存储较多，需要另外一个与原待排序对象数组同样大小的**辅助数组**。这是这个算法的缺点。
- 归并排序是一个**稳定**的排序方法。

## 基数排序<a id="8.5"/>

#### 1. 简单理解

基于数据位数的一种排序算法，按照不同的位数分别排序，对于每个位数，使用一个桶来进行计数，按照计数和桶之间的大小关系进行排序，将所有位数排序后终止。

#### 2. 排序演示

49、38、65、97、76、13、27、[49]

- 第一次分配：13|65|76|97、27|38|49、[49]
- 第一次收集：13、65、76、97、27、38、49、[49]
- 第二次分配：13|27|38|49、[49]|65|76|97
- 第二次收集：13、27、38、49、[49]、65、76、97

#### 3. 代码实现

```c++
int NBit(int x, int n, int radix=10){
    return (x / n) % radix; // 计算当前n位的值
}

void RadixSort(int* ARRAY, int* bucket, int n, int radix=10){
    int i, j, MaxValue = 0, MaxBits = 1;
    for(i = 0; i < n; i++) // 求序列中的最大值
        MaxValue = ARRAY[i] > MaxValue ? ARRAY[i] : MaxValue;
    while(MaxValue >= radix){  // 求最大值的位数
        MaxBits++;
        MaxValue /= radix;
    }

    int counter[radix]; // 定义桶，数量为radix
    int temp = 1; // 用于去除低位
    for(i = 0; i < MaxBits; i++){ // 按每一位进行排序
        for(j = 0; j < radix; j++) // 桶置空
            counter[j] = 0;
        // 分配
        for(j = 0; j < n; j++) // 桶计数，将该位的值相同的元素放入同一个桶内
            counter[NBit(ARRAY[j], temp, radix)]++;
        for(j = 1; j < radix; j++) // 每个桶的大小按升序累加，用于辅助数组的索引
            counter[j] += counter[j - 1];
        // 收集
        for(j = n - 1; j >= 0; j--){ // 遍历序列
            int num = NBit(ARRAY[j], temp, radix); // 计算该位的值
            bucket[counter[num] - 1] = ARRAY[j]; // 将元素按照所在桶的位置填入辅助数组
            counter[num]--; // 桶大小减一
        }
        for(j = 0; j < n; j++) // 将收集后的序列赋值到原序列中
            ARRAY[j] = bucket[j];
        temp *= radix; // 提高位
    }
}
```

#### 4. 算法分析

- 设m为最大位数，时间复杂度为**O(m*n)**，空间复杂度为O(n)，**稳定**排序。

## 排序方法总结<a id="8.6"/>

| 算法 | 平均时间复杂度 | 最坏时间复杂度 | 空间复杂度 | 稳定性 | 测试50000数(ms) | 测试100000数(ms) |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 直接插入排序 | O(n^2) | O(n^2) | O(1) | 是 | 1595 | 6260 |
| 希尔排序 | O(nlogn) | O(n^s) | O(1) | 否 | 10 | 22 |
| 冒泡排序 | O(n^2) | O(n^2) | O(1) | 是 | 6500 | 26500 |
| 快速排序 | O(nlogn) | O(n^2) | O(nlogn) | 否 | 9 | 15 |
| 直接选择排序 | O(n^2) | O(n^2) | O(1) | 否 | 2450 | 9615 |
| 堆排序 | O(nlogn) | O(nlogn) | O(1) | 否 | <10 | 20 |
| 归并排序 | O(nlogn) | O(nlogn) | O(n) | 是 | 7 | 18 |
| 基数排序 | O(n*m) | O(n*m) | O(m) | 是 | <5 | <10 |
