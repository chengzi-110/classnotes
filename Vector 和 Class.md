# Vector 和 Class

---

# 一、Vector（动态数组）

## 什么是 Vector？

`vector` 是 C++ 标准库提供的**动态数组**，大小可以自动扩展，不需要像普通数组一样提前指定长度。

```cpp
#include <vector>
using namespace std;
```

---

## 基本用法

### 创建 vector

```cpp
vector<int> a;                   // 空的 vector
vector<int> b(5);                // 5个元素，初始值都是 0
vector<int> c(5, 10);            // 5个元素，初始值都是 10
vector<int> d = {1, 2, 3, 4, 5}; // 直接初始化
```

### 添加和删除元素

```cpp
vector<int> v = {1, 2, 3};

v.push_back(4);   // 末尾添加：{1, 2, 3, 4}
v.pop_back();     // 删除末尾：{1, 2, 3}
```

### 访问元素

```cpp
vector<int> v = {10, 20, 30};

cout << v[0];       // 10，下标访问（不检查越界）
cout << v.at(1);    // 20，at() 访问（越界会报错，更安全）
cout << v.front();  // 10，第一个元素
cout << v.back();   // 30，最后一个元素
```

### 常用属性

```cpp
vector<int> v = {1, 2, 3, 4, 5};

cout << v.size();    // 5，元素个数
cout << v.empty();   // 0（false），是否为空
v.clear();           // 清空所有元素
```

### 遍历

```cpp
vector<int> v = {1, 2, 3, 4, 5};

// 方式1：下标
for (int i = 0; i < v.size(); i++) {
    cout << v[i] << " ";
}

// 方式2：范围 for（推荐）
for (int x : v) {
    cout << x << " ";
}
```

---

## 对比普通数组

| 特性 | 普通数组 | vector |
|------|---------|--------|
| 大小 | 固定，不能改变 | 动态，可增减 |
| 越界检查 | ❌ 无 | ✅ at() 有 |
| 获取长度 | ❌ 需要手动记 | ✅ .size() |
| 传参 | 需要额外传长度 | 直接传，自带长度 |

---

---

# 二、Class（类）

## 什么是 Class？

`class` 是 C++ 面向对象的核心，用来**把数据和操作数据的函数打包在一起**，描述一类事物的属性和行为。

---

## 基本结构

```cpp
class 类名 {
public:
    // 公开的成员变量和函数（外部可以访问）

private:
    // 私有的成员变量和函数（只有类内部可以访问）
};
```

---

## 示例：定义一个学生类

```cpp
class Student {
public:
    string name;
    int age;

    // 构造函数：创建对象时自动调用
    Student(string n, int a) {
        name = n;
        age = a;
    }

    // 成员函数
    void introduce() {
        cout << "我叫" << name << "，今年" << age << "岁" << endl;
    }
};

int main() {
    Student s("张三", 20);  // 创建对象
    s.introduce();          // 输出：我叫张三，今年20岁
    cout << s.name;         // 输出：张三
}
```

---

## public 和 private

```cpp
class BankAccount {
public:
    string owner;

    void deposit(int amount) {
        balance += amount;  // 可以访问私有变量
    }

    int getBalance() {
        return balance;     // 通过公开函数暴露私有数据
    }

private:
    int balance = 0;        // 余额是私有的，外部不能直接改
};

int main() {
    BankAccount acc;
    acc.owner = "张三";
    acc.deposit(1000);
    cout << acc.getBalance();  // ✅ 输出 1000
    cout << acc.balance;       // ❌ 编译错误！不能直接访问私有变量
}
```

> 把数据设为 `private`，通过公开函数来访问，这叫做**封装**，是面向对象的核心思想之一。

---

## 构造函数和析构函数

```cpp
class MyClass {
public:
    // 构造函数：对象创建时自动调用
    MyClass() {
        cout << "对象创建了" << endl;
    }

    // 析构函数：对象销毁时自动调用
    ~MyClass() {
        cout << "对象销毁了" << endl;
    }
};

int main() {
    MyClass obj;  // 输出：对象创建了
}                 // 函数结束，obj 销毁，输出：对象销毁了
```

---

## Vector 里存 Class 对象

两者可以结合使用：

```cpp
class Student {
public:
    string name;
    int score;
    Student(string n, int s) : name(n), score(s) {}
};

int main() {
    vector<Student> students;

    students.push_back(Student("张三", 90));
    students.push_back(Student("李四", 85));
    students.push_back(Student("王五", 95));

    for (const Student& s : students) {
        cout << s.name << ": " << s.score << endl;
    }
    // 输出：
    // 张三: 90
    // 李四: 85
    // 王五: 95
}
```

---

## 总结

| | vector | class |
|--|--------|-------|
| 是什么 | 动态数组容器 | 自定义数据类型 |
| 作用 | 存储一组数据 | 把数据和函数打包在一起 |
| 关键词 | `push_back` `size` `[]` | `public` `private` 构造函数 |
| 常见组合 | `vector<类名>` 存储一组对象 | — |
