# 03 STL 与常用容器（完整课堂版）

本章目标：
- 理解 STL（Standard Template Library）的意义与使用方式
- 掌握 vector、string、map、unordered_map、set 等常用容器
- 掌握迭代器、排序、查找等常用算法
- 能用 STL 解决实际问题：词频统计、排序、去重、查找等
- 能完成本章练习题，并理解参考答案

先决条件：已掌握第 1、2 章的基础 C++ 与 OOP

---

## 第一节：什么是 STL？

STL 是 C++ 标准模板库（Standard Template Library），它包含：
- 容器（container）
- 迭代器（iterator）
- 算法（algorithm）
- 函数对象（functor）
- 适配器（adapter）

它的特点是：
- 通用：适用于多种数据类型
- 高效：常见算法和数据结构都经过优化
- 代码简洁：减少重复开发

常见 STL 组件：
- 序列容器：vector, deque, list, array
- 关联容器：map, set, multimap, multiset
- 无序关联容器：unordered_map, unordered_set
- 通用算法：sort, find, reverse, unique, lower_bound

---

## 第二节：vector：动态数组的“万能工具”

### 2.1 vector 的基本概念

`std::vector` 表示动态数组：
- 能自动扩容
- 支持随机访问
- 尾部插入删除效率高
- 很常用于当数组长度不固定时

示例：
```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> v; // 创建一个空的 int 数组，后面可以动态添加元素

    v.push_back(10);    // 在尾部插入元素 10
    v.push_back(20);    // 在尾部插入元素 20
    v.push_back(30);    // 在尾部插入元素 30

    std::cout << "size = " << v.size() << "\n"; // size 表示当前元素数量

    for (int i = 0; i < (int)v.size(); ++i) {
        std::cout << v[i] << ' ';  // 下标访问，和普通数组一样
    }
    std::cout << '\n';

    return 0;
}
```

### 2.2 逐行讲解

```cpp
std::vector<int> v;
```
- `vector` 是模板类
- `vector<int>` 表示元素类型为 int
- 初始化后是空的，没有元素

```cpp
v.push_back(10);
```
- 在尾部依次插入元素
- 它会自动扩容，按需增长内部数组

```cpp
v.size();
```
- 返回当前元素个数
- 类型是 `size_t`，通常是 `unsigned long` 的别名

```cpp
for (int i = 0; i < (int)v.size(); ++i)
```
- 遍历 vector 中的每一个元素
- 传统 for 循环常用于索引访问

### 2.3 常用 vector 操作

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> v = {1, 2, 3, 4, 5}; // 直接初始化

    v.push_back(6);      // 尾部追加
    v.pop_back();         // 删除尾部元素

    std::cout << v.front() << '\n'; // 第一个元素
    std::cout << v.back() << '\n';  // 最后一个元素

    v.clear();            // 清空所有元素
    std::cout << v.empty() << '\n'; // 判断是否为空，1 表示空

    return 0;
}
```

### 2.4 vector 的优点

- 随机访问 O(1)
- 尾部插入删除十分高效
- 动态扩容，不需要在编译期提前分配大小

### 2.5 适用场景

- 存储一组元素
- 管理数组式数据
- 动态输入处理
- 大多数算法题中都非常常见

---

## 第三节：string：文本处理的核心工具

### 3.1 string 的使用

```cpp
#include <iostream>
#include <string>

int main() {
    std::string s = "hello";  // 定义字符串变量
    std::cout << s << '\n';    // 输出 hello

    s += " world";            // 在末尾拼接字符串
    std::cout << s << '\n';   // 输出 hello world

    std::cout << s.size() << '\n'; // 输出字符串长度
    std::cout << s[0] << '\n';     // 输出第一个字符 h

    return 0;
}
```

### 3.2 逐行讲解

```cpp
std::string s = "hello";
```
- `string` 是标准库中的字符串类型
- 不同于 C 风格字符数组，string 更安全、更方便

```cpp
s += " world";
```
- 使用 `+=` 拼接字符串
- 与 `std::string` 结合较多，代码更易读

```cpp
s.size();
```
- 返回字符串长度
- 这是非常常见的接口

```cpp
s[0]
```
- 访问字符串的第一个字符
- `s[0]` 是 `char` 类型

### 3.3 常用 string 操作

```cpp
#include <iostream>
#include <string>

