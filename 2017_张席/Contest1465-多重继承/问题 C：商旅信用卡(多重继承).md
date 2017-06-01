# 问题 C: 商旅信用卡(多重继承)

## 题目描述

某旅游网站（假设旅程网）和某银行推出旅游综合服务联名卡—旅程信用卡，兼具旅程会员卡和银行信用卡功能。

旅程会员卡，有会员卡号（int）、旅程积分（int），通过会员卡下订单，按订单金额累计旅程积分。

信用卡，有卡号（int）、姓名（string)、额度（int)、账单金额（float)、信用卡积分（int）。------请注意数据类型

信用卡消费金额m，若超额度，则不做操作；否则，账单金额+m，信用卡积分按消费金额累加。

信用卡退款m，账单金额-m，信用卡积分减去退款金额。

通过旅程信用卡在旅程网下单，旅程积分和信用卡积分双重积分（即旅程积分和信用卡积分同时增加）。

旅程信用卡可以按      旅程积分：信用卡积分= 1：2    的比例将信用卡积分兑换为旅程积分。

初始假设信用卡积分、旅程积分、账单金额为0。

根据上述内容，定义旅程会员卡类、信用卡类，从两者派生出旅程信用卡类并定义三个类的构造函数和其它所需函数。

生成旅程信用卡对象，输入卡信息，调用对象成员函数完成旅程网下单、信用卡刷卡、信用卡退款、信用卡积分兑换为旅程积分等操作。

## 输入

第一行：输入旅程会员卡号 信用卡号 姓名 额度

第二行：测试次数n

第三行到第n+2行，每行：操作 金额或积分

o   m（旅程网下订单，订单金额m）

c   m（信用卡消费，消费金额m）

q   m (信用卡退款，退款金额m）

t    m（积分兑换，m信用卡积分兑换为旅程积分）

## 输出

输出所有操作后旅程信用卡的信息：

旅程号   旅程积分

信用卡号  姓名   账单金额   信用卡积分

## 样例输入
```
1000 2002  lili  3000
4
o 212.5
c 300
q 117.4
t 200
```

## 样例输出
```
1000 312
2002 lili 395.1 195
```

## 优秀代码示例
```C++
#include <iostream>
#include <string>

using namespace std;

// 旅程网会员卡
class CVIPCard_LCWGO {
protected:
    // 会员卡号
    int id;
    // 积分
    int points;
public:
    // 构造函数
    CVIPCard_LCWGO(int id, int init_points = 0): id(id), points(init_points) {}
    // 消费函数
    void consume(float num) {
        // 累积积分
        points += (int)num;
    }
    // 输出函数
    void print() {
        cout << id << ' ' << points << endl;
    }
};

// 信用卡
class CCreditCard {
protected:
    // 信用卡号
    int id;
    // 姓名
    string name;
    // 额度
    int credits;
    // 账单金额
    float bill;
    // 积分
    int points;
public:
    // 构造函数
    CCreditCard(int id, string name, int credits, float bill = 0, int points = 0)
        :id(id), name(name), credits(credits), bill(bill), points(points) {}
    // 消费函数
    void consume(float num) {
        if (bill + num <= credits) {
            bill += num;
            // 累计积分
            points += (int)num;
        }
    }
    // 退款函数
    void refund(float num) {
        // 退款需在合理范围内
        if (bill - num >= 0) {
            bill -= num;
            // 扣除响应的积分
            points -= (int)num;
        }
    }
    // 输出函数
    void print() {
        cout << id << ' ' << name << ' ' << bill << ' ' << points << endl;
    }
};

// 旅程信用卡
class CCreditCard_LCWGO: public CVIPCard_LCWGO, public CCreditCard {
public:
    // 构造函数
    CCreditCard_LCWGO(int VIPCard_id, int CreditCard_id, string name, int credits)
        :CVIPCard_LCWGO(VIPCard_id), CCreditCard(CreditCard_id, name, credits) {}
    // 下订单函数
    void order(float num) {
        // 如果消费金额在可用余额范围内
        if (bill + num <= credits) {
            // 分别调用两个父类的消费函数
            CCreditCard::consume(num);
            CVIPCard_LCWGO::consume(num);
        }
    }
    // 消费函数
    void consume(float num) {
        // 默认调用信用卡的消费函数
        CCreditCard::consume(num);
    }
    // 积分转换函数
    void creditCardPointsToVIPCardPoints (int num) {
        if (num < CCreditCard::points) {
            CCreditCard::points -= num;
            CVIPCard_LCWGO::points += (int)(num / 2);
        }
    }
    // 输出函数
    void print() {
        CVIPCard_LCWGO::print();
        CCreditCard::print();
    }
};

int main () {
    int VIPCard_id, CreditCard_id;
    string name;
    int credits;
    int n;
    cin >> VIPCard_id >> CreditCard_id >> name >> credits;
    CCreditCard_LCWGO p(VIPCard_id, CreditCard_id, name, credits);
    cin >> n;
    while (n--) {
        char opr;
        float num;
        cin >> opr >> num;
        switch (opr) {
            // 旅程网下订单
            case 'o': p.order(num); break;
            // 信用卡消费
            case 'c': p.consume(num); break;
            // 退款
            case 'q': p.refund(num); break;
            // 积分转换
            case 't': p.creditCardPointsToVIPCardPoints((int)num);
        }
    }
    p.print();
    return 0;
}
```