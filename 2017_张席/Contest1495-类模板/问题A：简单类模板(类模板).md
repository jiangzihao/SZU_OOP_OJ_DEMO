# 问题 A: 简单类模板(类模板)

## 题目描述

定义一个列表类，该列表包含属性：数值列表（用长度为100的数组表示），数据长度（实际的数据个数）；包含的方法：初始化、插入、删除、打印，方法定义为：

1）初始化，接受外来参数，把数据保存在数值列表中，未使用的列表部分全部初始化为-1

2）插入，接受外来参数的插入位置和插入数值，插入位置从0开始计算，注意从插入位置开始，原有数据都要往后移动一位，且数据长度+1

3）删除，接受外来参数的删除位置，删除位置从0开始计算，注意从删除位置后一位开始，原有数据都要往前移动一位，且数据长度-1

4）打印，把包含的数据按位置顺序输出一行，数据之间单个空格隔开

使用类模板的方法，使得这个类支持整数int类型和浮点数double类型

## 输入

第一行先输入参数n表示有n个数据，接着输入n个整数

第二行输入两个参数，表示插入位置和插入数值，数值为整数

第三行输入删除位置

第四行先输入参数n表示有n个数据，接着输入n个浮点数

第五行输入两个参数，表示插入位置和插入数值，数值为浮点数

第六行输入删除位置

## 输出

针对头三行输入，分别执行初始化、插入操作和删除操作，调用打印方法输出列表包含的整数数据

针对接着的三行输入，分别执行初始化、插入操作和删除操作，调用打印方法输出列表包含的浮点数数据

## 样例输入
```
5 11 22 33 44 55
2 888
4
5 1.1 2.2 3.3 4.4 5.5
2 88.8
3
```

## 样例输出
```
11 22 888 33 55
1.1 2.2 88.8 4.4 5.5
```

## 优秀代码示例
```C++
// Author: 2016190037 温标林
#include<iostream>
#include<cstring>

using namespace std;

template<class T>
class Clist {
private
    int n;
    T arr[100];
public:
    Clist(int n0);
    void insert(int n0, T x);
    void erase(int x);
    void print();
};

template<class T>
Clist<T>::Clist(int n0) {
    n = n0;
    for (int i = n; i < 100; i++) arr[i] = -1;
    for (int i = 0; i < n; i++) cin >> arr[i];
}

template <class T>
void Clist<T>::insert(int n0, T x) {
    for (int i = n - 1; i >= n0; i--)
        arr[i+1] = arr[i];
    arr[n0] = x;
}

template <class T>
void Clist<T>::erase(int x) {
    for (int i = x; i < n - 1; i++)
        arr[i] = arr[i+1];
}

template <class T>
void Clist<T>::print() {
    for (int i = 0; i < n - 1; i++)
        cout << arr[i] << " ";
    cout << arr[n] << endl;
}

int main() {
    int n;
    cin >> n;
    Clist<int> a(n);
    int idx, x;
    cin >> idx >> x;
    a.insert(idx, x);
    cin >> idx;
    a.erase(idx);
    a.print();
    cin >> n;
    Clist<float> b(n);
    float y;
    cin >> idx >> y;
    b.insert(idx, y);
    cin >> idx;
    b.erase(idx);
    b.print();
    return 0;
}
```