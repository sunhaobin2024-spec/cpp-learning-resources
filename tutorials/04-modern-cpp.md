# 04 现代 C++（完整课堂版）

本章目标：
- 了解现代 C++ 的关键特性与演进意义
- 掌握 `auto`、范围 `for`、`lambda`、智能指针、移动语义等特性
- 理解 `std::thread` 与 `std::mutex` 在并发中的基本应用
- 能写出更现代、更简洁、更安全的 C++ 代码
- 能完成本章练习题，并理解参考答案

先决条件：已掌握第 1、2、3 章的基础语法、OOP 和 STL

---

## 第一节：什么是现代 C++？

现代 C++ 通常指：
- C++11
- C++14
- C++17
- C++20

这些版本带来了非常多的改进：
- 语言更加简洁
- 代码更容易维护
- 更适合工程和并发开发
- 更适合高性能与现代编程范式

现代 C++ 的特点包括：
- 自动类型推导
- 范围循环
- lambda 表达式
- 智能指针
- 移动语义
- 并发编程基础

---

## 第二节：auto 与类型推导

### 2.1 auto 的概念

`auto` 允许编译器自动推断变量类型，使代码更加简洁。

```cpp
#include <iostream>
#include <string>

int main() {
    auto x = 10;               // x 被推断为 int
    auto y = 3.14;            // y 被推断为 double
    auto name = std::string("C++");

    std::cout << x << " " << y << " " << name << '\n';
    return 0;
}
```

### 2.2 逐行讲解

```cpp
auto x = 10;
```
- 编译器会推断 `x` 的类型为 `int`
- 代码更短，同时可读性也很好

```cpp
auto y = 3.14;
```
- 推断为 `double`

```cpp
auto name = std::string("C++");
```
- 推断为 `std::string`

### 2.3 auto 的优点

- 减少冗长类型名
- 让代码更容易维护
- 与 STL 结合时非常自然

### 2.4 注意事项

`auto` 并不神奇，它只是“类型推导”，编译器仍然知道真实类型。它不能替代你对类型的理解。

例如：
```cpp
auto it = v.begin();
```
这里 `it` 的类型是迭代器类型，不是 `int`。你不能忽略真正的底层类型。

---

## 第三节：范围 for（range-based for）

范围 for 循环让遍历容器变得更简单。

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> v = {1, 2, 3, 4, 5};

    for (int x : v) {
        std::cout << x << ' ';
    }
    std::cout << '\n';

    return 0;
}
```

### 3.1 逐行讲解

```cpp
for (int x : v)
```
- `x` 是每一个元素的副本
- `:` 后面是要遍历的容器

如果要修改元素，应该使用引用：
```cpp
for (int &x : v) {
    x *= 2;
}
```

### 3.2 范围 for 的优点

- 语法更简洁
- 更适合遍历容器
- 代码更容易读

---

## 第四节：lambda 表达式

### 4.1 lambda 是什么？

lambda 用于定义匿名函数，尤其适合回调、排序、过滤等场景。

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> v = {5, 2, 4, 1, 3};

    std::sort(v.begin(), v.end(), [](int a, int b) {
        return a < b;
    });

    for (int x : v) {
        std::cout << x << ' ';
    }
    std::cout << '\n';

    return 0;
}
```

### 4.2 逐行讲解

```cpp
[](int a, int b) {
    return a < b;
}
```
- `[]` 表示 lambda 的捕获列表
- `()` 表示参数列表
- `{}` 表示函数体

这里的 lambda 用于自定义排序规则：按升序排序。

### 4.3 lambda 的常见用法

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> v = {1, 2, 3, 4, 5};

    for_each(v.begin(), v.end(), [](int x) {
        std::cout << x * 2 << ' ';
    });
    std::cout << '\n';

    return 0;
}
```

### 4.4 捕获列表

lambda 中的 `[]` 可以捕获外部变量：
```cpp
int multiplier = 3;
auto f = [multiplier](int x) {
    return x * multiplier;
};
```

- `[=]`：按值捕获全部
- `[&]`：按引用捕获全部
- `[x]`：只按值捕获 x

---

## 第五节：智能指针（smart pointer）

### 5.1 为什么需要智能指针？

传统 `new` / `delete` 容易出现：
- 内存泄漏
- double free
- 资源释放时机错误

智能指针让资源管理更安全。

### 5.2 unique_ptr：唯一所有权

```cpp
#include <iostream>
#include <memory>

