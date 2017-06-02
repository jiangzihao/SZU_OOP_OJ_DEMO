# 问题 E: 平均学分绩点计算（类和对象）

## 题目描述

课程的总评成绩与绩点对应关系为：

A+ ~ 4.5、A~ 4.0、B+~ 3.5、B~3.0、C+ ~ 2.5、C ~ 2.0、D ~ 1.0、F ~ 0

如果选修n门课(n<20)，则平均学分绩点(GPA)的计算公式为：

平均学分绩点（GPA）

= (∑各课程总评成绩对应绩点×课程学分)/ ∑ 课程学分

用选课类描述选课信息，包含属性: 课程号、课程学分、总评成绩、包含方法：返回课程号、计算成绩对应的绩点并返回结果、构造函数。

主函数输入某学生的n门选课信息，计算获得的学分及平均学分绩点。

可以增加成员或全局函数，静态、非静态、友元都可以。

## 输入

 第一行输入测试次数t

 后跟t组测试数据，每组测试数据格式如下：

 选课门数n

 n门选课信息，课程号 学分 总评绩点

## 输出

  对每组测试数据，输出：

  选修的所有课程号 

  获得学分（保留1位小数）  平均学分绩点（保留2位小数）

## 样例输入
```
2
4
1300800001 3 A
1501020003 4 B
1900600005 5 A+
5000520002 3 C
3
1300800007 3 B
1501020006 3.5 F
5000520008 3 A
```

## 样例输出
```
1300800001 1501020003 1900600005 5000520002
获得学分:15.0 平均学分绩点:3.50
1300800007 1501020006 5000520008
获得学分:6.0 平均学分绩点:2.21
```

## 优秀代码示例
```C++
// Author: 2016150040 杨汇琛
#include <iostream>
#include <string>
#include <cstdio>

using namespace std;
 
class LESSON {
private:
    int n;
    double *credit, gpa, all_cre, get_cre;
    string *les_no, *lv;
public:
    LESSON( int init_n ) : n( init_n ) {
        credit = new double[ n ];
        les_no = new string[ n ];
        lv = new string[ n ];
        for( int i = 0; i < n; ++i )
            cin >> les_no[i] >> credit[i] >> lv[i];
    }
    ~LESSON() {
        delete []credit;
        delete []les_no;
        delete []lv;
    }
    double CalGpa() {
        gpa = all_cre = get_cre = 0;
        for( int i = 0; i < n; ++i ) {
            // 通过字符串中的第一个字符决定其个位分值
            double wei = ( 'A' - lv[i][0] ) + 4;
            // 再通过字符串的长度判断是不是A+、B+、C+
            if( lv[i].size() == 2 ) wei += 0.5;
            else if( lv[i][0] == 'F' ) wei = 0;
            if( wei != 0 ) get_cre += credit[i];
            gpa += wei*credit[i];
            all_cre += credit[i];
        }
        gpa /= all_cre;
        return gpa;
    }
    void PrintInfo() {
        for( int i = 0; i < n; ++i ) {
            if( i ) cout << ' ' << les_no[i];
            else cout << les_no[i];
        }
        printf( "\n获得学分:%.1lf 平均学分绩点:%.2lf\n", get_cre, gpa );
    }
};
 
int main() {
    int T;
    cin >> T;
    while( T-- ) {
        int n;
        cin >> n;
        LESSON ls( n );
        ls.CalGpa();
        ls.PrintInfo();
    }
    return 0;
}
```