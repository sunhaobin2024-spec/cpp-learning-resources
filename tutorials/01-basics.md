# 01 基础语法（完整课堂版）

本章目标：
- 能搭建 C++ 开发环境并编译运行程序
- 理解并掌握 C++ 的程序结构和第一段程序
- 熟悉基本数据类型、输入输出、条件语句、循环、函数、数组和 std::vector
- 能独立完成本章练习题，并理解参考答案

先决条件：无

---

## 第一节：为什么学习 C++？

C++ 是一门通用编程语言，既有高级语言的易读性，也有底层控制能力。它广泛用于：
- 游戏开发
- 图形界面程序
- 操作系统和系统软件
- 服务器后端
- 编译器与引擎
- 算法竞赛

学习 C++ 不是为了“看起来高级”，而是因为它能让你掌握：
- 程序执行流程
- 内存与资源管理
- 面向对象设计
- 高性能代码的思维方式

---

## 第二节：开发环境与编译流程

### 2.1 常见开发环境

- Windows：Visual Studio / MinGW
- macOS：Xcode / clang++
- Linux：g++

### 2.2 编译与运行示例

```bash
# 这条命令表示：用 g++ 编译 main.cpp 文件，输出名为 main 的可执行程序
# -o 表示指定输出文件名
# 如果我们在当前目录执行 ./main，就会运行这个程序
# 这一步是 C++ 程序从源代码变成可执行文件的核心过程
g++ main.cpp -o main

# 这条命令表示：在当前目录运行生成的程序
./main
```

### 2.3 运行流程理解

源代码（main.cpp）
  ↓
编译器（g++ / clang++ / MSVC）
  ↓
可执行文件（main.exe / main）
  ↓
操作系统执行

理解这条链路很重要，因为后面所有的程序问题，本质上都属于：
- 编译问题
- 运行时问题
- 逻辑问题

---

## 第三节：第一段程序 Hello World

### 3.1 代码示例

```cpp
#include <iostream>        // 引入标准输入输出库，允许使用 std::cout 和 std::cin

int main() {                // 程序的入口函数，所有 C++ 程序都从这里开始执行
    std::cout << "Hello, C++!" << std::endl;  // 输出字符串到屏幕，并换行
    return 0;               // 返回 0 表示程序正常结束，退出状态为成功
}                           // main 函数结束
```

### 3.2 逐行讲解

1. `#include <iostream>`
   - 这是一个预处理指令
   - 作用：把标准库中的 iostream 头文件引入进来
   - 这样我们才能用 `std::cout` 输出内容

2. `int main() {`
   - `main` 是程序的入口函数
   - `int` 表示函数返回一个整数
   - 每个 C++ 程序必须有一个 `main`

3. `std::cout << "Hello, C++!" << std::endl;`
   - `std::cout`：标准输出流，表示屏幕输出
   - `<<`：插入运算符，把右边内容送到输出流中
   - `"Hello, C++!"`：字符串字面量
   - `std::endl`：输出换行并刷新流

4. `return 0;`
   - 这是函数返回语句
   - 0 是常见约定，表示“程序正常退出”

### 3.3 你可以这样理解

你可以把程序看成一个执行器：
- 进入 `main`
- 做一些事情
- 返回一个状态码

C++ 程序的本质就是：
- 接收输入
- 处理数据
- 输出结果

---

## 第四节：基本数据类型与变量

### 4.1 常用数据类型

```cpp
#include <iostream>            // 引入输入输出流
#include <string>              // 引入字符串类型

int main() {                   // 程序入口
    int age = 18;              // 整型变量，存储整数，例子里是 18
    double score = 98.5;       // 双精度浮点数，适合存放小数
    char ch = 'A';             // 字符类型，单引号包裹
    bool ok = true;            // 布尔类型，只有 true 或 false
    std::string name = "Tom"; // 字符串类型，双引号包裹

    std::cout << age << ", " << score << ", " << ch << ", " << ok << ", " << name << '\n';
    // 第一行输出：age、score、ch、ok、name 的内容
    // '\n' 表示换行，等价于换行符
    return 0;                  // 返回 0，表示程序正常结束
}                              // main 函数结束
```

### 4.2 数据类型说明

- `int`：整数，例如 1, 10, -5
- `double`：小数，例如 3.14, 99.99
- `char`：单个字符，例如 'A', 'b', '9'
- `bool`：布尔值，只有 `true` 和 `false`
- `std::string`：字符串，适合处理文本

### 4.3 变量命名规则

- 只能包含字母、数字、下划线
- 不能以数字开头
- 尽量用有意义的名字，比如 `score`, `name`, `total`
- 命名建议：`studentAge`、`totalScore` 这种写法更容易阅读

---

## 第五节：输入输出（cin / cout）

