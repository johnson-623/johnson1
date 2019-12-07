# 十月份C++作业             By18061138    赵崇尚
## P301	9.1
Q:* *对于下面的程序任务，vector、deque和list哪种容器最为适合？解释你的选择的理由。如果没有哪一种容器优于其他容器，也请解释理由。*   
(a) 读取固定数量的单词，将它们按字典序插入到容器中。我们将在下一章中看到，关联容器更适合这个问题。   
(b) 读取未知数量的单词，总是将单词插入到末尾。删除操作在头部进行。
(c) 从一个文件读取未知数量的整数。将这些数排序，然后将它们打印到标准输出。   
答：   
（a）列表（list）；题目要求按字典顺序插入容器，可能涉及中间部位插入。 
（b）队列（deque）；涉及容器头尾的插入和删除操作，队列比较合适。
（c）vector。需要容器内元素排序，vector支持随机访问。

---
## P302	9.20
Q：*编写程序，从一个list拷贝元素到两个deque中。值为偶数的所有元素都拷贝到一个deque中，而奇数值元素都拷贝到另一个deque中。*
```
int main(){
    list<int> a = {1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16};
    deque<int> ji,ou;
    list<int>::iterator iter = a.begin();
    while (iter != a.end()){
        if (*iter % 2 == 1)
            ou.push_back(*iter);
        else
            ji.push_back(*iter);
		++iter;
    }
    return 0;
}
```


---
## P315	9.29
`vec.resize`可用于改变容器大小：如果当前大小>要求大小-容器后部元素会被删除；如果当前大小<要求大小-新元素将被添加到容器后部。   
vec目前包含25个元素    
(1). `vec.resize(100)`:将75个值为0的元素添加到vec的末尾；   
(2).`vec.resize(10)`:将保留vec的前10的元素，容器后部的15个元素将被删除。 

---
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
*编译已通过*

---
## P331	9.52
代码如下：
```
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
}//以上代码对括号中表达式的处理仅为加法（编译问题暂未解决）
```


---
## P339	10.3	
accumulate（定义在<numeric>中）:只读算法
```
vector<int> s;
int sum;
sum=accumulate(s.cbegain(),s.cend(),0);
```
sum即为s中各元素之和。

---
## P349 10.15
lambda表达式：`[](){};`    
`[a](const int b){return a+b};`    

---
## P365	10.34
```
#include <iostream>
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
}
```

---
## P370	10.42
代码如下：
```
void quchong(list<string> &words){
    sort(words.begin(), words.end());
    list.unique();
}
```
---
## P381	11.12
```
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
```

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

---
## P396	11.38
单词计数程序，代码如下：
```
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
```
单词替换代码如下：
```
#include <iostream>
#include <fstream>
#include <sstream>
#include <string>
#include <map>
using namespace std;


map<string, string> buildMap(ifstream &map_file) {
	unordered_map<string, string> trans_map;
	string key;
	string value;
	while (map_file >> key && getline(map_file, value)) {
		if (value.size() > 1)
			trans_map[key] = value.substr(1);
		else
			trans_map[key] = value;
	}
	return trans_map;
}

const string& transform(const string &s, const unordered_map<string, string> &m) {
	auto map_iter = m.find(s);
	if (map_iter != m.cend())
		return map_iter->second;
	else
		return s;
}

void word_transform(ifstream &map_file, ifstream &input) {
	auto trans_map = buildMap(map_file);
	string text;
	while (getline(input, text)) {
		istringstream stream(text);    //读取每个单词
		string word;
		bool firstword = true;
		while (stream >> word) {
			if (firstword)
				firstword = false;
			else
				cout << " ";
			cout << transform(word, trans_map);
		}
		cout << endl;
	}
}

int main(int argc,  char* argv[]) {
	ifstream map_file(argv[1]), input(argv[2]);
	word_transform(map_file, input);
	return 0;
}
```

---
## P446	13.12
```
bool fun(const Sales_data *trans, Sales_data accum)
{
    Sales_data item1(*trans), item2(accum);
    return item1.isbn() != item2.isbn();
}
```
Q：发生几次析构函数调用？
*分析：* 一共会发生三次析构函数调用。局部变量item1、item2以及临时变量accum在函数结束后销毁；指针trans无析构函数。

---
## P452	13.18
Q:定义一个Employee类，它包含雇员的姓名和唯一的雇员证号。为这个类定义默认构造函数，以及接受一个表示雇员姓名的string的构造函数。每个构造函数应该通过递增一个static数据成员来生成一个唯一的证号。
代码如下：
```
class Employee {
public:
	Employee() { id = unique++; };
	Employee(const std::string& str) : name(str) { id = unique++; };
private:
	std::string name;
	int id;
	static int unique;
};
int static unique = 0;
```


---
## P472	13.46
Q：什么类型的引用可以绑定到下面的初始化器上？
```
int f();
vector<int> vi(100);
int? r1 = f();
int? r2 = vi[0];
int? r3 = r1;
int? r4 = vi[0] * f();
```
&&:右值引用
&：左值引用
`int&& r1 = f();`右值引用
`int& r2 = vi[0];`左值引用
`int&& r3 = r1;`右值引用
`int& r4 = vi[0 *f();`左值引用

