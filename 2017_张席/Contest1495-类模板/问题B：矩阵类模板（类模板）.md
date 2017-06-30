# 问题 B: 矩阵类模板（类模板）

## 题目描述

设计一个矩阵类模板Matrix，支持任意数据类型的数据。

要求至少包含2个成员函数：矩阵转置函数transport、以及打印输出函数print

编写main函数进行测试，调用类的成员函数完成转置和输出。

## 输入

第一行先输入t，表示有t个测试用例

从第二行开始输入每个测试用例的数据。

首先输入数据类型，I表示int，D表示double，C表示char，接着输入两个参数m和n，分别表示矩阵的行和列

接下来输入矩阵的元素，一共m行，每行n个数据

## 输出

输出转置后的矩阵

## 样例输入
```
2
I 2 3
1 2 3
4 5 6
C 3 3
a b c
d e f
g h i
```

## 样例输出
```
1 4
2 5
3 6
a d g
b e h
c f i
```

## 优秀代码示例
```C++
// Author: 2016150128 纪静敏
#include<iostream>

using namespace std;

template<class T1>
class Matrix {
protected:
    T1 **p;
    T1 **q;
    int m, n;
public:
    Matrix(int x, int y) {
        m = x;
        n = y;
        p = new T1*[m];
        for (int i = 0; i < m; i++)
            p[i] = new T1[n];
        for (int i = 0; i < m; i++)
            for (int j = 0; j < n; j++)
                cin >> p[i][j];
    }
    void transport() {
        q = new T1*[n];
        for (int i = 0; i < n; i++)
            q[i] = new T1[m];
        for (int i = 0; i < m; i++)
            for (int j = 0; j < n; j++)
                q[j][i] = p[i][j];
    }
    void print() {
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++) {
                cout << q[i][j];
                if (j == m-1) cout << endl;
                else cout << " "; 
            }
    }
    ~Matrix() {
        for(int i = 0; i < m; i++)
            delete []p[i];
        delete []p;
        for(int i=0;i<n;i++)
            delete []q[i];
        delete []q;
    }
};

int main() {
    int t;
    cin >> t;
    while (t--) {
        char type;
        int m, n;
        cin >> type >> m >> n;
        if (type == 'I') {
            Matrix<int> m1(m, n);
            m1.transport();
            m1.print();
        } else if (type == 'C') {
            Matrix<char> m1(m, n);
            m1.transport();
            m1.print();
        } else {
            Matrix<double> m1(m, n);
            m1.transport();
            m1.print();
        }
    }
    return 0;
}
```