

### 

C++ STL

#### pair

默认排序规则是，从前往后，越靠前位置的元素越优先排序作为关键字

```cpp
typedef pair<int,pair<int,int>> PII;
```

如果用 vector 容器自带的排序，排序规则则为：

PII.first - 第一排序关键字

PII.second.first - 第二排序关键字

PII.second.second - 第三排序关键字

#### vector自带排序改写大根堆

priority_queue 默认为大根堆，改小根堆如下：

```cpp
priority_queue<int,vector<int>,greater<int>> heap;
```

大根堆的完整写法如下：

```cpp
priority_queue<int,vector<int>,less<int>> heap;
```

greater 表示升序排列，less 表示降序排列，升序排列维护首元即为最小元，降序排列维护首元即为最大元

优先队列结合 PII 对组写法：

```cpp
priority_queue<PII,vector<PII>,greater<PII>> heap;
```

这里默认排序规则即为按升序排序，以 first 为第一排序关键字，second 为第二排序关键字

#### 数组函数

去重函数（unique）：

对一个排好序（一般是升序）的数组进行去重，返回值为去重后数组内剩下的不重复的元素个数

```cpp
cnt = unique(a,a+n) - a;
```

其中 a 为数组，元素范围为 0 - n 之间

翻转函数（reverse）：

把一个数组进行反序

```cpp
reverse(a);
```

#### String 类

取子串函数（substr）：

两个参数，第一个表示子串的起始位置，第二个表示所取子串的长度，其中第二个参数可以忽略，此时默认取到字符串结尾

```cpp
string sub = s.substr(0,s.size());
```

该语句相当于取 s 从 0 位置开始，长度和 s 相同的子串，即为 s 本身

#### 散列表 unordered_map< x , y >

最常见的用法，用来做字符串哈希，把 x 用 string 类，y 用 int 类，可以把 string 映射到一个用户指定的 int 型

```cpp
unorderred_map<string,int> mmap;
```

检验函数（count）：

用来检验某个 string 是否在当前散列表中有对应的 int 值，相当于 dist 和 st 数组的结合

```cpp
if(!mmap[str].count())//说明不存在
if(mmap[str].count())//说明存在
```

#### 全排列函数 next_permutation

生成某个序列的全排列，入参含义同**sort**函数，传入待生成序列的起点位置和终点的下一个位置

生成原理：`next_permutation` 会把当前排列调整为字典序的下一个排列。如果当前排列是最后一个排列，返回 `false`，并将序列重新排列成第一个排列（即最小排列），如果当前排列是最大的字典序排列，它将返回排列的第一个字典序排列

```cpp
do{
    ///
}while(next_permutation(a,a+n));
```

会直接把生成的全排列覆盖在 a 序列原来的位置上，当得到最后一组全排列以后，会返回 false 值，可以作为循环的终止条件，常常和 do-while 循环结合得到所有全排列

#### 结构体类构造 STL

map，set，multiset，multimap 这亖个容器都是会在内部根据 < 对元素进行排序的，如果使用**自定义数据类型**来构造上述容器，则需要给出排序规则，哪怕我们实际上并不需要排序，否则编译器会报错

unordered_map 是基于哈希实现的结构，如果用自定义数据类型则需要我们手动实现哈希函数，比较复杂，一般只用来对已有数据类型（longlong，string）进行哈希维护

前者可以通过重载对应数据类型的运算符来实现

```cpp
typedef struct Node {
	int a, b;
	bool operator > (const Node& x)
	{
		return a < x.a;
	}
	bool cmp(const Node& x)
	{
		return a < x.a;
	}

}Node;

map<Node, int>myMap;
set<Node>mySet;
multimap<Node, int>mmap;
multiset<Node>sset;
```

#### 集合 set

支持的操作：

1. 每个元素被**唯一**储存，可以用来**去重**
2. 对元素自动排序，可以用来模拟**堆**
3. 支持快速按**值**查找或删除元素

不支持的操作：

1. 无法按**下标**像数组那样遍历集合
2. 遍历集合只能通过**迭代器**进行遍历

##### 插入元素 insert

如果集合中已经存在该元素，则不会重复插入

```cpp
mySet.insert(x);
```

##### 查找元素 find

```cpp
if(mySet.find(x) != mySet.end())//元素存在
```

##### 删除元素 rease

```cpp
mySet.erase(x)
```

#### 键值表 map