int main() {
    std::unique_ptr<int> p = std::make_unique<int>(42);
    std::cout << *p << '\n';
    return 0;
}
```

### 5.3 shared_ptr：共享所有权

```cpp
#include <iostream>
#include <memory>

int main() {
    std::shared_ptr<int> p1 = std::make_shared<int>(100);
    std::shared_ptr<int> p2 = p1; // 共享所有权

    std::cout << *p1 << " " << *p2 << '\n';
    return 0;
}
```

### 5.4 选择建议

- `unique_ptr`：默认首选
- `shared_ptr`：需要共享时使用
- 避免裸指针，除非非常必要

### 5.5 关键点

```cpp
std::make_unique<T>(...)
std::make_shared<T>(...)
```
- 比 `new` 更安全
- 更符合现代 C++ 风格
- 避免手工管理内存

---

## 第六节：移动语义和 std::move

### 6.1 什么是移动语义？

移动语义允许对象把资源“转移”给另一个对象，而不是复制一份。

```cpp
#include <iostream>
#include <string>
#include <utility>

int main() {
    std::string s1 = "hello";
    std::string s2 = std::move(s1);

    std::cout << "s1 = " << s1 << '\n';
    std::cout << "s2 = " << s2 << '\n';
    return 0;
}
```

### 6.2 逐行讲解

```cpp
std::string s2 = std::move(s1);
```
- `std::move(s1)` 表示把 `s1` 的内容当作右值进行移动
- 编译器可能执行更高效的移动而不是复制

### 6.3 为什么它重要？

- 避免不必要的拷贝
- 对大型对象和资源管理对象尤其重要
- 适合工程代码和高性能编程

---

## 第七节：RAII（资源获取即初始化）

RAII 是现代 C++ 的核心设计思路：
- 资源在对象构造时获取
- 资源在对象析构时释放

智能指针本质上就是一种 RAII 实现。

```cpp
#include <iostream>
#include <memory>

class Demo {
public:
    Demo() {
        std::cout << "构造\n";
    }

    ~Demo() {
        std::cout << "析构\n";
    }
};

int main() {
    std::unique_ptr<Demo> p = std::make_unique<Demo>();
    return 0;
}
```

### 7.1 关键点

- 资源的生命周期和对象生命周期绑定
- 资源释放自动发生，不需要手动 `delete`
- 这是现代 C++ 编程中的核心价值

---

## 第八节：线程基础（std::thread 与 std::mutex）

### 8.1 std::thread 基础

```cpp
#include <iostream>
#include <thread>

void task() {
    std::cout << "hello from thread\n";
}

int main() {
    std::thread t(task);
    t.join();  // 等待线程结束
    return 0;
}
```

### 8.2 逐行讲解

```cpp
std::thread t(task);
```
- 创建一个新线程并启动 `task` 函数

```cpp
t.join();
```
- 等待该线程执行完毕
- `join` 是最常见的线程同步方式

### 8.3 std::mutex：互斥锁

```cpp
#include <iostream>
#include <thread>
#include <mutex>

std::mutex mtx;

void task(int id) {
    std::lock_guard<std::mutex> lock(mtx);
    std::cout << "thread " << id << " is running\n";
}

