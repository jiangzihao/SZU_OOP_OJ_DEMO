# 问题 B: 数据排序（函数模板）

## 题目描述

编写一个进行升序排序的函数模板，其中数组为具有n个元素，类型为T。

注意：必须使用模板函数

## 输入

第一行输入t表示有t个测试实例

第二行先输入一个大写字母表示数组类型，I表示整数类型，C表示字符型，S表示字符串型，D表示双精度数类型；然后输入n表示数组长度。

第三行输入n个数据

依次输入t个实例

## 输出

每行输出一个结果

## 样例输入
```
4
I 10
15 3 51 27 9 35 78 14 65 8
D 3
-11.3 25.42 13.2
C 6
a b g e u q
S 4
sandy david eason cindy
```

## 样例输出
```
3 8 9 14 15 27 35 51 65 78 
-11.3 13.2 25.42 
a b e g q u 
cindy david eason sandy 
```

## 优秀代码示例
```C++
// Author: 2016150043 黄泓凯
#include<iostream>
#include<string>

using namespace std;

template<class T>
void sort(T a[],int n) {
    for(int i = 0; i < n - 1; i++)
        for (int j = i + 1; j < n; j++) {
            if (a[i] > a[j]) {
                T t = a[i];
                a[i] = a[j];
                a[j] = t;
            }
        }
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
        if (ch=='I') {
            int *a = new int[n];
            for (int i = 0; i < n; i++) cin >> a[i];
            sort(a, n);
            for (int i = 0; i < n; i++)
                cout << a[i] << " ";
            cout << endl;
            delete []a;
        } else if (ch == 'D') {
            double *a = new double[n];
            for (int i = 0; i < n; i++) cin >> a[i];
            sort(a, n);
            for (int i = 0; i < n; i++)
                cout << a[i] << " ";
            cout << endl;
            delete []a;
        } else if (ch == 'S') {
            string *a = new string[n];
            for (int i = 0; i < n; i++) cin >> a[i];
            sort(a, n);
            for (int i = 0; i < n; i++)
                cout << a[i] << " ";
            cout << endl;
            delete []a;
        } else if(ch=='C') {
            char *a = new char[n];
            for (int i = 0; i < n; i++) cin >> a[i];
            sort(a, n);
            for (int i = 0; i < n; i++)
                cout << a[i] << " ";
            cout << endl;
            delete []a;
        }
    }
    return 0;
}
```