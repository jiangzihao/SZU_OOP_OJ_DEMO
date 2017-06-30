# 问题 E: 倚天屠龙记（函数模板）

## 题目描述

江湖中有一个传言，只要倚天剑和屠龙刀中暗藏的秘密拼到一起，就能得到天下无敌的内功秘笈。设计一个函数模板，完成拼凑的功能（将倚天剑的秘密连接到屠龙刀的后面），并将秘笈输出. 其中每个秘密由n个元素组成，类型为T。

## 输入

第一行输入t表示有t个测试实例

第二行先输入一个大写字母表示数据类型，I表示整数类型，D表示双精度数类型，C表示字符型；然后输入n表示数据个数。

第三行输入倚天剑的n个数据

第四行输入屠龙刀的n个数据

依次输入t个实例

## 输出

每行输出一个结果

## 样例输入
```
2
I 5
5 3 51 27 9
27 0 0 5 1
C 5
kitty
hello
```

## 样例输出
```
2700515351279
hellokitty
```

## 优秀代码示例
```C++
#include<iostream>
#include<string>

using namespace std;

template<class T>
void find(T a[],T b[],int n) {
    T temp = new T[2 * n + 1];
    for (int i = 0; i < n; i++) {
        temp[i] = a[i];
        temp[n + i] = b[i];
    }
    for (int i = 0; i < 2 * n; i++)
        cout << T[i]
    cout << endl;
}

int main() {
    int T;
    cin >> T;
    while (T--) {
        char ch;
        cin >> ch;
        while (ch < 'A' || ch > 'Z') cin >> ch;
        int n;
        cin >> n;
        if (ch == 'I') {
            int *a = new int[n], *b = new int[n];
            for (int i = 0; i < n; i++) cin >> a[i];
            for (int i = 0; i < n; i++) cin >> b[i];
            find(a, b, n);
            delete []a;
            delete []b;
        } else if (ch == 'D') {
            double *a = new double[n], *b = new double[n];
            for (int i = 0; i < n; i++) cin >> a[i];
            for (int i = 0; i < n; i++) cin >> b[i];
            find(a, b, n);
            delete []a;
            delete []b;
        } else if (ch == 'C') {
            char *a = new char[n], *b = new char[n];
            for (int i = 0; i < n; i++) cin >> a[i];
            for (int i = 0; i < n; i++) cin >> b[i];
            find(a, b, n);
            delete []a;
            delete []b;
        }
    }
    return 0;
}
```