# 问题 A: 图形面积（虚函数与多态）

## 题目描述

编写一个程序，定义抽象基类Shape，在Shape类中定义虚函数Area()；由它派生出3个派生类：Circle(圆形)、Square(正方形)、Rectangle(矩形)。用虚函数分别计算几种图形面积。
1、要求输出结果保留两位小数。
2、要求用基类指针数组，使它每一个元素指向每一个派生类对象。

## 输入

测试数据的组数 t

第一组测试数据中圆的半径

第一组测测试数据中正方形的边长

第一组测试数据中矩形的长、宽

.......

第 t 组测试数据中圆的半径

第 t 组测测试数据中正方形的边长

第 t 组测试数据中矩形的长、宽

## 输出

第一组数据中圆的面积

第一组数据中正方形的面积

第一组数据中矩形的面积

......

第 t 组数据中圆的面积

第 t 组数据中正方形的面积

第 t 组数据中矩形的面积

## 样例输入
```
2
1.2
2.3
1.2 2.3
2.1
3.2
1.23 2.12
```

## 样例输出
```
4.52
5.29
2.76
13.85
10.24
2.61
```

## 优秀代码示例
```C++
#include <iostream>
#include <iomanip>
#include <string>

using namespace std;

#define PI 3.14

class Shape {
public:
    // 纯虚函数
    virtual void area() = 0;
    // 作为基类需将析构函数虚拟化
    virtual ~Shape() {}
};

class Circle: public Shape {
private:
    double r;
public:
    Circle(double radius): r(radius) {}
    void area() {
        cout << fixed << setprecision(2) << r * r * PI << endl;
    }
    ~Circle() {};
};

class Square: public Shape {
private:
    double w;
public:
    Square(double width): w(width) {}
    void area() {
        cout << fixed << setprecision(2) << w * w << endl;
    }
    ~Square() {}
};

class Rectangle: public Shape {
private:
    double w, h;
public:
    Rectangle(double width, double height): w(width), h(height) {}
    void area () {
        cout << fixed << setprecision(2) << w * h << endl;
    }
    ~Rectangle() {}
};

int main () {
    int t;
    cin >> t;
    while (t--) {
        double r;
        double w, h;
        // 指针数组
        Shape *p[3];
        cin >> r;
        p[0] = new Circle(r);
        p[0]->area();
        cin >> w;
        p[1] = new Square(w);
        p[1]->area();
        cin >> w >> h;
        p[2] = new Rectangle(w, h);
        p[2]->area();
        delete p[0];
        delete p[1];
        delete p[2];
    }
    return 0;
}
```