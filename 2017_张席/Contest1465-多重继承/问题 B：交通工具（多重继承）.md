# 问题 B: 交通工具（多重继承）

## 题目描述

1、建立如下的类继承结构：

1)一个车类CVehicle作为基类，具有max_speed、speed、weight等数据成员，display()等成员函数

2)从CVehicle类派生出自行车类CBicycle，添加属性：高度height

3)从CVehicle类派生出汽车类CMotocar，添加属性：座位数seat_num

4)从CBicycle和CMotocar派生出摩托车类CMotocycle

2、分别定义以上类的构造函数、输出函数display及其他函数（如需要）。

3、在主函数中定义各种类的对象，并测试之，通过对象调用display函数产生输出。

## 输入

第一行：最高速度 速度 重量 第二行：高度 第三行：座位数

## 输出

第一行：Vehicle: 第二行及以后各行：格式见Sample

## 样例输入
```
100 60 20
28
2
```

## 样例输出
```
Vehicle:
max_speed:100
speed:60
weight:20

Bicycle:
max_speed:100
speed:60
weight:20
height:28

Motocar:
max_speed:100
speed:60
weight:20
seat_num:2

Motocycle:
max_speed:100
speed:60
weight:20
height:28
seat_num:2
```

## 优秀代码示例
```C++
// Author: 2016180092 蔡业湘
#include <iostream>
#include <string>

using namespace std;

class CVehicle {
public:
    CVehicle(double m, double s, double w): max_speed(m), speed(s), weight(w) {}
    void display() {
        cout << "max_speed:" << max_speed << endl
            << "speed:" << speed << endl
            << "weight:" << weight << endl;
    }
protected:
    double max_speed;
    double speed;
    double weight;
};

class CBicycle: virtual public CVehicle {
public:
    CBicycle(double m, double s, double w, double h): CVehicle(m, s, w), height(h) {}
    void display() {
        cout << "height:" << height << endl;
    }
protected:
    double height;
};

class CMotocar: virtual public CVehicle {
public:
    CMotocar(double m, double s, double w, int seat): CVehicle(m, s, w), seat_num(seat) {}
    void display() {
        cout << "seat_num:" << seat_num << endl;
    }
protected:
    int seat_num;
};

class CMotocycle: public CBicycle, public CMotocar {
public:
    CMotocycle(double m, double s, double w, double h, int seat)
        :CVehicle(m, s, w), CBicycle(m, s, w, h), CMotocar(m, s, w, seat) {}
};

int main() {
    double m, s, w, h;
    int seat;
    cin >> m >> s >> w;
    CVehicle p1(m, s, w);
    cout << "Vehicle:" << endl;
    p1.display();
    cout << endl;
    cin >> h;
    CBicycle p2(m, s, w, h);
    cout << "Bicycle:" << endl;
    p2.CVehicle::display();
    p2.display();
    cout << endl;
    cin >> seat;
    CMotocar p3(m, s, w, seat);
    cout << "Motocar:" << endl;
    p3.CVehicle::display();
    p3.display();
    cout << endl;
    CMotocycle p4(m,s,w,h,seat);
    cout << "Motocycle:" << endl;
    p4.CVehicle::display();
    p4.CBicycle::display();
    p4.CMotocar::display();
    return 0;
}

```