---
P481	13.49
为你的StrVec、String和Message类添加一个移动构造函数和一个移动赋值运算符。
StrVec代码如下：
```
StrVec(StrVec &&s) noexcept : elements(s.elements), first_free(s.first_free), cap(s.cap)
	{ s.elements = s.first_free = s.cap = nullptr; }
	StrVec operator=(StrVec &&rhs)noexcept
	{
		if (this != &rhs) {
			free();
			elements = rhs.elements;
			first_free = rhs.first_free;
			cap = rhs.cap;
			rhs.elements = rhs.cap = rhs.first_free = nullptr;
		}
		return *this;
}
```
String代码如下：
```
String(String &&s) :str(s.str) noexcept
	{
		s.str.clear();
	}
	String operator=(String &&rhs) noexcept
	{
		if (this != &rhs) {
			str.clear();
			str = rhs.str;
		}
		return *this;
	}
```
Message代码如下：
```

Message::Message(Message &&m) :contents(std::move(m.contents)) 
{
	move_Folders(&m);
}
Message Message::operator=(Message &&rhs)
{
	if (this != &rhs) {
		remove_from_Folders();
		contents = std; :move(rhs.contens);
		move_Folders(&rhs);
	}
	return *this;
}

```


---
P485	13.58
Q:编写新版本的 Foo 类，其 sorted 函数中有打印语句，测试这个类，来验证你对前两题的答案是否正确。
代码如下：
```
class Foo
{
public:
	Foo sorted() &&;
	Foo sorted() const &;
private:
	std::vector<int> data;
};

Foo Foo::sorted() &&
{
	std::cout << "Foo Foo::sorted() &&" << std::endl;
	sort(data.begin(), data.end());
	return *this;
}

Foo Foo::sorted() const &
{
	std::cout << "Foo Foo::sorted() const &" << std::endl;
	return Foo(*this).sorted();
}
```

---
P493	14.3
分别使用了以下版本的==：
a) const char     
(b) string     
(c) vector     
(d) string      

---
P500	14.20
*为你的Sales_data类定义加法和复合赋值运算符。*
代码如下：
```
Sales_data operator+(const Sales_data &lhs, const Sales_data &rhs) {
	Sales_data temp(lhs);
	temp += rhs;
	return temp;
}//复合运算符
Sales_data& Sales_data::operator+=(const Sales_data &rhs) {
	units_sold += rhs.units_sold;
	revenue += rhs.revenue;
	return *this;
}//加法运算符
```

---
P509	14.38
Q：*编写一个类令其检查某个给定的string对象的长度是否与一个阀值相等。使用该对象编写程序，统计并报告在输入的文件中长度为1的单词有多少个、长度为2的单词有多少个、……、长度为10的单词又有多少个。*
代码如下：
```
class checklength {
	size_t sz;
	public:
		checklength(size_t n) : sz(n) {}
		bool operator()(const string &str) {
			return str.size() == sz;
	}
}
```


---
P522	14.52
Q:*在下面的加法表达式中分别选用了哪个operator？列出候选函数、可行函数及为每个可行函数的实参执行的类型转换。*

```
struct longDouble {
  	longDouble operator+(const SmallInt&);
  };
  longDouble operator+(longDouble&, double);
  SmallInt si;
  longDouble ld;
  ld = si + ld;
  ld = ld + si;
```


---
P539	15.12
Q:有必要将一个成员函数同时声明成override和final吗？为什么？
A：有必要。override可被使于说明派生类的虚函数。其优点在于能更清晰地传达给编译器我们希望覆盖掉已存在的虚函数。若定义的虚函数与基类中的名字相同而形参列表有异，在不用override关键字的情况下此类定义为合法，使用则为非法；final：当某函数被定义为final，则后续的派生类不允许覆盖该函数。

---
P542	15.16
Q：改写你在15.2.2节练习中编写的数量受限的折扣策略，令其继承Disc_quote。
```
class Limited_quote : public Disc_quote
{
	Limited_quote(const string &book = "", double sales_price = 0.0, size_t qty = 0, double disc_rate = 0.0) : Disc_quote(book, sales_price, qty, disc_rate) { }
	double net_price(size_t cnt) const override
	{
		if (cnt <= quantity)
			return cnt * (1 - discount) * price;
		else
			return quantity * (1 - discount) * price + (cnt - quantity) *price;
	}
};
```

---
P562	15.30
Q:编写你自己的Basket类，用它计算上一个练习中交易记录的总价格。
```
class Basket
{
public:
	void add(const std::shared_ptr<Quote> &sale) { items.insert(sale); }
	double total_receipt(std::ostream&) const;
private:
	static bool jijiao(const std::shared_ptr<Quote> &lhs, const std::shared_ptr<Quote> &rhs)
	{
		return lhs->isbn() < rhs->isbn();
	}
	std::multiset<std::shared_ptr<Quote>, decltype(compare)*> items{compare};
};
 
double Basket::total_receipt(ostream &os) const
{
	double sum = 0.0;
	for(auto iter = items.cbegin(); iter != items.cend(); iter = items.upper_bound(*iter))
	{
		sum += print_total(os, **iter, items.count(*iter));
	}
	os << "总价为: " << sum << endl;
	return sum;
}
```
PS：该代码参考实例修改而来
