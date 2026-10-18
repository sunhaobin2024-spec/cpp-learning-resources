# 03 STL 与常用容器

本章目标：掌握常用容器（vector、string、deque、list、set、map、unordered_map）、迭代器与常用算法。

## 3.1 vector
- 动态数组，随机访问快，尾部插入快

示例：
```cpp
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v;
    for (int i = 0; i < 5; ++i) v.push_back(i);
    for (int x : v) std::cout << x << ' ';
}
```

## 3.2 string
- std::string 提供方便的字符串操作

## 3.3 map / unordered_map
- map 有序（红黑树），unordered_map 基于哈希表，平均访问更快

示例（统计词频）：
```cpp
#include <iostream>
#include <unordered_map>
#include <string>

int main() {
    std::unordered_map<std::string,int> cnt;
    std::string w;
    while (std::cin >> w) cnt[w]++;
    for (auto &p : cnt) std::cout << p.first << ": " << p.second << '\n';
}
```

## 3.4 常用算法（<algorithm>）
- sort, find, lower_bound, upper_bound, binary_search, reverse, unique 等

示例（排序并去重）：
```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> a = {3,1,2,3,2};
    std::sort(a.begin(), a.end());
    a.erase(std::unique(a.begin(), a.end()), a.end());
    for (int x : a) std::cout << x << ' ';
}
```

## 练习题
1. 用 unordered_map 实现单词统计（case sensitive）。
2. 给定一个整数数组，找出出现次数超过 n/2 的众数（摩尔投票或哈希）。
3. 使用 vector 和 sort 实现区间合并（Merge Intervals）。

---
