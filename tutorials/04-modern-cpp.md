# 04 现代 C++（C++11/14/17/20 简介）

本章目标：介绍现代 C++ 常用特性，提高代码可读性与性能。

## 4.1 auto 与类型推导
```cpp
auto x = 5; // int
auto s = std::string("hi");
```

## 4.2 范围 for（range-based for）
```cpp
for (auto &v : vec) { /* ... */ }
```

## 4.3 智能指针（<memory>）
- std::unique_ptr: 独占所有权
- std::shared_ptr: 共享所有权

示例：
```cpp
#include <memory>
#include <iostream>

int main() {
    auto p = std::make_unique<int>(42);
    std::cout << *p << '\n';
}
```

## 4.4 移动语义与 std::move
- 避免不必要的拷贝，使用移动构造函数或 std::move

示例：
```cpp
#include <string>

std::string foo() { return std::string("hello"); }
int main() {
    std::string s = foo(); // 利用移动/NRVO
}
```

## 4.5 Lambda 表达式
```cpp
#include <algorithm>
#include <vector>

int main() {
    std::vector<int> v = {3,1,4,1,5};
    std::sort(v.begin(), v.end(), [](int a, int b){ return a < b; });
}
```

## 4.6 线程与并发（<thread> / <mutex> 简介）
- std::thread 启动线程，std::mutex 保护共享资源

示例：
```cpp
#include <thread>
#include <iostream>

void f() { std::cout << "hello from thread" << std::endl; }
int main() {
    std::thread t(f);
    t.join();
}
```

## 练习题
1. 编写一个使用 std::thread 的计数程序，两个线程分别计数并用 mutex 同步输出。
2. 实现一个函数，接受一个 vector<string>，返回按长度排序且稳定的结果，使用 lambda。

---
