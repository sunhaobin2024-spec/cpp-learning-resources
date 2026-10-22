# 02 面向对象（完整课堂版）

本章目标：
- 理解对象、类、封装、继承和多态的基本概念
- 能定义自己的类，并为类编写构造函数和析构函数
- 能理解 this 指针、访问控制、复制构造和移动语义的基本用途
- 能完成本章练习题，并理解参考答案
- 能把类设计思想应用到后续项目开发中

先决条件：已掌握第 1 章的 C++ 基础语法

---

## 第一节：为什么要学习面向对象？

C++ 不只是“过程式语言”，它支持面向对象编程（OOP）。面向对象的核心思想是：
- 把数据和行为放在一起
- 把复杂问题拆成对象
- 用对象之间的交互来组织程序

例如：
- 学生对象：姓名、年龄、成绩、学习方法
- 车对象：颜色、品牌、速度、启动和刹车
- 用户对象：用户名、密码、权限、登录和退出

这种思维方式让程序更容易维护、更容易扩展，特别适合：
- 游戏开发
- 图形界面
- 工程软件
- 后端系统
- 数据处理平台

---

## 第二节：类与对象的基本概念

### 2.1 类是什么？

类（class）就是“模板”，描述对象的属性和行为。对象（object）是类的一个具体实例。

比如：
```cpp
class Person {
public:
    std::string name;
    int age;
};
```

这里：
- `Person` 是类
- `name` 和 `age` 是成员变量
- `Person p;` 就是一个对象

### 2.2 一个完整的类示例

```cpp
#include <iostream>
#include <string>

class Person {              // 定义一个类 Person
public:                     // public 表示对外公开
    std::string name;        // 成员变量：姓名
    int age;                 // 成员变量：年龄

    void introduce() {       // 成员函数：介绍自己
        std::cout << "My name is " << name << ", I am " << age << " years old.\n";
    }
};

int main() {
    Person p;                // 创建一个 Person 对象 p
    p.name = "Alice";       // 给对象成员赋值
    p.age = 20;             // 给对象成员赋值
    p.introduce();          // 调用成员函数
    return 0;
}
```

### 2.3 逐行讲解

- `class Person { ... };`
  - 定义一个类
  - 类中可以放成员变量和成员函数

- `public:`
  - 公开访问控制，它表示外部代码可以访问这些成员

- `std::string name;`
  - 成员变量：姓名

- `int age;`
  - 成员变量：年龄

- `void introduce() { ... }`
  - 成员函数：输出信息

- `Person p;`
  - 构造一个对象 p

- `p.name = "Alice";`
  - 给对象成员赋值

- `p.introduce();`
  - 调用对象的方法

### 2.4 访问控制说明

在类中常见的访问控制有：
- `public`：对外公开，外部代码可访问
- `private`：私有成员，外部不能直接访问
- `protected`：受保护成员，通常用于继承场景

示例：
```cpp
#include <iostream>
#include <string>

class Person {
private:
    std::string name;  // 私有成员，外部不能直接访问
    int age;           // 私有成员

public:
    void setName(const std::string& n) {
        name = n;
    }

    void setAge(int a) {
        age = a;
    }

    void show() const {
        std::cout << name << " " << age << "\n";
    }
};

int main() {
    Person p;
    p.setName("Bob");
    p.setAge(25);
    p.show();
    return 0;
}
```

说明：
- `private` 把数据隐藏起来
- 这样做更安全，也更符合封装思想

---

## 第三节：构造函数与析构函数

### 3.1 构造函数是什么？

构造函数（constructor）用于在对象创建时初始化成员。它的名字和类名相同，没有返回类型。

```cpp
#include <iostream>
#include <string>

class Person {
private:
    std::string name;
    int age;

public:
    Person() {                  // 默认构造函数
        name = "Unknown";
        age = 0;
    }

    Person(const std::string& n, int a) { // 带参数构造函数
        name = n;
        age = a;
    }

    void show() const {
        std::cout << name << " " << age << "\n";
    }
};

int main() {
    Person p1;                  // 调用默认构造函数
    Person p2("Charlie", 18);  // 调用带参数构造函数
    p1.show();
    p2.show();
    return 0;
}
```

### 3.2 析构函数是什么？

析构函数（destructor）在对象被销毁时自动调用，通常用于释放动态分配的资源。

```cpp
#include <iostream>

class Demo {
public:
    Demo() {
        std::cout << "构造函数被调用\n";
    }

    ~Demo() {  // 析构函数
        std::cout << "析构函数被调用\n";
    }
};

int main() {
    Demo d;  // 创建对象 d，构造函数执行
    return 0; // 函数退出前，d 销毁，析构函数执行
}
```

### 3.3 构造函数初始化列表