### 5.1 读入两个整数并输出和

```cpp
#include <iostream>            // 引入输入输出功能

int main() {                   // 程序入口
    int a;                     // 定义第一个整数变量 a
    int b;                     // 定义第二个整数变量 b

    std::cin >> a >> b;        // 从标准输入读入两个整数，空格或回车分割
    std::cout << "sum = " << (a + b) << '\n';
    // 输出字符串 "sum = "，再输出 a + b 的结果，最后换行
    return 0;                  // 返回 0，正常结束
}                              // 结束 main
```

### 5.2 说明

- `std::cin`：标准输入流，通常来自键盘
- `>>`：提取运算符，从输入流中读出数据
- `std::cout`：标准输出流，通常显示在屏幕上
- `<<`：插入运算符，把数据写入输出流

### 5.3 代码练习

```cpp
#include <iostream>              // 引入输出流头文件
#include <string>                // 引入字符串类型

int main() {                     // 程序入口
    int age;                     // 定义年龄变量
    std::string name;            // 定义名字变量

    std::cout << "请输入你的名字：";  // 提示用户输入名字
    std::cin >> name;                  // 读取名字

    std::cout << "请输入你的年龄：";  // 提示用户输入年龄
    std::cin >> age;                   // 读取年龄

    std::cout << "你好，" << name << "，你今年 " << age << " 岁。" << '\n';
    // 输出最终结果：你好，名字，你今年 x 岁
    return 0;                          // 程序正常退出
}                                      // 主函数结束
```

---

## 第六节：条件语句（if / else / switch）

### 6.1 if / else 示例

```cpp
#include <iostream>          // 引入输入输出功能

int main() {                 // 程序入口
    int x = 10;              // 定义变量 x

    if (x > 5) {             // 如果 x 大于 5
        std::cout << "x > 5\n";  // 输出 x > 5
    } else if (x == 5) {     // 否则如果 x 等于 5
        std::cout << "x == 5\n"; // 输出 x == 5
    } else {                 // 其他情况
        std::cout << "x < 5\n";  // 输出 x < 5
    }

    return 0;                // 程序正常结束
}                           // 函数结束
```

### 6.2 switch 示例

```cpp
#include <iostream>             // 引入输入输出

int main() {                    // 程序入口
    int n = 2;                  // 定义变量 n

    switch (n) {                // 根据 n 的值进入不同分支
        case 1:                // 当 n == 1 时执行
            std::cout << "one\n";  // 输出 one
            break;                   // 跳出 switch
        case 2:                // 当 n == 2 时执行
            std::cout << "two\n";  // 输出 two
            break;                   // 跳出 switch
        default:               // 以上都不匹配时执行
            std::cout << "other\n"; // 输出 other
            break;                   // 结束 switch
    }

    return 0;                  // 返回 0 退出程序
}                             // 主函数结束
```

### 6.3 条件语句要点

- `if` 适合判断范围和逻辑复杂条件
- `switch` 适合固定值判断，比如星期、菜单选择、状态码
- `break` 非常重要，避免“穿透”到后面的 case

---

## 第七节：循环（for / while / do-while）

### 7.1 for 循环

```cpp
#include <iostream>           // 引入输出流

int main() {                  // 程序入口
    for (int i = 0; i < 5; ++i) {  // 初始化 i=0，循环条件 i<5，每次循环后 i++
        std::cout << i << ' ';     // 输出当前 i 的值，后面跟一个空格
    }
    std::cout << '\n';         // 输出换行，让结果更整齐
    return 0;                 // 程序正常结束
}                            // 结束 main
```

### 7.2 while 循环

```cpp
#include <iostream>           // 引入输出流

int main() {                  // 程序入口
    int i = 0;                // 初始化循环变量

    while (i < 5) {           // 只要 i < 5 就继续执行循环
        std::cout << i << ' '; // 输出当前 i
        ++i;                  // 让 i 自增，避免死循环
    }

    std::cout << '\n';        // 换行输出
    return 0;                // 结束程序
}                           // 结束 main
```

### 7.3 do-while 循环

```cpp
#include <iostream>              // 包含 iostream

int main() {                     // 程序入口
    int i = 0;                   // 初始值

    do {                         // 先执行一次循环体
        std::cout << i << ' ';   // 输出当前 i
        ++i;                    // 自增
    } while (i < 5);             // 循环继续条件：i < 5

    std::cout << '\n';          // 换行
    return 0;                   // 正常退出
}                              // 主函数结束
```

### 7.4 什么时候用哪个循环？

- `for`：循环次数明确，最常见
- `while`：循环次数不固定，依赖条件
- `do-while`：至少执行一次

---

## 第八节：函数（定义、参数、返回）

### 8.1 简单函数示例

