# java Map 原理
JDK 1.6, JDK 1.7 HashMap 采用位桶 + 链表实现。

JDK 1.8 HashMap 采用位桶 + 链表 + 红黑树实现。（当链表长度超过阈值 “8” 时，将链表转换为红黑树）

## 介绍
### map 元素

HashMap 实际上是一个链表散列，即数组和链表的结合体。

HashMap 每一个节点都继承于 **Map.Entry** 。

每个 **Map.Entry** 包含 **Hash**、**Key**、**Value**、**Next** 等信息。

### 存储方式

先介绍位桶 + 链表这一种形式。

![[javaMap 位桶加链表数据结构.png]]

HashMap 的每一个元素，都是链表的一个节点（entry）。

新增一个元素时，会先计算 key 的 hash 值，找到存入数组的位置。

如果该位置已经有节点（链表头），则存入该节点的最后一个位置（链表尾）。

所以 HashMap 就是一个数组（bucket），数组上每一个元素都是一个节点（节点和所有下一个节点组成一个链表）或者为空，显然同一个链表上的节点 hash 值都一样。

## 相关操作
### HashMap hash 与 index

由于 HashMap 容量是 $2^n$ ，那么如果算出 hash，对应的数组索引为：$index = hash$  %  $2^n$
 

通过位运算，我们知道其等价于 $index = hash ⊕ (2^n -1)$，(⊕ 异或)
即： $index = hash\ \& ((1<<n) - 1)$

### HashMap 新增
1. 先计算 key 的 hash 值
2. hash 值作为 index ，找到对应的数值位置
	如果数组位置为空，直接存入当前的 Map.Entry
	如果数组位置为空，则遍历链表，插入末尾。
### HashMap 删除
1. 先计算 key 的 hash 值
2. hash 值作为 index ，找到对应的数值位置
3. 遍历该链表，找到目标 Map.Entry 进行删除。


## 容量与扩容

### HashMap 容量 (capacity) 和负载因子 (loadFactor)
capacity 是数组（bucket）的大小，loadFactor 是数组的最大填满比例。

当数组中的节点（entry）数目 >  $capacity∗loadFactor$ 时，就需要扩容，调整数组的大小为当前的 2 倍，以提高 HashMap 的 hash 效率。

所以数组的初始容量和扩容后的容量必须是 $2^n$。
默认的 capacity 为 16（n = 4），loadFactor 为 0.75。

我们知道散列访问效率高，链表反之。但散列空间利用率不如链表。
loadFactor 过大，容易导致访问时频繁发生碰撞，导致出现大量的链表访问，影响访问效率。
loadFactor 过小，则会导致 HashMap 频繁扩容，空间浪费多。
如果数据量较大，需要设置合理的 capacity 和 loadFactor 值。

### HashMap resize

由于map中 index的计算方式 （见[[java Map 原理### HashMap 容量 (capacity) 和负载因子 (loadFactor)]])，所有的 Map.Entry 的 index 都是 n 位二进制值。
如果此时 HashMap 的数组填满率过高时（$size > capacity*loadFactor$），需要进行扩容。
那么扩容后 N=n+1, Capacity = capacity * 2。

显然所有的 Map.Entry 都需要重新规划到新的空间上。那么所有的 Map.Entry 的 index 都是 n+1 为二进制。
也就是每个链表上的节点的 index 需要增加一个二进制 0 或 1。
显然就能把所有链表的长度减半。