int main() {
    std::string s = "C++";

    s.push_back('!');      // 追加一个字符
    s.append(" is great"); // 追加一个字符串

    std::cout << s << '\n';

    std::string t = "CPP";
    if (s.find("great") != std::string::npos) {
        std::cout << "找到 great\n";
    }

    return 0;
}
```

### 3.4 string 的优势

- 自动管理内存
- 支持大小、拼接、查找、截取等很多操作
- 比 C 风格 `char[]` 更安全、更好用

---

## 第四节：map 与 unordered_map：键值对容器

### 4.1 map：有序键值对

`std::map` 用于存储键值对，并对键进行排序。每个键唯一。

```cpp
#include <iostream>
#include <map>
#include <string>

int main() {
    std::map<std::string, int> mp;
    mp["Alice"] = 90;
    mp["Bob"] = 85;
    mp["Charlie"] = 95;

    for (const auto& [name, score] : mp) {
        std::cout << name << " -> " << score << '\n';
    }

    return 0;
}
```

### 4.2 unordered_map：无序哈希表

`std::unordered_map` 也是键值对容器，但内部用哈希表实现，平均访问更快。

```cpp
#include <iostream>
#include <unordered_map>
#include <string>

int main() {
    std::unordered_map<std::string, int> mp;
    mp["Alice"] = 90;
    mp["Bob"] = 85;
    mp["Charlie"] = 95;

    for (const auto& [name, score] : mp) {
        std::cout << name << " -> " << score << '\n';
    }

    return 0;
}
```

### 4.3 map vs unordered_map

- `map`：按键排序，适合需要有序输出
- `unordered_map`：平均 O(1) 查找，适合大量键值存储和查询
- 选择哪一个，取决于是否需要顺序

### 4.4 词频统计示例

```cpp
#include <iostream>
#include <unordered_map>
#include <string>

int main() {
    std::unordered_map<std::string, int> cnt;
    std::string word;

    while (std::cin >> word) {
        ++cnt[word];
    }

    for (const auto& [w, freq] : cnt) {
        std::cout << w << " : " << freq << '\n';
    }

    return 0;
}
```

说明：
- 读入所有单词
- 以单词为键、出现次数为值
- 最后遍历输出统计结果

---

## 第五节：set 与 unordered_set：去重与集合操作

### 5.1 set：有序集合

```cpp
#include <iostream>
#include <set>

int main() {
    std::set<int> s = {5, 3, 1, 2, 3};

    for (int x : s) {
        std::cout << x << ' ';
    }
    std::cout << '\n';

    return 0;
}
```

输出：
```text
1 2 3 5
```

说明：
- `set` 自动去重
- 元素有序排列
- 很适合“不重复元素”的场景

### 5.2 unordered_set：无序集合

```cpp
#include <iostream>
#include <unordered_set>

int main() {
    std::unordered_set<int> s = {5, 3, 1, 2, 3};

    for (int x : s) {
        std::cout << x << ' ';
    }
    std::cout << '\n';

    return 0;
}
```

说明：
- 无序集合不保证顺序
- 适合快速判断某个元素是否存在

---

## 第六节：迭代器（iterator）

迭代器类似指针，用来遍历 STL 容器。

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> v = {10, 20, 30};

    for (std::vector<int>::iterator it = v.begin(); it != v.end(); ++it) {
        std::cout << *it << ' ';  // *it 表示当前元素
    }
    std::cout << '\n';

    return 0;
}
```

### 6.1 常用迭代器接口

- `begin()`：指向第一个元素
- `end()`：指向末尾后的一个位置
- `++it`：移动到下一个元素
- `*it`：访问当前元素

### 6.2 范围 for 更简洁

```cpp
for (int x : v) {
    std::cout << x << ' ';
}
```

相比迭代器，这种写法更容易理解，并且更短。

---

## 第七节：常用算法（<algorithm>）

STL 中常见算法包括：
- `sort`
- `find`
- `reverse`
- `binary_search`
- `lower_bound`
- `upper_bound`
- `count`
- `unique`

### 7.1 sort：排序

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> v = {5, 1, 3, 2, 4};
    std::sort(v.begin(), v.end());

    for (int x : v) {
        std::cout << x << ' ';
    }
    std::cout << '\n';

    return 0;
}
```

### 7.2 reverse：翻转

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> v = {1, 2, 3, 4};
    std::reverse(v.begin(), v.end());

    for (int x : v) {
        std::cout << x << ' ';
    }
    std::cout << '\n';

    return 0;
}
```

### 7.3 find：查找元素

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> v = {10, 20, 30, 40};
    auto it = std::find(v.begin(), v.end(), 30);

    if (it != v.end()) {
        std::cout << "找到 30，位置是：" << (it - v.begin()) << '\n';
    } else {
        std::cout << "没找到\n";
    }

    return 0;
}
```

### 7.4 unique：去重

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> v = {1, 2, 2, 3, 3, 4};
    std::sort(v.begin(), v.end());
    v.erase(std::unique(v.begin(), v.end()), v.end());

    for (int x : v) {
        std::cout << x << ' ';
    }
    std::cout << '\n';

    return 0;
}
```