作用：实现哈希表的作用，map<x1,x2> 其中 x1 是键，x2 是值，map 的作用是把键的类型映射到一个唯一的值的类型

##### 插入 insert

每次插入必须把键和值作为一组同时插入，需要我们自己设好一个值，而不是像哈希表那样插入键以后会自动生成一个唯一与之对应的值

```cpp
myMap.insert({"abc",1});
```

**插入也可以用类似于数组赋值的形式实现**：

```cpp
myMap["abc"] = 1;
```

##### 查找键 find

可以查找对应的键在 map 中是否存在

```cpp
if(myMap.find("abc") != myMap.end())//说明对应键存在
```

##### 删除键 erase

根据键的内容，删除 map 中的某个键值对

```cpp
myMap.erase("abc");
```

##### 访问元素

通过类似于数组的方式可以访问某个键对应的值

```cpp
myMap["abc"]
```

**注意：**如果访问了原本在 map 中不存在的键，访问之后 map 中会插入这个键，并且给他生成一个默认的值（访问完会使得不存在的元素存在了）

##### 遍历元素

使用迭代器遍历即可

```cpp
for (auto it = age_map.begin(); it != age_map.end(); ++it) {
    cout << it->first << " -> " << it->second << endl;
}
```

遍历到的每个元素都分为键和值两部分，分别用 first 和 second 指针指向键和值的内容

##### 获取最大和最小

begin 和 rbegin 函数，分别获取键对应的最小值和最大值，再通过 first 和second 可以分别得到键和值的内容

```cpp
auto min_elem = age_map.begin();
auto max_elem = age_map.rbegin();

cout << "Min element: " << min_elem->first << " -> " << min_elem->second << endl;
cout << "Max element: " << max_elem->first << " -> " << max_elem->second << endl;
```

#### 数组类 vector

##### 删除最后一个元素

```cpp
vector<int>q;
q.push_back(1);//插入
q.pop_back();//删除最后一个元素
```

#### 位级 bitset

##### 结构定义

可以看成一个只存储 0 1 两个元素的数组，尖括号内定义大小

```cpp
bitset<10> s;
```

##### 统计为 1 的数量

```cpp
s.count();
```

##### 位运算

两个同类型的 bitset 可以进行位运算，实现过程就是他们的每一位之间都进行位运算

```cpp
bitset<8> bits4 = bits1 & bits2; // 按位与
bitset<8> bits5 = bits1 | bits2; // 按位或
bitset<8> bits6 = bits1 ^ bits2; // 按位异或
bitset<8> bits7 = ~bits1; // 按位取反
```

两个 bitset< N > 位运算的时候的复杂度为 N / 32，因为其内部并不是真的拿数组一位一位存的，而是用若干个 32 位的 int 来存的，其一次性可以处理一个 int，也就是 32 位 bit 位，会比一般的数组运算快很多 

##### 二维形式

bitset 也可以定义为二维形式

```cpp
bitset<10> s[10];
```

相当于定义了一个全存 0 和 1 的二维数组，他们也可以实现位运算，形如 s [ 1 ] & s [ 2 ] 这样的形式

##### 初始化

```cpp
std::bitset<8> bits1; // 定义一个8位的bitset，所有位初始化为0
std::bitset<8> bits2(0xFF); // 用整数初始化，0xFF对应二进制11111111
std::bitset<8> bits3("10101010"); // 用字符串初始化，字符串表示二进制数
```

##### 访问和修改位

可以通过下标运算符 `[]` 访问和修改 `bitset` 中的位，索引从0开始。

```cpp
bits1[0] = 1; // 设置第0位为1
bool bit = bits1[1]; // 获取第1位的值
```

##### 常用操作

**设置位**：

```cpp
bits1.set(); // 将所有位设置为1
bits1.set(2, 1); // 将第2位设置为1
```

**重置位**：

```cpp
bits1.reset(); // 将所有位重置为0
bits1.reset(2); // 将第2位重置为0
```

**翻转位**：

```cpp
bits1.flip(); // 翻转所有位
bits1.flip(2); // 翻转第2位
```

**测试位**：

```cpp
bool isSet = bits1.test(2); // 测试第2位是否为1
```

**统计1的个数**：

```cpp
size_t count = bits1.count(); // 返回bitset中1的个数
```

**容器大小**：

```cpp
size_t size = bits1.size(); // 返回bitset的大小
```









