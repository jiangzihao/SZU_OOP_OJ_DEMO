# 问题 A: 任意鸡任意钱问题(构造与析构)

## 题目描述

百鸡百钱问题描述为：用100元钱买100只鸡，已知每只公鸡5元，每只母鸡3元，3只小鸡1元，问能买多少只公鸡、母鸡和小鸡？试将该类问题用一个类来表示，百鸡百钱问题只是这个类如CChickProblem的一个实例，假设各种鸡的价格不变,类中数据成员有总钱数、要买的总的鸡数、能买到的母鸡、小鸡和公鸡的数量。成员函数有构造和析构函数，求问题解的函数findSolution，打印问题解的函数printSolution。(要求用动态数组保存问题的所有解)

编写程序求解该类问题。

## 输入

测试数据的组数 t

第一组 鸡数 钱数

第二组 鸡数 钱数

.......
第一组解个数

## 输出


第一组第一个解公鸡数 母鸡数 小鸡数

第一组第二个解公鸡数 母鸡数 小鸡数

.........


第二组解个数

第二组第一个解公鸡数 母鸡数 小鸡数

第二组第二个解公鸡数 母鸡数 小鸡数

.........

## 样例输入
```
2
100 100
200 200
```

## 样例输出
```
3
4 18 78
8 11 81
12 4 84
7
4 43 153
8 36 156
12 29 159
16 22 162
20 15 165
24 8 168
28 1 171
```

## 优秀代码示例
```C++
// Author: 2016150043 黄泓凯
#include <iostream>

using namespace std;

class CChickProblem{
    int (*result)[3]; // 利用动态数组保存所有解
    int resultNum;    // 保存解的数量
    int num, money;   // 保存鸡数和钱数
public:
    CChickProblem() {}
    CChickProblem(int num, int money)
    :num(num),money(money) {}
    // 查找解并保存到动态数组
    void findSolution() {
        resultNum = 0;
        for (int i = 1; i <= num - 2; i++) {
            for (int j = 1; j < num - i; j++) {
                int k = num - i - j;
                if (k % 3 == 0 && 5 * i + j * 3 + k / 3 == money) resultNum++; // 第一次循环统计解的数量
            }
        }
        result = new int[resultNum][3];
        int index = 0;
        for (int i = 1; i <= num - 2; i++) {
            for (int j = 1; j < num - i; j++) {
                int k = num - i - j;
                if (k % 3 == 0 && 5 * i + j * 3 + k / 3 == money) { // 第二次循环保存解
                      result[index][0] = i;
                      result[index][1] = j;
                      result[index++][2] = k;
                }
            }
        }
    }
    // 输出解
    void printSolution() {
        cout << resultNum << endl;
        for (int i = 0;i < resultNum; i++)
            cout << result[i][0] << ' ' << result[i][1] << ' ' << result[i][2] << endl;
    }
};

int main() {
    int T;
    cin >> T;
    while (T--){
        int num, money;
        cin >> num >> money;
        CChickProblem test(num, money);
        test.findSolution();
        test.printSolution();
    }
    return 0;
}

```