说明：
- `std::unique` 只把相邻重复值压缩成一个
- 还需要配合 `erase` 把后面的多余元素移除

---

## 第八节：STL 实战：词频统计

### 8.1 需求说明

输入：一段文本或一组单词

输出：每个单词出现多少次

实现思路：
- 使用 `unordered_map<string, int>` 作为计数表
- 读入单词
- 每读到一个单词，就 `cnt[word]++`
- 最后遍历 map/unordered_map 输出结果

示例代码：
```cpp
#include <iostream>
#include <unordered_map>
#include <string>

int main() {
    std::unordered_map<std::string, int> cnt;
    std::string word;

    while (std::cin >> word) {
        ++cnt[word];
    }

    for (const auto& [w, frequency] : cnt) {
        std::cout << w << " -> " << frequency << '\n';
    }

    return 0;
}
```

### 8.2 代码内的关键点说明

```cpp
std::unordered_map<std::string, int> cnt;
```
- 键：单词
- 值：出现次数

```cpp
while (std::cin >> word)
```
- 只要输入中还有单词，就继续读取
- 这是一种经典的读入方式

```cpp
++cnt[word];
```
- 如果单词第一次出现，就插入键值对并设置为 1
- 如果已经出现过，就让计数加 1

---

## 第九节：STL 实战：排序与去重

### 9.1 需求说明

输入：一个整型数组

输出：去重后排序后的结果

示例代码：
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> v = {5, 2, 1, 3, 2, 5, 4};

    std::sort(v.begin(), v.end());         // 先排序
    v.erase(std::unique(v.begin(), v.end()), v.end()); // 去重

    for (int x : v) {
        std::cout << x << ' ';
    }
    std::cout << '\n';

    return 0;
}
```

### 9.2 代码解释

```cpp
std::sort(v.begin(), v.end());
```
- 把元素按从小到大排序

```cpp
std::unique(v.begin(), v.end())
```
- 把相邻重复元素压缩到一起
- 但是它不会真正删除后面的重复元素

```cpp
v.erase(..., v.end());
```
- 把多余的重复元素真正删掉

因此，这一组合常用于“对数组去重”。

---

## 第十节：STL 实战：查找和二分查找

### 10.1 线性查找

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> v = {1, 3, 5, 7, 9};
    int target = 7;

    auto it = std::find(v.begin(), v.end(), target);
    if (it != v.end()) {
        std::cout << "找到了，位置是 " << (it - v.begin()) << '\n';
    } else {
        std::cout << "没找到\n";
    }

    return 0;
}
```

### 10.2 二分查找

前提：容器必须有序。

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> v = {1, 2, 3, 4, 5, 6, 7};
    int target = 5;

    auto it = std::lower_bound(v.begin(), v.end(), target);
    if (it != v.end() && *it == target) {
        std::cout << "找到了" << '\n';
    } else {
        std::cout << "没找到" << '\n';
    }

    return 0;
}
```

### 10.3 什么时候用二分？

- 容器已排序
- 需要查找某个值有没有出现
- 查找效率更高，复杂度 O(log N)

---

## 第十一节：STL 常用容器对比

| 容器 | 用途 | 关键特性 |
|---|---|---|
| vector | 动态数组 | 支持随机访问，尾部插入快 |
| string | 字符串 | 方便拼接、去查找、截取 |
| map | 键值对，有序 | 键自动排序 |
| unordered_map | 键值对，无序 | 哈希查找快 |
| set | 集合，有序 | 自动去重 |
| unordered_set | 集合，无序 | 哈希去重 |

### 选择建议

- 如果你需要顺序：使用 `map`、`set`
- 如果你需要高性能哈希查找：使用 `unordered_map`、`unordered_set`
- 如果你需要数组：使用 `vector`
- 如果你需要文本：使用 `string`

---

## 第十二节：本章练习题（含参考答案）

### 练习 1：vector 读入并求和

要求：输入 n，然后输入 n 个整数，求和并输出。

参考答案：
```cpp
#include <iostream>
#include <vector>

int main() {
    int n;
    std::cin >> n;

    std::vector<int> v(n);
    int sum = 0;
    for (int i = 0; i < n; ++i) {
        std::cin >> v[i];
        sum += v[i];
    }

    std::cout << sum << '\n';
    return 0;
}
```

---

### 练习 2：统计每个单词出现频率

参考答案：
```cpp
#include <iostream>
#include <unordered_map>
#include <string>

