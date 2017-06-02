# 问题 A: 机器人变身（类与对象）

## 题目描述

编写一个机器人类，包含属性有机器名、血量、伤害值、防御值、类型和等级。其中血量、伤害和防御和等级、类型相关：
普通型机器人，类型为N，血量、伤害、防御是等级的5倍
攻击型机器人，类型为A，攻击是等级的10倍，其他属性和普通的一样
防御型机器人，类型为D，防御是等级的10倍，其他属性和普通的一样
生命型机器人，类型为H，生命是等级的50倍，其他属性和普通的一样。
机器人操作包括：打印、各个属性的获取和设置方法，构造函数可有可无，根据需要自行编写，

编写一个全局函数用于机器人变身，使得各种类型机器人能够相互转变。参数包括机器人对象指针和变身后的机器人类型，功能是修改机器人类型，并更改相关的属性。如果变身类型和机器人原来的类型不同，则执行变身功能，并返回true；如果变身类型和原来类型相同，则不执行变身，并返回false.

要求所有数据成员都是私有属性，用C++语言和面向对象设计思想来编程实现上述要求

## 输入

第一行输入t，表示要执行t次机器人变身

接着每两行，一行输入一个机器人的属性，包括机器名、类型、等级，另一行输入变身类型

依次类推输入

## 输出

每行输出变身后的机器人信息，要求调用机器人的打印方法来输出，即使机器人不变身也输出

属性输出依次为：名称、类型、等级、血量、伤害、防御

最后一行输出执行变身的次数

## 样例输入
```
3
X001 N 5
H
X002 A 5
D
X003 D 5
D
```

## 样例输出
```
X001--H--5--250--25--25
X002--D--5--25--25--50
X003--D--5--25--25--50
The number of robot transform is 2
```

## 优秀代码示例
```C++
// Author: 2016150143 黄鸿凯
#include <iostream>
#include <string>

using namespace std;

class Robot {
private:
    char type;
    int level;
    string name;
    int health, attack, defence;
public:
    // 构造函数。默认为普通机器人，默认等级为1
    Robot(string name, char type = 'N', int level = 1)
        :name(name), type(type), level(level) {
        // 调用init函数对机器人进行初始化
        init(type);
    }
    // 输出函数
    void print() {
        cout << name << "--" << type << "--" << level << "--" << health << "--" << attack << "--" << defence << endl;
    }
    char getType() { return type; }
    // 初始化机器人函数，会根据参数的值来决定机器人的类型
    void init(char type = 0) {
        // 如果没有参数，则按照现有的类型进行初始化
        if (type == 0) type = this->type;
        this->type = type;
        // 先按照普通机器人的标准初始化
        health = attack = defence = level * 5;
        // 然后根据具体类型赋予其不同的属性
        if (type == 'A') attack = level * 10;
        else if (type == 'D') defence = level * 10;
        else if (type == 'H') health = level * 50;
    }
};

// 机器人类型转换函数
bool change(Robot& a, char typeChanged){
    // 如果和当前类型相同则返回false
    if (a.getType() == typeChanged) return false;
    // 否则按照指定类型对机器人重新初始化
    a.init(typeChanged);
    return true;
}

int main(){
    int T;
    cin >> T;
    int ans = 0;
    while (T--) {
        string name;
        char type,typeChanged;
        int level;
        cin >> name >> type >> level >> typeChanged;
        Robot robot(name, type, level);
        if (change(robot, typeChanged)) ans++;
        robot.print();
    }
    cout << "The number of robot transform is " << ans << endl;
}
```