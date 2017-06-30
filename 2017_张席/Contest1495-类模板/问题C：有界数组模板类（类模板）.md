# 问题 C: 有界数组模板类（类模板）

## 题目描述

编写有界数组模板BoundArray（即检查对数组元素下标引用并在下标越界时终止程序的执行），能够存储各种类型的数据。要求实现对数组进行排序的方法sort，及对数组进行查找的方法search。

## 输入

第一行先输入t，表示有t个测试用例

从第二行开始输入每个测试用例的数据。

首先输入数据类型，I表示int，D表示double，C表示char，接着输入数组的元素个数

然后输入每个元素

最后输入要查找的元素

## 输出

首先输出从小到大排序的元素

然后输出查找元素的结果，找到则输出下标，没找到则输出-1

## 样例输入
```
2
I 2
1 2
2
D 3
3.5 6.2 2.9
2.1
```

## 样例输出
```
1 2 
1
2.9 3.5 6.2 
-1
```

## 优秀代码示例
```C++
// Author: 2016150043 黄泓凯
#include<iostream>

using namespace std;
 
template<typename T>
class BoundArray {
    T *arr;
    int num;
public:
    BoundArray() {}
    BoundArray(int num):num(num) {
        arr = new T[num];
    }
    void mysort() {
        sort(arr, arr + num);
        for (int i = 0; i < num; i++) {
            cout << arr[i] << " ";
        }
        cout << endl;
    }
    int find(T key) {
        int s = 0, e = num - 1;
        for (int i = 0; i < num; i++)
            if (arr[i] == key)
                return i;
        return -1;
    }
    void in() {
        for (int i = 0; i < num; i++)
            cin >> arr[i];
    }
};
 
int main() {
    int T;
    cin >> T;
    while (T--) {
        char ch;
        int n;
        cin >> ch >> n;
        if (ch == 'I') {
            BoundArray<int> tmp(n);
            tmp.in();
            tmp.mysort();
            int key;
            cin >> key;
            cout << tmp.find(key) << endl;
        } else if (ch == 'D') {
            BoundArray<double> tmp(n);
            tmp.in();
            tmp.mysort();
            double key;
            cin >> key;
            cout << tmp.find(key) << endl;
        } else if (ch == 'C') {
            BoundArray<char> tmp(n);
            tmp.in();
            tmp.mysort();
            char key;
            cin >> key;
            cout << tmp.find(key) << endl;
        }
    }
    return 0;
}
```