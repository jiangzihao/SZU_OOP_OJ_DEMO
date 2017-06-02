# 问题 C: 动物园（虚函数与多态）

## 题目描述

某个动物园内，有老虎、狗、鸭子和猪等动物，动物园的管理员为每个动物都起了一个名字，并且每个动物都有年龄、体重等信息。每到喂食的时候，不同的动物都会叫唤(speak)。每种动物的叫唤声均不同，老虎的叫唤声是“AOOO”，狗的叫唤声是“WangWang”，鸭子的叫唤声是“GAGA”，猪的叫唤声是“HENGHENG”。

定义一个Animal的基类，Animal类有函数Speak()，并派生老虎、狗、鸭子和猪类，其能发出不同的叫唤声（用文本信息输出叫声）。

编写程序，输入动物名称、名字、年龄，让动物园内的各种动物叫唤。

要求：只使用一个基类指针，指向生成的对象并调用方法。

## 输入

测试案例的个数

第一种动物的名称  名字  年龄

第二种动物的名称  名字 年龄

......

## 输出

输出相应动物的信息

如果不存在该种动物，输出There is no 动物名称 in our Zoo.  ，具体输出参考样例输出

## 样例输入
```
4
Tiger Jumpjump 10
Pig Piglet 4
Rabbit labi 3
Duck tanglaoya 8
```

## 样例输出
```
Hello,I am Jumpjump,AOOO.
Hello,I am Piglet,HENGHENG.
There is no Rabbit in our Zoo.
Hello,I am tanglaoya,GAGA.
```

## 优秀代码示例
```C++
// Author: 2016150043 黄泓凯

#include<iostream>
#include<cstdio>
#include<string>

using namespace std;
 
class Animal {
private:
    string type, name;
    int age;
public:
    Animal (string type, string name, int age)
      :type(type), name(name), age(age) {}
    virtual void speak() = 0;
};
 
class Tiger: public Animal {
public:
    Tiger(string type, string name, int age): Animal(type, name, age) {}
    void speak() {
        cout << "Hello,I am " << name << ",AOOO." << endl;
    }
};
 
class Pig: public Animal{
public:
    pig(string type,string name,int age): Animal(type, name, age) {}
    void speak() {
        cout << "Hello,I am " << name << ",HENGHENG." << endl;
    }
};
 
class Duck: public Animal {
public:
    Duck(string type,string name,int age): Animal(type, name, age) {}
    void speak() {
        cout << "Hello,I am " << name << ",GAGA." << endl;
    }
};
 
class Dog: public Animal {
public:
    Dog(string type,string name,int age): Animal(type, name, age) {}
    void speak() {
        cout << "Hello,I am " << name << ",WangWang." << endl;
    }
};
 
int main() {
    int t;
    cin >> t;
    while (t--) {
        string type, name;
        int age;
        Animal *p;
        cin >> type >> name >> age;
        if (type == "Tiger") p = new Tiger(type, name, age);
        else if (type == "Pig") p = new Pig(type, name, age);
        else if (type == "Duck") p = new Duck(type, name, age);
        else if (type == "Dog") p = new Dog(type, name, age);
        else {
            cout << "There is no " << type << " in our Zoo." << endl;
            continue;
        }
        p->speak();
        delete p;
    }
    return 0;
}
```