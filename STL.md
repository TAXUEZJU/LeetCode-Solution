### C++标准模板库（STL）介绍

#### vector 常见用法
`vector` 翻译为向量，是一种可以容纳同类型元素的容器，也可以理解为“长度根据需要而自动改变的数组”。要使用 vector ，需要添加以下两行：
`# include <vector>`
`using namespace std;`
##### 1. vector 定义
`vector<typename> name;`
##### 2. vector 容器内元素的访问
- 通过下标访问
对于一个定义为 `vector<typename> vi` 的 vector 容器来说，使用 `vi[index]` 访问即可，下标是从 `0` 到 `vi.size()-1`
- 通过迭代器访问
迭代器可以理解为一种 **复杂的指针**，定义是 `vector<typename>::iterator it;`，可以通过 `*it` 来访问 vector 里的元素
    - `vi[i]` 和 `*(vi.begin()+i)` 是等价的，所以可以通过以下这种方式访问容器内的元素
        ``` C++
        vector<int>::iterator it = vi.begin();
        printf("%d", *(it + i));
        ```
    - 迭代器还实现了两种自加操作：`++it` 和 `it++` （自减操作同理），于是有另一种遍历vector中元素的写法，注意 `end()` 并不是取vi的尾元素地址，而是取尾元素地址的下一个地址
        ``` C++
        //vector的迭代器不支持it < vi.end()的写法，因此循环条件只能用it != vi.end()
        for(vector<int>::iterator it = vi.begin(); it != vi.end(); it++)
        {
            printf("%d ", *it);
        }
        ```
- 注意，在常用 **STL** 容器中，只有在 **vector** 和 **string** 中，才允许使用 `vi.begin() + 3` 这种迭代器加上整数的写法
##### 3. vector 常用函数解析
- **push_back()**
`push_back(x)` 即在 vector 后面添加一个元素 x，时间复杂度 **O(1)** ，如 `vi.push_back(x)`
- **pop_back()**
用以删除 vector 的尾元素，时间复杂度 **O(1)**
- **size()**
用来获得 vector 中元素的个数，时间复杂度 **O(1)** 。size() 返回的是 **unsigned** 类型，一般来说用 `%d` 不会有很大问题，比如 `printf("%d\n", vi.size());`
- **clear()**
用来清空 vector 中所有元素，时间复杂度 **O(N)**
- **insert()**
`insert(it, x)` 用来向 vector 的任意迭代器 it 处插入一个元素 x ，时间复杂度 **O(N)**
- **erase()**
    - `erase(it)` 即删除迭代器为 it 处的元素
    - `erase(first, last)` 即删除迭代器 `[first, last)` 内的所有元素
##### 4. vector 的常见用途
- 本身可以作为数组使用，在一些元素个数不确定的场合可以很好节省空间
- 在需要按一定格式输出数量不确定的数据时
- 实现邻接表储存图

#### set 常见用法
`set`翻译为集合，是一个 **内部自动有序** （递增排序） 且 **不含重复元素** 的容器。要使用 set ，需要添加以下两行：
`# include <set>`
`using namespace std;`
##### 1. set 定义
`set<typename> name;`
##### 2. set 容器内元素的访问
- set 只能通过迭代器访问
`set<typename>::iterator it;`
    由于除开 **vector** 和 **string** 之外的 STL 容器都不支持 `*(it + i)` 的访问方式，因此只能如下枚举：
    ``` C++
    for(set<int>::iterator it = st.begin(); it ！= st.end(); it++)
    {
        printf("%d ", *it);
    }
    ```
##### 3. set 常用函数解析
- **insert()**
`insert(x)` 可将 x 插入 set 容器中，并自动递增排序和去重，时间复杂度 **O(logN)**
- **find()**
`find(value)` 返回 set 中对应值为 value 的迭代器，时间复杂度 **O(logN)** ，如
`set<int>::iterator it = st.find(2);`
- **erase()**
    - `erase(it)` 删除迭代器为 it 处的元素
    - `erase(value)` 删除值为 value 的元素
    - `erase(first, last)` 删除迭代器 `[first, last)` 内的所有元素
