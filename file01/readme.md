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

#3.4（p81）



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













                               
                            
