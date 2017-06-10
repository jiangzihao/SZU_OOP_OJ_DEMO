# 问题 C: 矩阵相加（运算符重载）

## 题目描述

已知一个矩阵包含行数m、列数n、数值data三个属性，包含初始化、输出、相加等操作，要求

1. 在类定义中，矩阵的data属性是一个整数指针型指针。只有创建对象时，根据外来输入的行数和列数，才把指针变成一个二维数组

2. 用运算符重载的方法实现两个矩阵对象的相加，矩阵相加是指两个矩阵的每个位置上的两个元素相加

3. 用构造函数实现对象的初始化，用输出函数实现矩阵的输出。提示：在构造函数内做输入可以减少很多麻烦

整数指针变成二位数组的参考代码
```C++
//m和n是行数和列数
int m, n;
int **data;
int i, j;
cin>>m>>n;
data=new int*[m];  //先创建m行
for(i=0;i<m;i++) 
  { data[i]=new int[n]; }  //再创建n列

for (i=0; i<m; i++)
  for (j=0; j<n; j++)
    cin>>data[i][j];
```

## 输入

第一行输入t表示t个实例

第二行输入第一个示例的矩阵的行数和列数，两个矩阵的行数和列数都是相同的

第三行起，输入第一个矩阵的具体数据

依次类推，输入第二个矩阵的具体数据

依次类推，输入下一个示例的数据

## 输出

输出每两个矩阵相加的结果，每个示例结果之间用一个回车分隔开

### 样例输入
```
2
2 3
1 2 3 
4 5 6
-1 -2 -3
6 5 4
2 2
11 22
33 44
55 66
77 88
```

## 样例输出
```
0 0 0
10 10 10
66 88
110 132
```

## 优秀代码示例
```C++
#include <iostream>
#include <string>

using namespace std;

class Martix {
private:
    int m, n;
    int **data;
public:
    // 构造函数
    Martix(int m, int n): m(m), n(n) {
        if (m > 0 && n > 0) {
            data = new int*[m];
            for (int i = 0; i < m; i++) {
                data[i] = new int[n];
                // 在构造函数内输入
                for (int j = 0; j < n; j++) cin >> data[i][j];
            }
        }
    }
    // 拷贝构造函数
    // 注意在此处形参为常量引用
    // 是由于C++规定，只有常量引用能引用常量(临时对象)，而一般引用不能引用常量(临时对象)
    Martix(const Martix &p): m(p.m), n(p.n) {
        data = new int*[m];
        for (int i = 0; i < m; i++) {
            data[i] = new int[n];
            for (int j = 0; j < n; j++) data[i][j] =  p.data[i][j];
        }
    }
    // 此处应当返回对象而非对象引用，且不应该修改参数的值
    // 因为加法并不修改两个参数的值
    Martix operator +(const Martix &p) {
        // 用于保存结果的矩阵
        Martix result(p);
        for (int i = 0; i < result.m; i++) {
            for (int j = 0; j < result.n; j++) {
                result.data[i][j] += data[i][j];
            }
        }
        return result;
    }
    // 输出函数
    void show() const {
        for (int i = 0; i < m; i++) {
            cout << data[i][0];
            for (int j = 1; j < n; j++) {
                cout << ' ' << data[i][j];
            }
            cout << endl;
        }
    }
    ~Martix() {
        // 先释放一级指针
        for (int i = 0; i < m; i++) delete []data[i];
        // 最后释放二级指针
        delete []data;
    }
};

int main() {
    int t;
    cin >> t;
    while (t--) {
        int m, n;
        cin >> m >> n;
        Martix p1(m, n);
        Martix p2(m, n);
        (p1 + p2).show();
    }
    return 0;
}
```