更推荐的写法是使用初始化列表：
```cpp
class Person {
private:
    std::string name;
    int age;

public:
    Person() : name("Unknown"), age(0) {
    }

    Person(const std::string& n, int a) : name(n), age(a) {
    }
};
```

好处：
- 效率更高
- 代码更清晰
- 对成员变量初始化更稳定

---

## 第四节：this 指针

this 是一个特殊的指针，指向当前对象本身。它常用于：
- 区分成员变量和参数变量
- 返回当前对象本身
- 链式调用

示例：
```cpp
#include <iostream>

class Counter {
private:
    int value;

public:
    Counter(int v = 0) : value(v) {}

    Counter& add(int delta) {
        value += delta;
        return *this;    // 返回当前对象本身
    }

    void print() const {
        std::cout << value << '\n';
    }
};

int main() {
    Counter c(5);
    c.add(3).add(2).add(1);  // 链式调用
    c.print();                // 输出 11
    return 0;
}
```

### 4.1 为什么需要 this？

因为在函数里，参数和成员变量可能同名。例如：
```cpp
class Person {
private:
    std::string name;

public:
    void setName(const std::string& name) {
        this->name = name; // 区分成员变量和参数变量
    }
};
```

这里 `this->name` 表示成员变量，`name` 表示参数。

---

## 第五节：封装（Encapsulation）

封装的核心就是：
- 把数据和操作数据的方法放在一起
- 对外提供必要接口
- 不让外部随意破坏内部状态

示例：
```cpp
#include <iostream>

class BankAccount {
private:
    int balance;

public:
    BankAccount() : balance(0) {}

    void deposit(int amount) {
        if (amount > 0) {
            balance += amount;
        }
    }

    void withdraw(int amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
        }
    }

    int getBalance() const {
        return balance;
    }
};

int main() {
    BankAccount acc;
    acc.deposit(100);
    acc.withdraw(30);
    std::cout << acc.getBalance() << '\n';
    return 0;
}
```

### 5.1 为什么封装重要？

因为封装让对象更加稳定：
- 保护内部状态
- 限制非法操作
- 增强可维护性
- 更容易维护业务规则

---

## 第六节：继承（Inheritance）

继承表示一种“分类”和“复用”的方式。派生类可以继承基类中的成员并扩展功能。

```cpp
#include <iostream>
#include <string>

class Animal {
public:
    void eat() {
        std::cout << "eat\n";
    }
};

class Dog : public Animal {
public:
    void bark() {
        std::cout << "woof\n";
    }
};

int main() {
    Dog d;
    d.eat();  // 继承自 Animal
    d.bark(); // Dog 自己的方法
    return 0;
}
```

### 6.1 继承的好处

- 代码复用
- 结构逻辑更清晰
- 可以按“概念层次”组织程序

### 6.2 访问控制在继承中的含义

- `public` 继承：基类的 public 成员仍为 public，protected 成员仍为 protected
- `protected` 继承：基类 public 变为 protected
- `private` 继承：基类 public/protected 都变为 private

一般情况下，默认使用 `public` 继承。

---

## 第七节：多态（Polymorphism）

### 7.1 什么是多态？

多态让同一个接口能表现出不同的行为。最典型的方式是虚函数（virtual function）。

```cpp
#include <iostream>

class Base {
public:
    virtual void speak() {  // 使用 virtual 开启动态绑定
        std::cout << "Base\n";
    }

    virtual ~Base() {}  // 虚析构函数，确保派生类资源正确释放
};

class Derived : public Base {
public:
    void speak() override {  // override 表示覆盖基类函数
        std::cout << "Derived\n";
    }
};

int main() {
    Base* b = new Derived();
    b->speak();  // 动态绑定，调用 Derived::speak
    delete b;
    return 0;
}
```

### 7.2 动态绑定的意义

如果没有 virtual，那么调用的是编译期绑定，可能调用的是 Base::speak，而不是派生类中的覆盖实现。

动态绑定让行为根据对象实际类型决定，因此在工程代码中非常关键。

### 7.3 纯虚函数与抽象类

```cpp
class Shape {
public:
    virtual double area() const = 0;  // 纯虚函数
};

class Circle : public Shape {
private:
    double r;

public:
    Circle(double r) : r(r) {}

    double area() const override {
        return 3.14159 * r * r;
    }
};
```

说明：
- 有纯虚函数的类是抽象类
- 抽象类不能实例化对象
- 抽象类常用于设计接口与统一抽象层

---

## 第八节：复制构造与赋值运算符

### 8.1 为什么要学习复制构造？

当对象管理资源时（例如动态分配内存），默认的复制行为可能导致浅拷贝问题。浅拷贝会让多个对象共享同一个资源，导致重复释放或内存错误。

