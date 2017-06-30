# 问题 D: 谁的票数最高（函数模板）

## 题目描述

某小镇要票选镇长，得票最高者当选。但由于投票机制不健全，导致每届投票时，候选人在投票系统的识别码类型不一致。请编写函数模板，能针对多种类型的数据，查找出得票最高的元素。其中，每届投票的选票有n张，识别码类型为T

注意：必须使用模板函数

## 输入

第一行输入t表示有t个测试实例

第二行先输入一个大写字母表示识别码类型，I表示整数类型，C表示字符型，S表示字符串型；然后输入n表示数组长度。

第三行输入n个数据

依次输入t个实例

## 输出

每行输出一个结果，分别输出当选者的识别码和得票数，以空格分开。

## 样例输入
```
3
I 10
5 3 5 2 9 7 3 7 2 3
C 8
a b a e b e e q
S 5
sandy david eason cindy cindy
```

## 样例输出
```
3 3
e 3
cindy 2
```

## 优秀代码示例
```C++
// Author: 2016190037 温标林
#include<iostream>
#include<string>

using namespace std;

template<class T>
void find(T a[], int n) {
    T winner;
    int max = 0;
    for (int i = 0; i < n; i++) {
        T candi = a[i];
        int res = 0;
        for (int j = 0; j < n; j++)
            if (a[j] == a[i]) res++;
        if (res > max) {
            max = res;
            winner = candi;
        }
    }
    cout << winner << " " << max << endl;
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
            int *a = new int[n];
            for (int i = 0; i < n; i++) cin >> a[i];
            find(a, n);
            delete []a;
        } else if (ch == 'D') {
            double *a = new double[n];
            for (int i = 0; i < n; i++) cin >> a[i];
            find(a, n);
            delete []a;
        } else if (ch == 'S') {
            string *a = new string[n];
            for (int i = 0; i < n; i++) cin >> a[i];
            find(a, n);
            delete []a;
        } else if (ch == 'C') {
            char *a = new char[n];
            for(int i = 0; i < n; i++) cin >> a[i];
            find(a, n);
            delete []a;
        }
    }
    return 0;
}

```