```cpp
#include <iostream>               // 引入输出流

int add(int a, int b) {          // 定义函数 add，接收两个 int 参数，返回 int
    return a + b;                // 把 a + b 的结果返回给调用方
}

int main() {                     // 程序入口
    int result = add(3, 4);      // 调用 add(3, 4) ，得到 7
    std::cout << result << '\n'; // 输出 7
    return 0;                    // 程序正常结束
}                               // 主函数结束
```

### 8.2 引用传参示例

```cpp
#include <iostream>              // 输入输出头文件

void inc(int &x) {              // 这里 x 是引用参数，意味着修改的是原变量
    x = x + 1;                  // 给 x 加一
}

int main() {                    // 程序入口
    int value = 5;              // 定义一个整数
    inc(value);                  // 调用 inc，传递 value 的引用
    std::cout << value << '\n'; // 输出 6
    return 0;                   // 退出程序
}                              // 结束 main
```

### 8.3 函数的重要性

函数可以把代码分成更小的模块：
- 更好阅读
- 更易维护
- 更容易复用
- 更容易调试

---

## 第九节：数组和 std::vector

### 9.1 C 风格数组

```cpp
#include <iostream>          // 输入输出头文件

int main() {                 // 程序入口
    int arr[5] = {1, 2, 3, 4, 5};  // 定义一个长度为 5 的整数数组

    for (int i = 0; i < 5; ++i) {   // 从 0 到 4 遍历数组下标
        std::cout << arr[i] << ' ';  // 输出 arr[i] 的值
    }

    std::cout << '\n';        // 换行
    return 0;                // 程序正常退出
}                           // end main
```

### 9.2 vector 示例（推荐）

```cpp
#include <iostream>                // 输入输出头文件
#include <vector>                  // 引入动态数组 vector

int main() {                       // 程序入口
    std::vector<int> v;            // 定义一个空的 int 向量
    v.push_back(10);               // 在尾部插入 10
    v.push_back(20);               // 在尾部插入 20
    v.push_back(30);               // 在尾部插入 30

    for (int x : v) {               // 范围 for 遍历 v 中的每一个元素
        std::cout << x << ' ';      // 输出元素 x
    }

    std::cout << '\n';             // 换行
    return 0;                     // 退出程序
}                                // 结束 main
```

### 9.3 为什么推荐 vector？

- 自动管理内存
- 长度可动态变化
- 更安全、更方便
- 更现代、更符合 C++ 风格

---

## 第十节：常见错误与调试思路

### 10.1 未初始化变量

```cpp
#include <iostream>

int main() {
    int x;        // 未初始化的变量，值不确定
    std::cout << x << '\n';
    return 0;
}
```

说明：上面的代码有未定义行为，可能输出随机值。必须在使用前进行初始化。

### 10.2 数组越界

```cpp
#include <iostream>

int main() {
    int arr[3] = {1, 2, 3};
    std::cout << arr[10] << '\n';  // 越界访问，风险很高，可能导致崩溃或随机错误
    return 0;
}
```

说明：数组下标必须在合法范围内，越界属于典型错误。

### 10.3 输入失败

```cpp
#include <iostream>

int main() {
    int x;
    std::cin >> x;          // 如果输入不是整数，读入会失败
    if (std::cin.fail()) {  // 检查上一次输入是否失败
        std::cout << "输入错误\n";
        return 0;
    }
    std::cout << x << '\n';
    return 0;
}
```

调试建议：
- 先读错误信息
- 再用最小例子验证
- 再用断点/打印语句定位

---

## 第十一节：本章练习题（含参考答案）

### 练习 1：输入两个整数，输出和

题目：
```text
输入：3 5
输出：8
```

参考答案：
```cpp
#include <iostream>       // 引入输入输出头文件

int main() {              // 程序入口
    int a, b;             // 定义两个整数变量
    std::cin >> a >> b;   // 读入两个整数
    std::cout << a + b << '\n';  // 输出它们的和并换行
    return 0;             // 正常退出
}                        // 结束主函数
```

### 练习 2：输出前 n 个自然数的平方

题目：
```text
输入：5
输出：
1
4
9
16
25
```

参考答案：
```cpp
#include <iostream>         // 引入输入输出功能

int main() {                // 程序入口
    int n;                  // 定义 n
    std::cin >> n;          // 读取 n

    for (int i = 1; i <= n; ++i) { // 从 1 到 n 循环
        std::cout << i * i << '\n'; // 输出 i 的平方并换行
    }

    return 0;               // 正常退出
}                          // 结束 main
```

### 练习 3：判断一个数是否是素数