```cpp
#include <iostream>
#include <cstring>

class String {
private:
    char* data;

public:
    String(const char* s) {
        data = new char[std::strlen(s) + 1];
        std::strcpy(data, s);
    }

    // 复制构造函数：深拷贝
    String(const String& other) {
        data = new char[std::strlen(other.data) + 1];
        std::strcpy(data, other.data);
    }

    // 赋值运算符：防止浅拷贝问题
    String& operator=(const String& other) {
        if (this == &other) return *this;
        delete[] data;
        data = new char[std::strlen(other.data) + 1];
        std::strcpy(data, other.data);
        return *this;
    }

    ~String() {
        delete[] data;
    }

    void print() const {
        std::cout << data << '\n';
    }
};

int main() {
    String a("hello");
    String b = a;   // 调用复制构造
    b.print();
    return 0;
}
```

### 8.2 规则：三五法则

如果一个类管理资源，通常需要：
- 复制构造函数
- 复制赋值运算符
- 析构函数

如果你还做了移动语义，那还可能需要：
- 移动构造函数
- 移动赋值运算符

这就是常见的“Rule of Five”。

---

## 第九节：移动语义（C++11 引入）

### 9.1 为什么需要移动语义？

移动语义可以避免不必要的数据拷贝，尤其在传递大对象时会更高效。

```cpp
#include <iostream>
#include <utility>
#include <string>

class BigData {
private:
    std::string data;

public:
    BigData(std::string d) : data(std::move(d)) {
    }

    void print() const {
        std::cout << data << '\n';
    }
};

int main() {
    std::string s = "hello world";
    BigData obj(std::move(s));
    std::cout << s << '\n';  // 这里 s 可能为空，说明内容已转移
    obj.print();
    return 0;
}
```

### 9.2 std::move 的作用

`std::move` 并不“移动对象”，它只是把对象转换成右值引用，表示希望它可以被移动。

使用场景：
- 传递大型对象给函数
- 构造对象时避免复制
- 处理资源管理对象时提高效率

---

## 第十节：常见错误与调试方法

### 10.1 访问控制错误

```cpp
class Person {
private:
    int age;
};

int main() {
    Person p;
    // p.age = 20;  // 编译错误：age 是私有成员，外部不能访问
    return 0;
}
```

说明：
- 访问控制是 OOP 的基本规范
- 必须通过公有接口读写对象状态

### 10.2 析构和复制问题

如果一个类中有 `new`，要特别注意：
- 复制构造是否正确
- 赋值运算符是否正确
- 析构函数是否释放资源

否则可能发生：
- double free
- dangling pointer
- 内存泄漏

### 10.3 虚函数忘记加 `virtual`

```cpp
class Base {
public:
    void speak() { std::cout << "Base\n"; }
};

class Derived : public Base {
public:
    void speak() { std::cout << "Derived\n"; }
};

int main() {
    Base* p = new Derived();
    p->speak();  // 这里调用的是 Base::speak，而不是 Derived::speak
    return 0;
}
```

解决办法：在基类中加上 `virtual`。

---

## 第十一节：本章练习题（含参考答案）

### 练习 1：定义一个简单的 Rectangle 类

要求：
- 有成员变量 `width` 和 `height`
- 有构造函数初始化它们
- 有 `area()` 方法返回面积

参考答案：
```cpp
#include <iostream>

class Rectangle {
private:
    int width;
    int height;

public:
    Rectangle(int w, int h) : width(w), height(h) {}

    int area() const {
        return width * height;
    }
};

int main() {
    Rectangle r(3, 4);
    std::cout << r.area() << '\n';  // 输出 12
    return 0;
}
```

---

### 练习 2：实现一个简单的 Student 类

要求：
- 包含 `name` 和 `score`
- 提供 `setName`、`setScore`、`display` 方法
- 名字和分数必须通过接口访问

参考答案：
```cpp
#include <iostream>
#include <string>

class Student {
private:
    std::string name;
    int score;

public:
    Student(const std::string& n, int s) : name(n), score(s) {}

    void setName(const std::string& n) {
        name = n;
    }

    void setScore(int s) {
        score = s;
    }

    void display() const {
        std::cout << "Name: " << name << ", Score: " << score << '\n';
    }
};

int main() {
    Student s("Alice", 95);
    s.display();
    s.setScore(99);
    s.display();
    return 0;
}
```

---

### 练习 3：实现一个简单的 Shape 继承结构

要求：
- 基类 Shape 有虚函数 `area()`
- 派生类 Circle、Rectangle
- 通过基类指针调用 `area()`，演示多态

