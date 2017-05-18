# 问题 F: 日期时间合并输出（友元函数）

## 题目描述

已知日期类Date，有属性：年、月、日，其他成员函数根据需要自行编写，注意该类没有输出的成员函数
已知时间类Time，有属性：时、分、秒，其他成员函数根据需要自行编写，注意该类没有输出的成员函数
现在编写一个全局函数把时间和日期的对象合并起来一起输出，
函数原型为：void Display(Date &, Time &)
函数输出要求为：
1、时分秒输出长度固定2位，不足2位补0
2、年份输出长度固定为4位，月和日的输出长度固定2位，不足2位补0
例如2017年3月3日19时5分18秒
则输出为：2017-03-03 19:05:18
程序要求
1、把函数Display作为时间类、日期类的友元
2、分别创建一个日期对象和时间对象，保存日期的输入和时间的输入
3、调用Print函数实现日期和时间的合并输出

## 输入

第一行输入t表示有t组示例

接着一行输入三个整数，表示年月日

再接着一行输入三个整数，表示时分秒

依次输入t组示例

## 输出

每行输出一个日期和时间合并输出结果

输出t行

## 样例输入
```
2
2017 3 3
19 5 18
1988 12 8
5 16 4
```

## 样例输出
```
2017-03-03 19:05:18
1988-12-08 05:16:04
```

## 优秀代码示例
```C++
// Author: 2016150043 黄鸿凯
#include <iostream>
#include <iomanip>

using namespace std;
 
class Time;

class Date {
    int year, month, day;
public:
    Date(int year, int month, int day)
        :year(year),month(month),day(day) {}
    void print() {
        cout << setfill('0') << setw(4) << year << '-' << setw(2) << month << '-' << setw(2) << day << ' ';
    }
    friend void Display(Date&, Time&);
};
 
class Time {
    int hour, minute, second;
public:
    Time(int hour, int minute, int second)
        :hour(hour), minute(minute), second(second) {}
    void print() {
        cout << setfill('0') << setw(2) << hour << ':' << setw(2) << minute << ':' << setw(2) << second << endl;
    }
    friend void Display(Date&, Time&);
};
 
void Display(Date& a, Time& b) {
    a.print();
    b.print();
}
 
int main() {
    int T;
    cin >> T;
    while (T--) {
        int year, month, day, hour, minute, second;
        cin >> year >> month >> day >> hour >> minute >> second;
        Date a(year, month, day);
        Time b(hour, minute, second);
        Display(a, b);
    }
}
```