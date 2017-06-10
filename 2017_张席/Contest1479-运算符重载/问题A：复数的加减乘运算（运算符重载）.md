# 问题 A: 复数的加减乘运算（运算符重载）

## 题目描述

定义一个复数类，通过重载运算符：+、-、*，实现两个复数之间的各种运算。

要求如下：
1. 实现Complex类；
2. 编写main函数，初始化两个Complex对象，计算它们之间的加减乘，并输出结果。
复数相乘的运算规则
设z1=a+bi，z2=c+di(a、b、c、d∈R)是任意两个复数，那么它们的积(a+bi)(c+di)=(ac-bd)+(bc+ad)i.

## 输入

第1行：输入两个数值，分别为第一个Complex对象的实部和虚部。
第2行：输入两个数值，分别为第二个Complex对象的实部和虚部。

## 输出

第1行：两个Complex对象相加后的输出结果。
第2行：两个Complex对象相减后的输出结果。
第3行：两个Complex对象相乘后的输出结果。

## 样例输入
```
10 20
50 40
```

## 样例输出
```
Real=60 Image=60
Real=-40 Image=-20
Real=-300 Image=1400
```

## 优秀代码示例
```C++
// Author: 2016190072 张子垚
#include <iostream>
#include <string>

using namespace std;

class Complex {
private:
    double x, y;
public:
    Complex(double _x, double _y):x(_x),y(_y) {}
    void show() {
        cout << "Real=" << x << " Image=" << y << endl;
    }
    friend Complex operator *(const Complex &t1, const Complex &t2);
    friend Complex operator -(const Complex &t1, const Complex &t2);
    friend Complex operator +(const Complex &t1, const Complex &t2);
};

Complex operator *(const Complex &t1, const Complex &t2) {
    return Complex(t1.x * t2.x - t1.y * t2.y, t1.x * t2.y + t1.y * t2.x);
}

Complex operator +(const Complex &t1, const Complex &t2) {
    return Complex(t1.x + t2.x, t1.y + t2.y);
}

Complex operator -(const Complex &t1, const Complex &t2) {
    return Complex(t1.x - t2.x, t1.y - t2.y);
}

int main() {
    double x, y;
    cin >> x >> y;
    Complex a(x, y);
    cin >> x >> y;
    Complex b(x, y);
    (a + b).show();
    (a - b).show();
    (a * b).show();
    return 0;
}
```