- **size()**
`size()` 用来获得 set 内元素的个数， 时间复杂度 **O(1)**
- **clear()**
`clear()` 用来清空 set 中的所有元素，复杂度 **O(N)**
##### 4. set 常见用途
set 最主要的作用是自动去重并按升序排列，因此遇到需要去重但不方便直接开数组的情况，可以尝试用 set 解决
- set 中元素是唯一的，需要处理不为一的情况，需要使用 multiset 。另外，C++ 11 标准中还增加了 unordered_set ，以散列代替 set 内的红黑树，可以用来处理只去重不排序的需求，速度比 set 快得多

#### string 常见用法
string对字符串常用的功能进行了封装，要使用 string ，需要添加以下两行：
`# include <string>`
`using namespace std;`
##### 1. string 定义
- 与基本数据类型相同，在 string 后跟上变量名即可：
`string str;`
- 初始化可直接对变量赋值
`string str = "abcd";`
##### 2. string 中内容的访问
- 通过下标访问
    ``` C++
    string str = "abcd";
    for(int i = 0; i < str.length(); i++)
    {
        printf("%c", str[i]);
    }
    ```
    如果要读入和输出整个字符串，则只能用 **cin** 和 **cout**
- 通过迭代器访问
    ``` C++
    string str = "abcd";
    for(string:iterator it = str.begin(); it != str.end(); it++)
    {
        printf("%c", *it);
    }
    ```
    string 和 vector 一样，支持直接对迭代器加减某个数字，如 `str.begin() + 3` 的写法是可行的
##### 3. string 常用函数解析
- **operator +=**
string 的加法，可以直接将两个 string 拼接起来
`str3 = str1 + str2;`
`str1 += str2;`
- **compare operator**
两个 string 类型可以直接用 ==、!=、<、<=、>、>= 比较大小，比较规则是 **字典序**
- **length()/size()**
前者返回 string 的长度，即存放的字符数，后者与前者基本相同
- **insert()**
string 的 insert() 有很多种写法，下面给出几个常用的写法，时间复杂度 **O(N)**
    - **insert(pos, string)** ，在 pos 位置插入字符串 string
    - **insert(it, it2, it3)** , it 为原字符串的欲插入位置，it2 和 it3 为待插字符串的首尾迭代器，用来表示字符串 [it2, it3) 将被插在 it 的位置上
- **erase()**
    - `str.erase(it)` 用于删除单个元素，it 为需要删除的元素的迭代器
    - `str.erase(first, last)` 删除迭代器 `[first, last)` 内的所有元素
    - `str.erase(pos, length)` 其中 pos 为需要开始删除的起始位置，length 为删除的字符个数
- **clear()**
用于清空 string 中的数据，时间复杂度一般为 `O(1)`
- **substr(pos, len)** 返回从 pos 位开始，长度为 len 的子串，时间复杂度为 **O(len)**
- **string::npos**
`string::npos` 是一个常数，用以作为 find 函数失配时的返回值，其本身的值为 -1 ，但由于时 unsigned_int 类型，因此实际上也可以认为是 unsigned_int 类型的最大值 4294967295
- **find()**
    - `str.find(str2)` 当 str2 是 str 的子串时，返回其在 str 中第一次出现的位置；如果不是，返回 string::npos
    - `str.find(str2, pos)` 从 str 的 pos 号位开始匹配 str2 ，返回值与上相同，时间复杂度 **O(mn)** ，其中 n 和 m 分别为 str 和 str2 的长度
- **replace()**
    - `str.replace(pos, len, str2)` 把 str 从 pos 位开始，长度为 len 的子串替换为 str2
    - `str.replace(it1, it2, str2)` 把 str 的迭代器 `[it1, it2)` 范围的子串替换为 str2

#### map 常见用法
map 翻译为映射，可以将任何基本类型（包括 STL 容器）映射到任何基本类型（包括 STL 容器）。要使用 map ，需要添加以下两行：
`# include <map>`
`using namespace std;`
##### 1. map 定义
`map<typename1, typename2> mp;`
- `<>` 内两个类型前者是键的类型，后者是值的类型
- 如果是字符串到整型的映射，**必须使用 string 而不能用 char 数组**
##### 2. map 容器内元素的访问
- 通过下标访问
    例如对一个定义为 `map<char, int> mp` 的 map 来说，可以直接使用 `mp['c']` 的方式来访问对应的整数，注意，**map 中的键值是唯一的**
- 通过迭代器访问
    - map 迭代器定义与其他 STL 容器相同
    `map<typename1, typename2>::iterator it;`
    - map 使用 `it->first` 访问键，使用 `it->second` 访问值
