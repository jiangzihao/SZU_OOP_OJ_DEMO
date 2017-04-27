# 问题 B: 存折与信用卡（继承）

## 题目描述

定义一个存折类CAccount，存折类具有帐号（account, long）、姓名（name,char[10])、余额（balance,float）等数据成员，可以实现存款（deposit,操作成功提示“saving ok!”)、取款（withdraw，操作成功提示“withdraw ok!”）和查询余额（check）的操作，取款金额必须在余额范围内，否则提示“sorry! over balance!”。从存折类派生出信用卡类CCreditcard，信用卡类增加了透支限额（limit,float）一项数据成员，对取款操作进行修改，允许在限额范围内透支金额，超出范围取款提示“sorry! over limit!”。

编写主函数，建立这两个类的对象并测试之。

1. 对于存折类，输入账号、姓名、余额后，按照查询余额、存款、查询余额、取款、查询余额的顺序调用类方法并输出。

2. 对于信用卡类，输入账号、姓名、余额、透支限额后，按照查询余额、存款、查询余额、取款、查询余额的顺序调用类方法并输出。

## 输入

账号 姓名 余额

存款金额

取款金额

账号 姓名 余额 透支限额

存款金额

取款金额

## 输出

账户余额

存款操作结果

账户余额

取款操作结果

账户余额

账户余额

存款操作结果

账户余额

取款操作结果

账户余额

## 样例输入
```
1000 Tom 1000
500
1000
2000 John 500 500
500
1501
```

## 样例输出
```
balance is 1000
saving ok!
balance is 1500
withdraw ok!
balance is 500
balance is 500
saving ok!
balance is 1000
sorry! over limit!
balance is 1000
```

## 优秀代码示例
```C++
#include<iostream>
#include<string>

using namespace std;

// 存折类
class CAccount {
protected:
    // 账户id
    double account;
    // 名字
    string name;
    // 余额
    double balance;
public:
    // 构造函数
    CAccount(double account, string name, double balance):
        account(account), name(name), balance(balance) {}
    // 存款操作
    void deposit(double x) {
        balance += x;
        cout << "saving ok!" << endl;
    }
    // 取款操作
    void withdraw(double x) {
        if (x <= balance) {
            balance -= x;
            cout << "withdraw ok!" << endl;
        }
        else {
            // 余额不足输出错误提示
            cout << "sorry! over balance!" << endl;
        }
    }
    // 获取余额
    double check() {
        return balance;
    }
    // 输出余额
    void print() {
        cout << "balance is " << balance << endl;
    }
};

// 信用卡类
class CCreditcard :public CAccount {
protected:
    // 信用额度
    double limit;
public:
    // 构造函数
    CCreditcard(double account, string name, double balance, double limit)
        :CAccount(account,name,balance), limit(limit) {}
    // 重写的取款操作
    void withdraw(double x) {
        // 注意此处的判断条件
        if (x <= balance + limit) {
            balance -= x;
            cout << "withdraw ok!" << endl;
        }
        else {
            // 余额不足时输出错误提示
            cout << "sorry! over limit!" << endl;
        }
    }
};

/*
 * 不建议在主函数内直接输入余额，会造成大量冗余
 * 最好就是写一个print()函数，来减小冗余
**/
int main() {
    double account;
    string name;
    double save, withdraw, balance, limit;
    cin >> account >> name >> balance;
    CAccount acc(account, name, balance);
    // 账户余额
    acc.print();
    cin >> save;
    // 存款
    acc.deposit(save);
    // 账户余额
    acc.print();
    cin >> withdraw;
    // 取款
    acc.withdraw(withdraw);
    // 账户余额
    acc.print();
    cin >> account >> name >> balance >> limit;
    CCreditcard cre(account, name, balance, limit);
    // 账户余额
    cre.print();
    cin >> save;
    // 存款
    cre.deposit(save);
    // 账户余额
    cre.print();
    cin >> withdraw;
    // 取款
    cre.withdraw(withdraw);
    // 账户余额
    cre.print();
    return 0;
}
```
