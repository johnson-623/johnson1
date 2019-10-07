*Now this is my begain of using this amazing item!

#2.23（p51）
答：若指针拥有一个合法值，则能将它用在条件表达式中。使用非法指针作为条件或者参与比较都会报错。

#2.24
答：viod*可用于存放任意类型数据的地址；而long*只能用于存放long类型的数据。

#2.25(p53)
a).ip为int类型的指针，i为int类型，r为指针i的引用；
b).i为int类型，ip为int类型指针；
c).ip为int类型指针，ip2为int类型。

#2.35（p62）**const 对象必须初始化**
整型常量-i、j2；整型常量引用-k、k2；整型-j；整型指针-p；

**验证程序**：
const int i = 42;
auto j = i;//i为常量，auto判断会忽略顶层const，故j为int变量
j = 0; //赋值成功，j为int型

const auto &k = i; // 
// k = 0; //赋值失败，因为k为const int&

auto *p = &i;
// *p = 0; //赋值失败，*p不可修改，因为p为const int *

const auto j2 = i, &k2 = i; 
// j2 = 0; //赋值失败，j2为const int，j2值不可修改
// k2 = 0; //赋值失败，k2为const int&, k2值不可修改

#3.4（p81）

**判断字符串大小**：
***代码***：

#include <iostream>
#include <string>

using std::string;
using std::cin;
using std::cout;
using std::endl;

int main()
{
    string s1, s2;
    cout << "Please input string s1 and s2:" << endl;
    while(cin >> s1 >> s2)
    {
    if (s1==s2)
      cout << "String s1 and s2 are same! " << endl;
    else if(s1 > s2)
      cout << "String s1 is bigger and s1 is: " << s1 << endl;
    else 
      cout << "String s2 is bigger and s2 is: " << s2 << endl;
    }
    return 0;
 }
 
 
**判断字符串等长**：
***代码***：

#include <iostream>
#include <string>

using std::string;
using std::cin;
using std::cout;
using std::endl;

int main()
{
    string s1, s2;
    while (cin >> s1 >> s2)
    {
        if (s1.size() == s2.size())
        cout << "s1 and s2 have the same size! "<<endl;
        else if(s1.size() > s2.size())
        cout << "The size of s1 is bigger : " << s1 << endl;
        else 
        cout << "The size of s2 is bigger : " << s2 << endl;
    }
    return 0;
}

#3.5(p81)
**连接字符串并输出**
***代码***：
#include <iostream>

using std::string;
using std::cin;
using std::cout;
using std::endl;

int main()
{
    string s1, s2;
    while (cin >> s2)
    {
        s1 += s2;
    }
    cout << s1 << endl;
    return 0;
}

#3.20（p94）


**#3.23（p99）**
#include <iostream>
#include <vector>
#include<cctype>
using namespace std;
int main()
{
	vector<int>ivec(10,1);//定义一个int类型的容器ivec
	int ival;
	cout<<"请输入10个整型数字！"<<endl;
	for(vector<int>::iterator iter = ivec.begin();iter<ivec.end();++iter)//使用迭代器访问vector中的元素
	{
	   cout<<(*iter)*2<<endl;
	}
	   if(ivec.size()==0)//如果容器为空，则输入No element! 并退出
	{
	   cout<<"No element!"<<endl;
	   return -1;
	}
	return 0;
}


#6.20（p188）
void change(int *q,int *p)
{
  int t;
  t=*p;
  *p=*q;
  *q=t;
}
int n,m;
cin>>n>>m;
change(&n,&m);
cout<<"n="<<n<<"m="<<m;

#6.19(p193)
(b)合理；
(a)不合理:括号中参数只有一个，而调用时却出现两个数值；
(c)不合理:参数类型为double，而调用时却为整型；
(d)不合理:参数第三项为int，调用时却为浮点型；

#6.39（p210）
(a)：第二条声明是为计算两个整型常量。不合法，因为无法和第一条进行区分；
(b)：第二条声明为得到double类型的get()函数。不合法，因为不能使用不同的返回值类型对函数进行重载；
(c)：重置一个double类型的变量。合法。

#7.16（p241）


#7.27（p249）

#7.49（p266）

#7.58（p272）










                               
                            
