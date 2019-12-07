# 十月份C++作业
## P301	9.1







----
## P302	9.20



----
## P315	9.29
`vec.resize`可用于改变容器大小：如果当前大小>要求大小-容器后部元素会被删除；如果当前大小<要求大小-新元素将被添加到容器后部。   
vec目前包含25个元素    
(1). `vec.resize(100)`:将75个值为0的元素添加到vec的末尾；   
(2).`vec.resize(10)`:将保留vec的前10的元素，容器后部的15个元素将被删除。 

----
## P324	9.43
从一个string拷贝字符时，如果开始位置大于size，则会抛出out_of_range的异常。
代码如下：
```
#include <iostream>   
using namespace std;    
void huan(string &s, string oldVal, string newVal)   
{    
    string::size_type loc= 0;//loc表示初始位置    
    while (loc<s.length())   
    {
        loc = s.find(oldVal, loc);//从零号位置开始查找
        if (loc == string::npos) //string::npos 为m为搜寻到oldVal的情况
            break;
        s.erase(loc, oldVal.length());//删除旧字符
        s.insert(loc, newVal);//插入新字符
        loc = loc + newVal.length();//更新loc的最后位置
    }   
}    
int main(int argc,char *argv[])    
{   
    string s = "tho thru";    
    huan(s, "tho", "though");//替换简写的单词   
    huan(s, "thru", "through");      
    cout << s << endl;    
    return 0;    
}    
```

----
## P331	9.52
代码如下：
`
#include <iostream>
#include <stack>
using namespace std;
    
int main(int argc,char *argv[])
{
    string s;
    cin>> s ;
    int sum=0;
    stack<char> charstack;
    string::size_type loc=0;
    while(loc< s.length()){
        if(s[loc]=='('){
            while(s[loc]!=')'){
                cout<< s[loc]<<endl;
                charstack.push(s[loc]);
                loc++;
            }
        }//此时停留在‘)’位置
        while(charstack.top()!='('){
            //if(charstack.top()>='0' && charstack.top()<='9')
                sum+=int(charstack.top());
           // charstack.pop();
        }
        charstack.pop();
        charstack.push(sum);
        break;
    }
    cout<< charstack.size()<<endl;
    cout<< int(charstack.top())<<endl;
    cout<< sum<<endl;
}`//以上代码对括号中表达式的处理仅为加法





---
## P339	10.3	
accumulate（定义在<numeric>中）:只读算法
`
vector<int> s;
int sum;
sum=accumulate(s.cbegain(),s.cend(),0);
`
sum即为s中各元素之和。

---
## P349 10.15
lambda表达式：[](){};
`[a](const int b){return a+b};`

---
## P365	10.34
`#include <iostream>
#include <vector>
using namespace std;

void ReverseIterator()
{
    vector<int> iVector;
    int m;
    for (int i = 1; i <= 5; ++i)
    {
        cin >> m;
        iVector.push_back(m);
    }
 
    copy(iVector.rbegin(), iVector.rend(), ostream_iterator<int>(cout," "));
    cout << endl;
}
int main()
{
    ReverseIterator();
    return 0;
}`

---
## P370	10.42
代码如下：
`void quchong(list<string> &words){
    sort(words.begin(), words.end());
    list.unique();
}`

---
## P381	11.12
`
#include <iostream>
#include <vector>
using namespace std;
int main() {
    string a;
    int b;
    vector <pair <string, int> > v;
    while (true) {
        cout << "请输出单词：" << endl;
        cin >> a;
        cout << "请输入数字:" << endl;
        cin >> b;
        v.push_back({ a, b });
        cout << "如果希望停止则输入‘stop’，输入其他以继续" << endl;
        cin >> a;
        if (a == "stop")
            break;
    }
    for (auto &p : v)
        cout << p.first << "   " << p.second << endl;
}
`

---
## P383	11.17	
1.`copy(v.begain(),v.end(),inserter(c,c.end()));`    
2.`copy(v.begain(),v.end(),back_inserter(c));`   
3.`copy(c.begain(),c.end(),inserter(v,v.end()));`    
4.`copy(c.begain(),c.end(),inserter(v));`     
四种调用均为合法，调用解释如下：
1.将v中的元素按照顺序依次插入到c的尾部；
2.同1；
3.将c中的元素按照顺序依次插入到v的尾部；
4.同3。

----
## P396	11.38
单词计数程序，代码如下：
`
#include <iostream>
#include <vector>
#include <string>
#include <unordered_map>
#include <unordered_set>

using namespace std;

void fun()
{
    unordered_map<string, size_t> m;//unordered-无序
    string a;
    while (cin >> a)
    {
        ++m[a];
    }
}
int main()
{
    fun();
    return 0;
}
`


----
## P446	13.12
`bool fun(const Sales_data *trans, Sales_data accum)
{
    Sales_data item1(*trans), item2(accum);
    return item1.isbn() != item2.isbn();
}
`
Q：发生几次析构函数调用？
*分析：* 一共会发生三次析构函数调用。局部变量item1、item2以及临时变量accum在函数结束后销毁；指针trans无析构函数。

---
## P452	13.18



----
## P472	13.46


----
P481	13.49


---
P485	13.58


----
P493	14.3
P500	14.20
P509	14.38
P522	14.52
P539	15.12
P542	15.16
P562	15.30
