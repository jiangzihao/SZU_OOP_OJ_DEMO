# 问题 A: 圆和圆柱体计算（继承）

## 题目描述

定义一个CPoint点类，包含数据成员x,y（坐标点）。

以CPoint为基类，派生出一个圆形类CCircle，增加数据成员r(半径）和一个计算圆面积的成员函数。

再以CCircle做为直接基类，派生出一个圆柱体类CCylinder，增加数据成员h(高)和一个计算体积的成员函数。

生成圆和圆柱体对象，调用成员函数计算面积或体积并输出结果。

## 输入

输入圆的圆心位置、半径

输入圆柱体圆心位置、半径、高

## 输出

输出圆的圆心位置 半径

输出圆面积

输出圆柱体的圆心位置 半径 高

输出圆柱体体积

## 样例输入
```
0 0 1
1 1 2 3
```

## 样例输出
```
Circle:(0,0),1
Area:3.14
Cylinder:(1,1),2,3
Volume:37.68
```

## 优秀代码示例
```C++
// Author: 2016150043 黄泓凯
#include<iostream>

using namespace std;

// 圆周率
const double PI = 3.14;

// 点类
class CPoint {
protected:
    // 坐标
    double x, y;
public:
    // 构造函数
    CPoint(double x, double y)
        :x(x), y(y) {}
    // 获得横坐标x
    double getX() { return x; }
    // 获得纵坐标y
    double getY() { return y; }
};

// 圆类
class CCircle: public CPoint {
protected:
    // 半径
    double r;
public:
    // 构造函数
    CCircle(double x1, double y1, double r)
        :CPoint(x1, y1), r(r) {}
    // 获得半径r
    double getR() { return r; }
    // 计算面积
    double area() { return PI * r * r; }
};

// 圆柱体类
class CCylinder: public CCircle {
protected:
    // 高
    double h;
public:
    // 构造函数
    CCylinder(double x1, double y1, double r1, double h)
        :CCircle(x1, y1, r1), h(h) {}
    // 获得高h
    double getH() { return h; }
    // 计算体积
    double volume() { return PI * r * r * h; }
};

int main(){
    double x, y, r, h;
    cin >> x >> y >> r;
    // 实例化圆对象
    CCircle circle(x, y, r);
    cout << "Circle:(" << circle.getX() << ',' << circle.getY() << ")," circle.getR() << endl;
    cout << "Area:" << circle.area() << endl;
    cin >> x >> y >> r >> h;
    // 实例化圆柱体对象
    CCylinder cylinder(x, y, r, h);
    cout << "Cylinder:(" << cylinder.getX() << ',' << cylinder.getY() << ')' << cylinder.getR() << ',' << cylinder.getH() << endl;
    cout << "Volume:" << cylinder.volume() << endl;
}
```
