# 问题 B: 虚拟电话（构造与析构）

## 题目描述

虚拟电话包含属性：电话号、状态、机主姓名。
1、电话号是一个类，它包含号码和类型，其中号码是整数类型，类型用单个字母表示用户类别，A表示政府，B表示企业、C表示个人。类操作包括构造、属性的获取和设置等方法，根据需要自行编写。
2、状态用一个数字表示，1表示在用，0表示未用，
3、机主姓名是一个字符串
电话操作包括：构造、析构、打印和查询。
1、构造函数需要考虑复合类成员的构造，并且输出提示信息。假设电话号码为12345678，则构造函数输出"12345678 constructed."
2、打印是输出电话的相关信息，其中如果电话状态是在用则输出use；状态是未用则输出unuse，输出格式看示例。
3、析构函数是输出提示信息。假设电话号为12345678，则析构函数输出"12345678 destructed. "
4、查询操作是根据给定的号码查询电话，如果电话自身号码和给定号码不相同，则返回0；如果电话自身号码和给定号码相同，则返回1
用C++和面向对象思想实现以下要求：
1、输入相关数据，创建三个电话对象，并通过构造方法初始化。
2、输入若干个电话号码，通过查询操作查询这些号码是否在三个电话对象中，如果不存在输出"wrong number."，存在则调用打印操作输出电话信息，具体看输出样例。

## 输入

头三行输入三个电话信息，每行包括电话号码、电话类型、状态、机主姓名

接着一行输入t，表示有t个号码要查询

接着t行输入t个电话号码

## 输出

t行输出t个号码的查询结果

## 样例输入
```
80000001 A 1 tom
80000002 B 0 ken
80000003 C 1 mary
3
50000002
80000003
80000002
```

## 样例输出
```
80000001 constructed.
80000002 constructed.
80000003 constructed.
wrong number.
Phone=80000003--Type=C--State=use--Owner=mary
Phone=80000002--Type=B--State=unuse--Owner=ken
80000003 destructed.
80000002 destructed.
80000001 destructed.
```

## 优秀代码示例
```C++
#include <iostream>
#include <string>

using namespace std;

#define NUM 3

// 电话号类
class TelNumber {
private:
    int number;
    char type;
public:
    TelNumber(int number, char type):number(number), type(type) {}
    int getNumber() {
        return number;
    }
    char getType() {
        return type;
    }
};

// 虚拟电话类
class VirtualTel {
private:
    TelNumber number;
    int status;
    string name;
public:
    // 构造函数
    VirtualTel(int telNum, char type, int status, string name)
        :number(telNum, type), status(status), name(name) {
        cout << number.getNumber() << " constructed." << endl;
    }
    ~VirtualTel() {
        cout << number.getNumber() << " destructed." << endl;
    }
    // 检查输入是否与号码相同
    int checkNumber(int telNumber) {
        return number.getNumber() == telNumber;
    }
    // 输出信息
    void print() {
        cout << "Phone=" << number.getNumber() << "--Type=" << number.getType() << "--State=";
        if (status) cout << "use";
        else cout << "unuse";
        cout << "--Owner=" << name << endl;
    }
};

int main () {
    int number, status;
    char type;
    string name;
    int i;
    // 利用指针数组创建对象
    VirtualTel *virtualTels[3];
    for (i = 0; i < NUM; i++) {
        cin >> number >> type >> status >> name;
        virtualTels[i] = new VirtualTel(number, type, status, name);
    }
    int t;
    cin >> t;
    while (t--) {
        // 要查询的号码
        int numberChecked;
        cin >> numberChecked;
        // 标志变量flag，用于判断是否查询成功
        int flag = 0;
        for (i = 0; i < NUM; i++) {
            if (virtualTels[i]->checkNumber(numberChecked)) {
                virtualTels[i]->print();
                flag = 1;
            }
        }
        if (!flag) cout << "wrong number." << endl;
    }
    // 倒序释放
    for (i = NUM - 1; i >= 0; i--) delete virtualTels[i];
    return 0;
}
```