int main() {
    std::thread t1(task, 1);
    std::thread t2(task, 2);

    t1.join();
    t2.join();
    return 0;
}
```

### 8.4 为什么要锁？

多个线程同时访问共享资源时，可能出现：
- 数据竞争
- 结果不稳定
- 程序行为随机

使用 `std::mutex` 可以保护共享资源，保证安全访问。

---

## 第九节：现代 C++ 常见练习题（含参考答案）

### 练习 1：使用 auto 和 vector 统计和

参考答案：
```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> v = {1, 2, 3, 4, 5};
    int sum = 0;

    for (auto x : v) {
        sum += x;
    }

    std::cout << sum << '\n';
    return 0;
}
```

---

### 练习 2：lambda 进行排序

参考答案：
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> v = {5, 2, 9, 1, 7};

    std::sort(v.begin(), v.end(), [](int a, int b) {
        return a < b;
    });

    for (int x : v) {
        std::cout << x << ' ';
    }
    std::cout << '\n';
    return 0;
}
```

---

### 练习 3：使用 unique_ptr 处理资源

参考答案：
```cpp
#include <iostream>
#include <memory>

int main() {
    auto p = std::make_unique<int>(42);
    std::cout << *p << '\n';
    return 0;
}
```

---

### 练习 4：使用 std::move 进行字符串移动

参考答案：
```cpp
#include <iostream>
#include <string>
#include <utility>

int main() {
    std::string a = "hello";
    std::string b = std::move(a);

    std::cout << a << '\n';
    std::cout << b << '\n';
    return 0;
}
```

---

### 练习 5：线程加锁输出

参考答案：
```cpp
#include <iostream>
#include <thread>
#include <mutex>

std::mutex mtx;

void task(int id) {
    std::lock_guard<std::mutex> lock(mtx);
    std::cout << "线程 " << id << " 运行中\n";
}

int main() {
    std::thread t1(task, 1);
    std::thread t2(task, 2);

    t1.join();
    t2.join();
    return 0;
}
```

---

## 第十节：第 4 周学习计划（课程版）

目标：在 7 天内掌握现代 C++ 常见语法和安全编程思维。

### 第 1 天：auto 与范围 for
- 学习 `auto`
- 学习 `for (auto x : v)`
- 练习：遍历 vector 并求和

### 第 2 天：lambda
- 学习 `[](){}`
- 实现排序和遍历函数
- 练习：按不同规则排序

### 第 3 天：智能指针
- 学习 `unique_ptr`, `shared_ptr`, `make_unique`, `make_shared`
- 练习：安全管理一个动态对象

### 第 4 天：移动语义
- 学习 `std::move`
- 理解为什么对象移动比复制高效

### 第 5 天：RAII
- 理解资源管理和对象生命周期
- 练习：封装一个资源类

### 第 6 天：线程基础
- 学习 `std::thread` 和 `std::mutex`
- 练习：两个线程输出互斥访问

### 第 7 天：综合复盘
- 做所有练习题
- 复盘 modern C++ 的核心思想：安全、简洁、效率

---

## 第十一节：本章小结

本章的核心思想是：
- `auto` 让代码更简洁
- lambda 让回调更自然
- 智能指针让资源管理更安全
- `std::move` 让对象转移更高效
- 线程与互斥让并发更成熟

现代 C++ 的格言可以概括为：
- 少用裸指针
- 多用容器和标准库
- 多用 RAII
- 让编译器帮你管理生命周期

如果你能理解：
- `auto` 不是偷懒，而是自动类型推导
- lambda 不是炫技，而是函数对象的现代写法
- 智能指针不是额外负担，而是安全管理资源的标准方式

那么你已经从“写得出代码”升级到了“写得更稳、更现代的代码”。

下一章我们会学习：
- 实战项目
- 小型命令行程序
- 任务队列
- 文本处理
- 线程同步

这部分会把前面所有知识串起来，真正做成可运行的程序。

---

## 第十二节：持续学习建议

现代 C++ 不应该只是“看一眼特性”，而应该在每一次代码实践里真正使用：
- 变量尽量用 `auto`
- 资源尽量用 `unique_ptr`
- 循环尽量用范围 for
- 对象传递尽量用移动语义
- 共享资源必须用 mutex 保护

就像学习任何一门语言一样，现代特性不是“背下来”，而是“自然地写出来”。

下一步：第 5 章进入实战项目，开始把前面的知识都拼接成真正能运行的小程序。