int main() {
    std::unordered_map<std::string, int> cnt;
    std::string word;

    while (std::cin >> word) {
        ++cnt[word];
    }

    for (const auto& [w, freq] : cnt) {
        std::cout << w << " : " << freq << '\n';
    }

    return 0;
}
```

---

### 练习 3：排序并去重

要求：输入一组整数，输出去重后按从小到大排序的结果。

参考答案：
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> v = {5, 1, 2, 2, 3, 5, 4};
    std::sort(v.begin(), v.end());
    v.erase(std::unique(v.begin(), v.end()), v.end());

    for (int x : v) {
        std::cout << x << ' ';
    }
    std::cout << '\n';
    return 0;
}
```

---

### 练习 4：用 map 统计分数

要求：输入多个学生姓名和分数，输出分数分布。

参考答案：
```cpp
#include <iostream>
#include <map>
#include <string>

int main() {
    std::map<std::string, int> score;
    score["Alice"] = 90;
    score["Bob"] = 85;
    score["Charlie"] = 90;

    for (const auto& [name, s] : score) {
        std::cout << name << " -> " << s << '\n';
    }

    return 0;
}
```

---

### 练习 5：找出数组中出现次数最多的元素

要求：给出一个整型数组，统计出现频率并返回最高频元素。

参考答案：
```cpp
#include <iostream>
#include <unordered_map>
#include <vector>

int main() {
    std::vector<int> v = {1, 2, 2, 3, 3, 3, 4};
    std::unordered_map<int, int> freq;

    for (int x : v) {
        ++freq[x];
    }

    int bestValue = 0;
    int bestCount = -1;

    for (const auto& [value, count] : freq) {
        if (count > bestCount) {
            bestValue = value;
            bestCount = count;
        }
    }

    std::cout << "most frequent is " << bestValue << " with count " << bestCount << '\n';
    return 0;
}
```

---

## 第十三节：第 3 周学习计划（课程版）

目标：在 7 天内熟练使用 STL 基础容器和算法。

### 第 1 天：vector 与 string
- 学习 vector 的 push_back, size, clear, empty
- 学习 string 的拼接、长度和查找
- 自己实现一个字符串简单加法器

### 第 2 天：map 和 unordered_map
- 学习键值对结构
- 练习：统计学生分数和单词频率
- 比较 map 和 unordered_map 的差异

### 第 3 天：set 和 unordered_set
- 学习集合去重
- 练习：输入多个数字，去重后输出

### 第 4 天：迭代器与算法
- 学习 begin, end, ++it, *it
- 学习 sort, find, reverse, unique

### 第 5 天：STL 实战训练
- 做词频统计程序
- 做排序去重程序
- 做二分查找题

### 第 6 天：综合题目
- 使用 STL 写一道中等难度算法题
- 例如：出现次数最多元素、相同数字去重、排序和二分查找

### 第 7 天：复盘与更新
- 回顾所有 STL 容器及作用场景
- 画一张“容器选择地图”
- 写一份简短总结：何时用 vector, map, set, unordered_map

---

## 第十四节：本章小结

本章的关键点可以概括为：
- vector 是最常用的动态数组
- string 是处理文本的首选工具
- map / unordered_map 是键值对容器
- set / unordered_set 是去重和集合场景的利器
- sort / find / reverse / unique 用于通用算法题
- STL 让 C++ 程序更简洁、更高效、更接近工程实践

学习 STL 的意义不只是“知道函数怎么用”，而是：
- 能够在真实场景中快速组织数据
- 能写出更短、更稳定、更可维护的代码
- 能在刷题与工程开发中减少重复实现

如果你能做到：
- 会用 vector 和 string
- 会用 map 和 unordered_map
- 会排序、去重、查找
- 能写出简单的词频统计和去重题目

那你已经真正进入了“中级 C++”的学习阶段。

下一章我们将学习：
- C++11/14/17/20 的现代特性
- auto
- lambda
- 智能指针
- 移动语义
- 多线程基础

这会让你从“能写代码”迈向“写更现代、更高质量的 C++ 代码”。

---

## 第十五节：持续学习建议

学习 STL 时，一定不要只看语法。你要明确：
- 什么时候用 vector
- 什么时候用 map
- 什么时候用 unordered_map
- 什么时候用 set
- 什么时候要排序和去重

最好的学习方法是：
- 先理解容器的底层思路
- 再看代码示例
- 再自己敲一遍
- 最后做题验证

很多人学 STL 时，只停留在“知道可用”，但没真正理解“为什么这样设计”。真正掌握它，需要你在真实题目中反复使用。

---

下一步：第 4 章《现代 C++》开始学习自动推导、lambda、智能指针和线程基础。
