# 问题 A: 在职研究生（多重继承）

## 题目描述

1、建立如下的类继承结构：
1)        定义一个人员类CPeople，其属性（保护类型）有：姓名、性别、年龄；
2)        从CPeople类派生出学生类CStudent，添加属性：学号和入学成绩；
3)        从CPeople类再派生出教师类CTeacher，添加属性：职务、部门；
4)        从CStudent和CTeacher类共同派生出在职研究生类CGradOnWork，添加属性：研究方向、导师；
2、分别定义以上类的构造函数、输出函数print及其他函数（如需要）。
3、在主函数中定义各种类的对象，并测试之。

## 输入

第一行：姓名性别年龄
第二行：学号成绩
第三行：职务部门
第四行：研究方向导师

## 输出

第一行：People:
第二行及以后各行：格式见Sample

## 样例输入
```
wang-li m 23
2012100365 92.5
assistant computer
robot zhao-jun
```

## 样例输出
```
People:
Name: wang-li
Sex: m
Age: 23

Student:
Name: wang-li
Sex: m
Age: 23
No.: 2012100365
Score: 92.5

Teacher:
Name: wang-li
Sex: m
Age: 23
Position: assistant
Department: computer

GradOnWork:
Name: wang-li
Sex: m
Age: 23
No.: 2012100365
Score: 92.5
Position: assistant
Department: computer
Direction: robot
Tutor: zhao-jun
```

## 优秀代码示例
```C++
#include<iostream>
#include<string>

using namespace std;

class CPeople {
protected:
    string name, sex;
    int age;
public:
    CPeople(string name, string sex, int age): name(name), sex(sex), age(age) {};
    void print() {
        cout << "People:" << endl;
        cout << "Name: " << name << endl;
        cout << "Sex: " << sex << endl;
        cout << "Age: " << age << endl;
        cout << endl;
    }
};

class CStudent : virtual public CPeople {
protected:
    string ID;
    double score;  
public:
    CStudent(string id, double score, string name, string sex, int age)
        :ID(id), score(score), CPeople(name, sex, age) {};
    void print() {
        cout << "Student:" << endl;
        cout << "Name: " << name << endl;
        cout << "Sex: " << sex << endl;
        cout << "Age: " << age << endl;
        cout << "No.: " << ID << endl;
        cout << "Score: " << score << endl;
        cout << endl;
    }
};

class CTeacher : virtual public CPeople {
protected:
    string position, department;
public:
    CTeacher(string position, string department, string name, string sex, int age)
        :position(position), department(department), CPeople(name, sex, age) {};
    void print() {
        cout << "Teacher:" << endl;
        cout << "Name: " << name << endl;
        cout << "Sex: " << sex << endl;
        cout << "Age: " << age << endl;
        cout << "Position: " << position << endl;
        cout << "Department: " << department << endl;
        cout << endl;
    }
};

class CGradeOnWork :public CStudent, public CTeacher {
protected:
    string direction, tutor;
public:
    CGradeOnWork(string direction, string tutor, string id, double score, string position, string department, string name, string sex, int age)
        :direction(direction), tutor(tutor), CStudent(id, score, name, sex, age), CTeacher(position, department, name, sex, age), CPeople(name, sex, age) {};
    void print() {
        cout << "GradOnWork:" << endl;
        cout << "Name: " << CPeople::name << endl;
        cout << "Sex: " << CPeople::sex << endl;
        cout << "Age: " << CPeople::age << endl;
        cout << "No.: " << CStudent::ID << endl;
        cout << "Score: " << CStudent::score << endl;
        cout << "Position: " << CTeacher::position << endl;
        cout << "Department: " << CTeacher::department << endl;
        cout << "Direction: " << direction << endl;
        cout << "Tutor: " << tutor << endl;
    }
};
 
int main() {
    string name, sex;
    int age;
    string ID;
    double score;
    string position, department;
    string direction, tutor;
    cin >> name >> sex >> age >> ID >> score >> position >> department >> direction >> tutor;
    CPeople a(name, sex, age);
    CStudent b(ID, score, name, sex, age);
    CTeacher c(position, department, name, sex, age);
    CGradeOnWork d(direction, tutor, ID, score, position, department, name, sex, age);
    a.print();
    b.print();
    c.print();
    d.print();
}
```