# 01 基础语法（入门）

本章目标：了解 C++ 的基本语法、编译流程、基本数据类型、输入输出、条件与循环、函数与数组。每节后面都有示例代码与练习题。

## 1.1 开发环境与编译
- 推荐编译器：g++, clang++（Linux/macOS）、MSVC（Windows）
- 编译示例：
  - g++ main.cpp -o main
  - ./main

## 1.2 第一个程序
示例：hello.cpp
```cpp
#include <iostream>

int main() {
    std::cout << "Hello, C++!" << std::endl;
    return 0;
}
```

## 1.3 基本数据类型
- 整数：int, long, long long
- 浮点：float, double
- 字符：char
- 布尔：bool
- 字符串：std::string（需要 #include <string>）

示例：
```cpp
#include <iostream>
#include <string>

int main() {
    int a = 10;
    double b = 3.14;
    std::string s = "C++";
    bool ok = true;
    std::cout << a << ", " << b << ", " << s << ", " << ok << '\n';
}
```

## 1.4 条件与循环
- if / else
- switch
- for, while, do-while

示例（计算 1..n 的和）：
```cpp
#include <iostream>
int main() {
    int n; std::cin >> n;
    int sum = 0;
    for (int i = 1; i <= n; ++i) sum += i;
    std::cout << sum << '\n';
}
```

## 1.5 函数与作用域
```cpp
#include <iostream>

int add(int x, int y) {
    return x + y;
}

int main() {
    std::cout << add(2, 3) << '\n';
}
```

## 1.6 数组与向量（简要）
- C 风格数组：int a[10];
- 推荐使用 std::vector（需 #include <vector>）

示例：
```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> v = {1,2,3,4};
    for (int x : v) std::cout << x << ' ';
}
```

## 练习题
1. 写一个程序读入两个整数并输出它们的和。
2. 读入 n（n<=100），输出前 n 个自然数的平方。
3. 判断一个数是否是素数（试写一个简单的 O(sqrt(n)) 解法）。

---
