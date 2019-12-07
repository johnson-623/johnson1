# 十月份C++作业
## P301	9.1









## P302	9.20
## P315	9.29
`vec.resize`可用于改变容器大小：如果当前大小>要求大小-容器后部元素会被删除；如果当前大小<要求大小-新元素将被添加到容器后部。   
vec目前包含25个元素    
(1). `vec.resize(100)`:将75个值为0的元素添加到vec的末尾；   
(2).`vec.resize(10)`:将保留vec的前10的元素，容器后部的15个元素将被删除。 

----
## P324	9.43
从一个string拷贝字符时，如果开始位置大于size，则会抛出out_of_range的异常。
代码如下：
`#include <iostream>
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
}`

----
P331	9.52



---
P339	10.3	10.15
P365	10.34
P370	10.42
P381	11.12
P387	11.17	
P396	11.38
P446	13.12
P452	13.18
P472	13.46
P481	13.49
P485	13.58
P493	14.3
P500	14.20
P509	14.38
P522	14.52
P539	15.12
P542	15.16
P562	15.30
