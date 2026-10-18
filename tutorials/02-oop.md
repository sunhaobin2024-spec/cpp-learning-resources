# 02 面向对象（类与对象）

本章目标：掌握类的定义、构造函数、析构函数、访问控制（public/private/protected）、继承、多态与虚函数。

## 2.1 类的定义与对象
```cpp
#include <string>
#include <iostream>

class Person {
public:
    std::string name;
    int age;
    Person(const std::string& n, int a): name(n), age(a) {}
    void say() const { std::cout << name << " " << age << '\n'; }
};

int main() {
    Person p("Alice", 20);
    p.say();
}
```

## 2.2 构造与析构
- 构造函数：用于初始化对象
- 析构函数：对象销毁时自动调用，用于释放资源

## 2.3 继承与访问控制
- public 继承使基类 public 成员在派生类中仍为 public

示例：
```cpp
#include <iostream>

class Animal {
public:
    void eat() { std::cout << "eat\n"; }
};

class Dog : public Animal {
public:
    void bark() { std::cout << "woof\n"; }
};

int main() {
    Dog d; d.eat(); d.bark();
}
```

## 2.4 多态与虚函数
- 基类指针/引用指向派生类对象
- virtual 关键字用于启用运行时多态

示例：
```cpp
#include <iostream>

class Base {
public:
    virtual void speak() { std::cout << "Base\n"; }
    virtual ~Base() {}
};

class Derived : public Base {
public:
    void speak() override { std::cout << "Derived\n"; }
};

int main() {
    Base* b = new Derived();
    b->speak(); // 输出 Derived
    delete b;
}
```

## 2.5 复制控制（拷贝构造、拷贝赋值、移动语义 简介）
- 若类管理资源（如动态内存），需定义拷贝/移动构造与赋值运算符
- 推荐使用 RAII（资源获取即初始化）和智能指针管理资源

## 练习题
1. 实现一个简单的字符串类（管理 char*），实现构造、析构、拷贝构造、拷贝赋值。
2. 实现一个基类 Shape（带虚函数 area()），派生 Circle 和 Rectangle，写一个函数计算多形态数组中所有形状的总面积。

---
