# 问题 A: 电话号码升位(拷贝构造函数)

## 题目描述

定义一个电话号码类CTelNumber,包含1个字符指针数据成员,以及构造、析构、打印及拷贝构造函数。

字符指针是用于动态创建一个字符数组，然后保存外来输入的电话号码

构造函数的功能是为对象设置键盘输入的7位电话号码，

拷贝构造函数的功能是用原来7位号码的对象升位为8位号码对象,也就是说拷贝构造的对象是源对象的升级.电话升位的规则是原2、3、4开头的电话号码前面加8，原5、6、7、8开头的前面加2。

注意:电话号码只能全部是数字字符，且与上述情况不符的输入均为非法)

## 输入

测试数据的组数 t

第一个7位号码

第二个7位号码

......

## 输出

第一个号码升位后的号码

第二个号码升位后的号码

......

如果号码升级不成功，则输出报错信息，具体看示例

## 样例输入
```
3
6545889
3335656
565655
```

## 样例输出
```
26545889
83335656
Illegal phone number
```

## 优秀代码示例
```C++
// Author: 2016190037 温标林
#include<cstdio>
#include<iostream>
#include<cstring>
#include<string>
using namespace std;

class number
{
private:
    string s;
public:
    number(string s1)
    {
        s = s1;
    }
    number(number&s1)
    {
        if (s1.s.size() != 7) s = "Illegal phone number";
        else if (s1.s[0] <= '1' || s1.s[0] >= '9') s = "Illegal phone number";
        else if(s1.s[0] < '5') s = "8" + s1.s;
        else s = "2" + s1.s;
        for (int i = 0; i < s.size(); i++)
            if (s[i] < '0' || s[i] > '9')
            {
                s = "Illegal phone number";
                break;
            }
    }
    ~number() {}
    void print()
    {
        cout << s << endl;
    }
};

int main()
{
    int T;
    scanf("%d", &T);
    while (T--)
    {
        string s;
        cin >> s;
        number A(s);
        number B(A);
        B.print();
    }
    return 0;
}
```
