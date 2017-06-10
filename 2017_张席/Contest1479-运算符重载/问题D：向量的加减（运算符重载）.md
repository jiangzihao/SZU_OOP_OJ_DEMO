# 问题 D: 向量的加减（运算符重载）

## 题目描述

设向量X=(x1,x2,…,xn)和Y=(y1,y2…,yn),它们之间的加、减分别定义为：
```
  X+Y=(x1+y1,x2+y2,…,xn+yn)
  X-Y=(x1-y1,x2-y2,…,xn-yn)
```
编程序定义向量类Vector ,重载运算符“+”、“-”,实现向量之间的加、减运算;并编写print函数作为向量的输出操作。
Vector类的基本形式如下：
```C++
class Vector{
int vec[5];
public:
Vector(int v[]);
Vector();
Vector(const Vector& obj);
Vector operator +(const Vector& obj);
Vector operator -(const Vector& obj);
void print();
};
```
要求如下：
1. 实现Vector类；
2. 编写main函数，初始化两个Vector对象的，计算它们之间的加减，并输出结果。

## 输入

第1行：输入5个int类型的值，初始化第一个Vector对象。
第2行: 输入5个int类型的值，初始化第二个Vector对象。

## 输出

第1行：2个Vector对象相加后的输出结果。
第2行：2个Vector对象相减后的输出结果。

## 样例输入
```
-4 1 0 10 5 
-11 8 10 17 -6 
```

## 样例输出
```
-15 9 10 27 -1 
7 -7 -10 -7 11 
```

## 优秀代码示例
```C++
// Author: 2016040187 张凯杰
#include<iostream>
using namespace std;

class Vector
{
    int vec[5];
public:
    Vector(int V[5]) {
        for (int i = 0; i < 5; i++) vec[i] = V[i];
    }
    Vector() {
        for (int i = 0; i < 5; i++) vec[i] = 0;
    }
    Vector(const Vector &a) {
        for (int i = 0; i < 5; i++) vec[i] = a.vec[i];
    }
    Vector operator + (const Vector &a) {
        Vector V;
        for (int i = 0; i < 5; i++) V.vec[i] = vec[i] + a.vec[i];
        return V;
    }
    Vector operator - (const Vector &a) {
        Vector V;
        for (int i = 0; i < 5; i++) V.vec[i] = vec[i] - a.vec[i];
        return V;
    }
    void print() {
        for (int i = 0; i < 5; i++) cout << vec[i] << " ";
        cout << endl;
    }
};
 
int main() {
    int v1[5];

    for (int i = 0; i < 5; i++)
        cin >> v1[i];
    Vector A(v1);

    for (int i = 0; i < 5; i++)
        cin >> v1[i];
    Vector B(v1);

    (A + B).print();
    (A - B).print();
    return 0;
}
```