参考答案：
```cpp
#include <iostream>             // 引入输入输出
#include <cmath>                // 引入 sqrt

bool isPrime(int n) {          // 定义判断函数，返回是否为素数
    if (n <= 1) return false;  // 1 及以下都不是素数
    if (n <= 3) return true;   // 2 和 3 是素数
    if (n % 2 == 0) return false; // 偶数不是素数，且 2 已处理

    int limit = static_cast<int>(std::sqrt(n)); // 计算平方根，作为判断上限
    for (int i = 3; i <= limit; i += 2) { // 只测奇数因子
        if (n % i == 0) return false; // 如果能整除，则不是素数
    }

    return true; // 其余情况都是素数
}

int main() {                   // 程序入口
    int x;                     // 定义待判断数字
    std::cin >> x;             // 读取 x
    std::cout << (isPrime(x) ? "YES" : "NO") << '\n';
    // 如果 isPrime(x) 为 true，输出 YES，否则输出 NO
    return 0;                 // 程序正常结束
}                             // 结束 main
```

### 练习 4：计算平均值

参考答案：
```cpp
#include <iostream>                     // 输入输出
#include <vector>                       // 动态数组
#include <iomanip>                      // 设置输出格式

int main() {                           // 程序入口
    int n;                             // 多少个数
    std::cin >> n;                     // 读入 n

    std::vector<double> arr(n);        // 创建长度为 n 的 double 数组
    double sum = 0.0;                  // 求和变量

    for (int i = 0; i < n; ++i) {      // 循环读取每个数
        std::cin >> arr[i];            // 读入第 i 个数
        sum += arr[i];                 // 累加到 sum
    }

    double avg = (n == 0) ? 0.0 : sum / n;  // 计算平��值，避免除零
    std::cout << std::fixed << std::setprecision(2) << avg << '\n';
    // 使用固定小数位输出，保留两位小数
    return 0;                         // 正常退出
}                                    // 结束 main
```

### 练习 5：单词统计

参考答案：
```cpp
#include <iostream>                     // 输入输出
#include <unordered_map>                // 哈希表
#include <string>                       // 字符串类型

int main() {                           // 程序入口
    std::unordered_map<std::string, int> cnt; // 用哈希表统计单词频率
    std::string word;                   // 每个单词

    while (std::cin >> word) {          // 只要还能读到单词就持续统计
        ++cnt[word];                   // 统计当前单词出现次数
    }

    for (const auto &pair : cnt) {      // 遍历哈希表中所有键值对
        std::cout << pair.first << " " << pair.second << '\n';
        // 输出单词和它出现的次数
    }

    return 0;                          // 正常结束
}                                     // 结束 main
```

---

## 第十二节：第 1 周学习计划（课程版）

目标：用 7 天把本章核心知识吃透。每次学习建议 60–120 分钟，最好写代码实践，不只是看讲解。

### 第 1 天：环境与 Hello World
- 安装编译器
- 写出第一个 Hello World
- 学会 g++ 编译
- 思考：程序入口函数为什么必须叫 main？

### 第 2 天：变量与数据类型
- 练习 int / double / char / bool / string
- 练习：输入姓名、年龄并输出

### 第 3 天：输入输出与条件语句
- 学习 cin / cout
- 学习 if / else / switch
- 按练习 1 和 2 实战

### 第 4 天：循环
- 学会 for / while / do-while
- 练习：打印 1 到 10，求和，判断质数

### 第 5 天：函数
- 学习函数定义、参数传递、返回值
- 写练习：求两个数最大值、是否为偶数

### 第 6 天：数组与 vector
- 学习数组和 vector
- 练习：求数组最大值、平均值

### 第 7 天：综合复盘
- 做本章所有练习
- 复盘每个知识点
- 尝试写一个 mini 程序：学生成绩管理系统（非常简单版）

---

## 第十三节：本章小结

这一章你需要掌握的核心知识：
- 程序结构：#include + int main + return 0
- 数据类型：int / double / char / bool / string
- 输入输出：cin / cout
- 条件语句：if / switch
- 循环：for / while / do-while
- 函数：定义、调用、参数传递
- 容器：数组、vector
- 调试：初始化、越界和输入失败

最重要的是：理论要懂，代码必须会手敲。

如果你可以把每个例子自己重新写一遍，并把练习题独立做出来，那么这章就算掌握了。

---

## 第十四节：下一步说明

下一章我们要学习：
- 类与对象
- 成员函数
- 构造函数
- 析构函数
- 继承和多态

你会在下一章看到更像“真正编程”的内容：
- 程序结构从过程式进入面向对象
- 代码组织更清晰
- 资源管理更规范
- 程序更容易扩展

如果你愿意，我下一步就直接继续把第 2 章也写成同样风格的完整版：
- 学习目标
- 中文逐行注释代码
- 代码讲解
- 参考答案
- 每天学习计划

我会继续按“完整课堂版”为你补齐后续章节。