参考答案：
```cpp
#include <iostream>

class Shape {
public:
    virtual double area() const = 0;
    virtual ~Shape() = default;
};

class Circle : public Shape {
private:
    double r;

public:
    Circle(double rr) : r(rr) {}

    double area() const override {
        return 3.14159 * r * r;
    }
};

class Rectangle : public Shape {
private:
    double w, h;

public:
    Rectangle(double ww, double hh) : w(ww), h(hh) {}

    double area() const override {
        return w * h;
    }
};

int main() {
    Shape* s1 = new Circle(5.0);
    Shape* s2 = new Rectangle(3.0, 4.0);

    std::cout << s1->area() << '\n';
    std::cout << s2->area() << '\n';

    delete s1;
    delete s2;
    return 0;
}
```

---

### 练习 4：深入理解复制构造

要求：
- 设计一个 `String` 类，管理动态字符数组
- 实现复制构造函数和赋值运算符
- 证明它不会发生浅拷贝错误

参考答案：
```cpp
#include <iostream>
#include <cstring>

class String {
private:
    char* data;

public:
    String(const char* s) {
        data = new char[std::strlen(s) + 1];
        std::strcpy(data, s);
    }

    String(const String& other) {
        data = new char[std::strlen(other.data) + 1];
        std::strcpy(data, other.data);
    }

    String& operator=(const String& other) {
        if (this == &other) return *this;
        delete[] data;
        data = new char[std::strlen(other.data) + 1];
        std::strcpy(data, other.data);
        return *this;
    }

    ~String() {
        delete[] data;
    }

    void print() const {
        std::cout << data << '\n';
    }
};

int main() {
    String a("hello");
    String b = a;   // 复制构造
    b.print();
    return 0;
}
```

---

### 练习 5：联合使用继承与多态

要求：
- 假设有一个动物父类，`Animal` 有 `voice()` 虚函数
- `Dog` 和 `Cat` 继承 Animal
- 创建一个 `Animal*` 数组，存放不同动物对象并调用 `voice()`

参考答案：
```cpp
#include <iostream>

class Animal {
public:
    virtual void voice() const = 0;
    virtual ~Animal() = default;
};

class Dog : public Animal {
public:
    void voice() const override {
        std::cout << "Woof!\n";
    }
};

class Cat : public Animal {
public:
    void voice() const override {
        std::cout << "Meow!\n";
    }
};

int main() {
    Animal* pets[2];
    pets[0] = new Dog();
    pets[1] = new Cat();

    for (int i = 0; i < 2; ++i) {
        pets[i]->voice();
    }

    delete pets[0];
    delete pets[1];
    return 0;
}
```

---

## 第十二节：第 2 周学习计划（课程版）

目标：在 7 天内掌握类、对象、封装、继承和多态，并完成全部练习。

### 第 1 天：类与对象
- 学习类的定义
- 学习成员变量、成员函数
- 自己写一个 `Person` 类

### 第 2 天：封装与访问控制
- 理解 `public` / `private` / `protected`
- 编写一个银行账户类

### 第 3 天：构造函数与析构函数
- 学习对象初始化和清理
- 练习：写 `Student` 或 `Rectangle` 类

### 第 4 天：继承与多态
- 学习基类/派生类
- 学习 `virtual` 和 `override`
- 练习：写 `Shape` 继承结构

### 第 5 天：复制构造与赋值
- 学习浅拷贝和深拷贝
- 自己实现 `String` 类

### 第 6 天：移动语义与 RAII
- 学习 `std::move`
- 了解智能指针和资源管理

### 第 7 天：综合复盘
- 完成全部练习题
- 从零重写 3 个类
- 记录不理解的点，作为下一章学习前的预热

---

## 第十三节：本章小结

这一章的重点是：
- 类是对象的模板
- 对象是类的实例
- 封装让数据更安全
- 继承让代码更可复用
- 多态让程序更灵活
- 构造/析构处理对象生命周期
- 复制和移动语义处理资源管理问题

如果你能做到：
- 会写一个类
- 会写构造函数
- 会写继承和多态
- 能解释深拷贝和浅拷贝

那么你已经从“会写函数的小程序员”走到了“会设计对象的程序员”这一阶段。

下一章我们将学习：
- STL 容器
- vector / string / map / set
- 常用算法
- 词频统计和排序

这些内容会更偏实战，特别适合你提升代码能力与算法思维。

---

## 第十四节：持续学习建议

提醒自己：
- OOP 不是背书，而是设计
- 能把现实中的对象映射到类很重要
- 类越小越好，每个类都应该职责单一
- 代码应优先写清晰和可维护，而不是炫技

面向对象的学习，不是一口气全部懂，而是通过不断写类、设计对象、修正设计，慢慢形成“对象视角”。

下一步：继续第 3 章 STL 与容器，进入更实战的编程场景。