- map 会以键从小到大的顺序自动排序
##### 3. map 常用函数解析
- **find()**
`find(key)` 返回键为 key 的映射的迭代器，时间复杂度 **O(logN)**
- **erase()**
    - `mp.erase(it)` ，删除单个元素，it 为需要删除的元素的迭代器，时间复杂度 **O(1)**
    - `mp.erase(key)` ，删除单个元素， key 为欲删除的映射的键，时间复杂度 **O(logN)**
    - `mp.erase(first, last)` 删除区间 `[first, last)` 内元素
- **size()**
用来获取 map 中映射的数量，时间复杂度为 **O(1)**
- **clear()**
用来清空 map 中的所有元素，复杂度 **O(N)**
##### 4. map 常见用途
- 需要建立字符（或字符串）与整数之间映射的情境，使用 map 可以减少代码量
- 判断大整数或者其他类型数据是否存在的情况，可以把 map 当 bool 数组用
- 字符串和字符串的映射可能也会用到
- map 的键和值是唯一的，如果一个键需要对应多个值，就只能用 multimap 。C++ 11 中还增加了 unordered_map，以散列代替 map 内部的红黑树实现，使其可以用来处理只映射而不按 key 排序的需求，速度比 map 快得多

#### queue 常见用法
queue 翻译为队列，主要是实现了一个先进先出的容器，要使用 queue，需要添加以下两行：
`# include <queue>`
`using namespace std;`
##### 1. queue 定义
`queue<typename> name;`
typename 可以是任意基本数据类型或容器
##### 2. queue 容器内元素的访问
**只能通过 `front()` 访问队首元素，`back()` 访问队尾元素**
##### 3. queue 常用函数解析
- `push()`
`push(x)` 将 x 进行入队，时间复杂度 `O(1)`
- `front()`、`back()`
分别获得队首元素和队尾元素，时间复杂度 `O(1)`
- `pop()`
令队首元素出队，时间复杂度 `O(1)`
- `empty()`
检测 queue 是否为空，返回 true 则空，返回 false 则非空，时间复杂度 `O(1)`
- `size()`
返回 queue 内元素的个数，时间复杂度 `O(1)`
##### 4. queue 常见用途
需要实现广度优先搜索时，可以不用自己手动实现一个队列，而是用 queue 作为代替，以提高程序的准确性
需要注意的是，**使用 `front()` 和 `back()` 前，必须用 `empty()` 判断队列是否为空**

#### priority_queue 常见用法
又称为优先队列，底层是用**堆**实现的。在优先队列中，**队首元素一定是当前队列中优先级最高的那一个**，要使用优先队列，添加以下两行：
`# include <queue>`
`using namespace std;`
##### 1. priority_queue 定义
`priority_queue<typename> name;`
##### 2. priority_queue 容器内元素的访问
优先队列只能通过 `top()` 函数访问队首元素
##### 3. priority_queue 常用函数解析
- `push()`
`push(x)` 将 x 入队，时间复杂度为 `O(logN)`，其中 N 为当前优先队列中的元素个数
- `top()`
可以获得队首元素，时间复杂度 `O(1)`
- `pop()`
令队首元素出队，时间复杂度 `O(logN)`，其中 N 为当前优先队列中的元素个数
- `empty()`
检测优先队列是否为空，返回 true 则为空，false 则非空，时间复杂度 `O(1)`
- `size()`
返回优先队列内元素的个数，时间复杂度 `O(1)`
##### 4. priority_queue 内元素优先级的设置
定义优先队列内元素的优先级是运用好优先队列的关键，下面分别介绍基本数据类型与结构体类型的优先级设置方法
- 基本数据类型的优先级设置
指的是 int、double、char 等可以直接使用的数据类型，优先队列对它们的优先级设置一般是数字大的优先级越高，因此队首元素是优先队列内元素最大的那个（char 型是字典序最大的）

