# 问题 A: 查找数组元素最小值（函数模板）

## 题目描述

设计函数模板求出数组的最小值，其中数组为具有n个元素，类型为T。

注意：必须使用模板函数

## 输入

第一行输入t表示有t个测试实例

第二行先输入一个大写字母表示数组类型，I表示整数类型，S表示字符串类型，D表示双精度数类型；然后输入n表示数组长度。

第三行输入n个数据

依次输入t个实例

## 输出

每行输出一个结果

## 样例输入
```
3
I 5
1 3 5 7 9
D 3
-1.1 -2.2 -3.3
S 3
linda lelele linlin
```

## 样例输出
```
1
-3.3
lelele
```

## 优秀代码示例
```C++
// Author: 2016190004 刘俊麟
#include<iostream>

using namespace std;

template<class T>
T Min(T *p, int n) {
    int i;
    T min = p[0];
    for (i = 1; i < n; i++)
        if (p[i] < min)
            min = p[i];
    return min; 
} 

int main() {
    int t,n,i;
    char m;
    cin >> t;
    while (t--) {
        cin >> m;
        if (m == 'I') {
            int *p;
            cin >> n;
            p = new int[n];
            for (i = 0; i < n; i++)
            cin >> p[i];
            cout << Min(p, n) << endl;
        } else if (m == 'D') {
            float *p;
            cin >> n;
            p = new float[n];
            for (i = 0; i < n; i++)
            cin >> p[i];
            cout << Min(p, n) << endl;
        } else if(m == 'S') {
            string *p;
            cin >> n;
            p = new string[n];
            for (i = 0; i < n; i++)
            cin >> p[i];
            cout << Min(p, n) << endl;
        }
    }
    return 0;
} 
```