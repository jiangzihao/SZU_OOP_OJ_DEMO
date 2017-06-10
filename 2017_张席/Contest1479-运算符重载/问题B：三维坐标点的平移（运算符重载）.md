# 问题 B: 三维坐标点的平移（运算符重载）

## 题目描述

定义一个三维点Point类，利用友元函数重载"++"和"--"运算符，并区分这两种运算符的前置和后置运算。

要求如下：
1. 实现Point类；
2. 编写main函数，初始化1个Point对象，将这个对象++或--后赋给另外一个对象，并输出计算后对象的坐标信息。

## 输入

第1行：输入三个int类型的值，分别为一个Point对象p1的x,y,z坐标。

## 输出

第1行：Point对象p1后置++之后的坐标信息输出。
第2行：Point对象p1后置++操作后赋给另外一个Point对象p2的坐标信息。
第3行开始，依次输出前置++，后置--，前置--运算的坐标信息，输出格式与后置++一样。

## 样例输入
```
10 20 30
```

## 样例输出
```
x=11 y=21 z=31
x=10 y=20 z=30
x=11 y=21 z=31
x=11 y=21 z=31
x=9 y=19 z=29
x=10 y=20 z=30
x=9 y=19 z=29
x=9 y=19 z=29
```

## 优秀代码示例
```C++
#include <iostream>
using namespace std;

class Point
{
private:
    int x, y, z;
public:
    Point(int x = 0, int y = 0, int z = 0)
        :x(x), y(y), z(z) {}
    // 前增量最好返回引用
    friend Point& operator ++(Point&);
    friend Point operator ++(Point&, int);
    // 前增量最好返回引用
    friend Point& operator --(Point&);
    friend Point operator --(Point&, int);
    void show() {
        cout <<"x=" <<x <<' ' <<"y=" <<y <<' ' <<"z=" <<z <<endl;
    }
};

Point& operator ++(Point &p) {
    p.x++;
    p.y++;
    p.z++;
    return p;
}

Point& operator --(Point &p) {
    p.x--;
    p.y--;
    p.z--;
    return p;
}

Point operator ++(Point &p, int) {
    Point temp(p);
    ++p;
    return temp;
}

Point operator --(Point &p, int) {
    Point temp(p);
    --p;
    return temp;
}

int main() {
    int x, y, z;
    cin >> x >> y >> z;
    // 用p保存原始对象
    Point p(x, y, z);

    Point p1 = p, p2 = p1++;
    p1.show();
    p2.show();

    p1 = p;
    p2 = ++p1;
    p1.show();
    p2.show();

    p1 = p;
    p2 = p1--;
    p1.show();
    p2.show();

    p1 = p;
    p2 = --p1;
    p1.show();
    p2.show();

    return 0;
}
```