#### 应用实例
##### [A1039](https://www.patest.cn/contests/pat-a-practise/1039)
```C++ {.line-numbers}
#include <cstdio>
#include <cstring>
#include <vector>
#include <algorithm>
using namespace std;
const int N = 40010;
const int M = 26*26*26*10 + 1;
vector<int> selectCourse[M];

int getID(char name[])
{
    int id = 0;
    for(int i = 0; i < 3; i++)
    {
        id = id * 26 + (name[i] - 'A');
    }
    id = id * 10 + (name[3] - '0');
    return id;
}

int main()
{
    char name[5];
    int n, k;
    scanf("%d%d", &n, &k);
    for(int i = 0; i < k; i++)
    {
        int course, x;
        scanf("%d%d", &course, &x);
        for(int j = 0; j < x; j++)
        {
            scanf("%s", name);
            int id = getID(name);
            selectCourse[id].push_back(course);
        }
    }
    for(int i = 0; i < n; i++)
    {
        scanf("%s", name);
        int id = getID(name);
        sort(selectCourse[id].begin(), selectCourse[id].end());
        printf("%s %d", name, selectCourse[id].size());
        for(int j = 0; j < selectCourse[id].size(); j++)
        {
            printf(" %d", selectCourse[id][j]);
        }
        printf("\n");
    }
    return 0;
}    
```

##### [A1047](https://www.patest.cn/contests/pat-a-practise/1047)
与上题输入输出互换
```C++ {.line-numbers}
#include <cstdio>
#include <vector>
#include <algorithm>
#include <cstring>
using namespace std;
const int maxn = 40001;
const int maxk = 2501;
vector<int> course[maxk];
char name[maxn][5];
bool cmp(int a, int b)
{
    return strcmp(name[a], name[b]) < 0;
}

int main()
{
    int n, k, x, courseID;
    scanf("%d%d", &n, &k);
    for(int i = 0; i < n; i++)
    {
        scanf("%s %d", name[i], &x);
        for(int j = 0; j < x; j++)
        {
            scanf("%d", &courseID);
            course[courseID].push_back(i);
        }
    }
    for(int i = 1; i <= k; i++)
    {
        sort(course[i].begin(), course[i].end(), cmp);
        printf("%d %d\n", i, course[i].size());
        for(int j = 0; j < course[i].size(); j++)
            printf("%s\n", name[course[i][j]]);
    }
    return 0;
}
```

##### [A1063](https://www.patest.cn/contests/pat-a-practise/1063)
```C++ {.line-numbers}
#include <cstdio>
#include <set>
using namespace std;
const int maxn = 51;
set<int> st[maxn];
void compare(int a, int b)
{
    int totalNum = st[b].size();
    int sameNum = 0;
    for(set<int>::iterator it = st[a].begin(); it != st[a].end(); it++)
    {
        if(st[b].find(*it) != st[b].end())
            sameNum++;
        else
            totalNum++;
    }
    printf("%.1f%%\n", sameNum * 100.0 / totalNum);
}

int main()
{
    int n;
     scanf("%d", &n);
     for(int i = 1; i <= n; i++)
     {
         int m, temp;
         scanf("%d", &m);
         for(int j = 0; j < m; j++)
         {
             scanf("%d", &temp);
             st[i].insert(temp);
         }
     }
     int t;
     scanf("%d", &t);
     for(int i = 0; i < t; i++)
     {
         int a, b;
         scanf("%d%d", &a, &b);
         compare(a, b);
     }
     return 0;
}
```

##### [A1060](https://www.patest.cn/contests/pat-a-practise/1060)
```C++
#include <iostream>
#include <string>
using namespace std;
int n;
string deal(string s, int &e)
{
    int k = 0;
    while(s.length() > 0 && s[0] == '0')
        s.erase(s.begin());
    if(s[0] == '.')
    {
        s.erase(s.begin());
        while(s.length() > 0 && s[0] == '0')
        {
            s.erase(s.begin());
            e--;
        }
    }
    else
    {
        while(k < s.length() & s[k] != '.')
        {
            k++;
            e++;
        }
        if(k < s.length())
        {
            s.erase(s.begin() + k);
        }
    }
    if(s.length() == 0)
    {
        e = 0;
    }
    int num = 0;
    k = 0;
    string res;
    while(num < n)
    {
        if(k < s.length())
            res += s[k++];
        else
            res += '0';
        num++;
    }
    return res;
}

int main()
{
    string s1, s2, ss1, ss2;
    cin >> n >> s1 >> s2;
    int e1 = 0, e2 = 0;
    ss1 = deal(s1, e1);
    ss2 = deal(s2, e2);
    if(ss1 == ss2 && e1 == e2)
        cout << "YES 0." << ss1 << "*10^" << e1 << endl;
    else
        cout << "NO 0." << ss1 << "*10^" << e1 << " 0." << ss2 << "*10^" << e2 << endl;
    return 0;
}
```
- A1100
- A1054
- A1071
- A1022
