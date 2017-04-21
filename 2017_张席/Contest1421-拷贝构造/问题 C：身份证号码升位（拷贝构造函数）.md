# 问题 C: 身份证号码升位（拷贝构造函数）

## 题目描述
```C++
class CDate

{

private:

int year, month, day;

public:

CDate(int,int,int);

bool check(); //检验日期是否合法

bool isLeap();

void print();

};

class CStudentID

{

private:

char *p_id, *p_name; //身份证号码，姓名

CDate birthday; //出生日期

int registered; //登记否

public:

CStudentID(char *p_idval, char *p_nameval, CDate &day); //构造函数，若:日期非法;日期与id日期不符;id有非法字符;id不是15位或18位;id是18位但检验码不对,则输出"illegal id"并置registered=0。否则输出对象的属性并置registered=1.

CStudentID(const CId &r); //拷贝构造函数，若r.p_id为15位则升到18位(加年份的19和校验位)

bool checked() { return registered; }

~CId();

};
```

按上述方式定义一个日期类CDate和学生ID类CStudentID。

身份证第18位校验码的生成方法：

1、将身份证号码前17位数分别乘以7,9,10,5,8,4,2,1,6,3,7,9,10,5,8,4,2。然后将其相加

2、将17位数字和系数乘加的和除以11，得到余数。

3、余数与校验码的对应关系为1,0,X,9,8,7,6,5,4,3,2。也即：如果余数是3，身份证第18位就是9。如果余数是2，身份证的最后一位号码就是X。

主函数:

//输入测试次数t

//循环t次

//每次循环中首先输入年月日,并定义日期对象

//然后输入姓名和身份证号码,并先用构造函数定义一个CStudentID对象s,若s.checked()为true,则再用s拷贝构造s_copy对象

## 输入

测试数据的组数 t

第一个出生日期年月日

第一个姓名,身份证号码

第二个出生日期年月日

第二个姓名,身份证号码

......

## 输出

第一个CStudent对象s的信息

第一个拷贝构造CStudent对象s_copy输出的信息或者无输出

第二个CStudent对象s的信息

第二个拷贝构造CStudent对象s_copy输出的信息或者无输出
......

## 样例输入
```
6
2018 2 29
张三 440301180229113
1997 4 30
李四 440301980808554
1920 5 8
王五 530102200508011
1980 1 1
赵六 340524198001010012
1988 11 12
钱七 1102038811120A4
1964 11 15
孙八 432831641115081
```

## 样例输出
```
张三 illegal id
李四 illegal id
王五 1920年5月8日 530102200508011
王五 1920年5月8日 53010219200508011X
赵六 illegal id
钱七 illegal id
孙八 1964年11月15日 432831641115081
孙八 1964年11月15日 432831196411150810
```

## 优秀代码示例
```C++
// Author: 2016190037 温标林
#include<cstdio>
#include<iostream>
#include<cstring>
#include<string>
using namespace std;

class CDate
{
private:
    int year, month, day;
public:
    CDate(int y = 0, int m = 0, int d = 0): year(y), month(m), day(d) {}
    CDate(CDate &p)
    {
        year = p.year;
        month = p.month;
        day = p.day;
    }
    // 利用拷贝构造函数从身份证ID中截取生日
    CDate(string s)
    {
        int i;
        if (s.size() == 18)
        {
            year = 0;
            for(i = 0; i < 4; i++)
                year = year * 10 + s[i] - '0';
            month = 0;
            for(i = 4; i < 6; i++)
                month = month * 10 + s[i] - '0';
            day = 0;
            for(i = 6; i < 8; i++)
                day = day * 10 + s[i] - '0';
        }
        else
        {
            year = 19;
            for(i = 0; i < 2; i++)
                year = year * 10 + s[i] - '0';
            month = 0;
            for(i = 2; i < 4; i++)
                month = month * 10 + s[i] - '0';
            day = 0;
            for(i = 4; i < 6; i++)
                day = day * 10 + s[i] - '0';
        }
    }
    // 判断日期相等
    bool equal(CDate &b)
    {
        return year == b.year && month == b.month && day == b.day;
    }
    // 判断闰年
    bool isLeap()
    {
        return year % 400 == 0 || year % 4 == 0 && year % 100 != 0;
    }
    // 判断日期溢出
    bool check()
    {
          int a[13] = {0,31,28 + isLeap(),31,30,31,30,31,31,30,31,30,31};
          if (month > 12 || month < 1) return false;
          return day <= a[month];
    }
    int gety() { return year; }
    int getm() { return month; }
    int getd() { return day; }
    void print()
    {
        printf("%d年%d月%d日", year, month, day);
    }
};

class CID
{
private:
    string p_id, p_name; //身份证号码，姓名
    CDate birthday; //出生日期
    int registered; //登记否
public:
    CID(string p_idval, string p_nameval, CDate &day)
    {
        p_id = p_idval;
        p_name = p_nameval;
        birthday = day;
        // 不支持2000年以后的15位身份证id
        if (day.gety() >= 2000 && p_id.size() < 18)
        {
            registered = false;
            return;
        }
        int i;
        // 不支持非18位也非15位的身份证id
        if (p_id.size() != 18 && p_id.size() != 15) {
            registered=false;
            return;
        }
        int y = day.gety(), m = day.getm(), s = day.getd();
        for (i = 0; i < p_id.size(); i++)
        {
            // 不支持除数字字符和X字符以外的字符
            if ((p_id[i] < '0' || p_id[i] > '9' ) && p_id[i] != 'X')
            {
                registered = false;
                return;
            }
            // 不支持15位身份证含有X字符
            if (p_id[i] == 'X' && i < 18)
            {
                registered = false;
                return;
            }
        }
        // 注册
        if (p_id.size() == 18)
        {
            CDate p(p_id.substr(6, 8));
            registered = p.equal(day);
        }
        else
        {
            CDate p(p_id.substr(6, 6));
            registered = p.equal(day);
        }
        if (!registered || p_id.size() == 15) return;
        int c[] = {7,9,10,5,8,4,2,1,6,3,7,9,10,5,8,4,2};
        int ans = 0;
        for(i = 0; i < 17; i++)
        ans += c[i] * (p_id[i] - '0');
        ans %= 11;
        int b[] = {1,0,-1,9,8,7,6,5,4,3,2};
        registered = p_id[17] == 'X' ? ans == 2 : p_id[17] - '0' == c[ans];
    }
    CID(const CID &r)
    {
        p_name = r.p_name;
        registered = r.registered;
        birthday = r.birthday;
        p_id = r.p_id.substr(0,6) + "19" + r.p_id.substr(6,9);
        int c[] = {7,9,10,5,8,4,2,1,6,3,7,9,10,5,8,4,2};
        int ans = 0;
        for (int i = 0; i < 17; i++)
            ans += c[i] * (p_id[i] - '0');
        ans %= 11;
        int b[] = {1,0,-1,9,8,7,6,5,4,3,2};
        if (ans == 2) p_id += "X";
        else p_id += char('0' + b[ans]);
    }
    int checked() { return registered; }
    ~CID(){}
    void print()
    {
        cout << p_name << " ";
        if(!registered)
        {
            printf("illegal id\n");
            return;
        }
        birthday.print();
        cout << " " << p_id << endl;
    }
};

int main()
{
    int T;
    cin >> T;
    while (T--)
    {
        int y, m, d;
        cin >> y >> m >> d;
        CDate day(y, m, d);
        string name, id;
        cin >> name >> id;
        CID a(id, name, day);
        a.print();
        if (a.checked())
        {
            CID b(a);
            b.print();
        }
    }
    return 0;
}
```
