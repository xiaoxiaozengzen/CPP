#C++ sstream 中处理字符串
C++引入ostringstream、istringstream、stringstream这三个类，要使用他们创建对象就必须包含<sstream>这个头文件。

istringstream的构造函数原形如下：
istringstream::istringstream(string str);
它的作用是从string对象str中读取字符，stringstream对象可以绑定一行字符串，然后以空格为分隔符把该行分隔开来。

下面我们分离以空格为界限，分割一个字符串。
#include<iostream>
#include<sstream>
#include<string>
int main()
{
    std::string str = "I am coding ...";
    std::istringstream is(str);
    do
    {
        std::string substr;
        is>>substr;
        std::cout << substr << std::endl;
    } while (is);
    return 0;
}
程序输出

I

am 

coding

...

另外用vector也可以实现
#include <vector>
#include<iostream>
#include <string>
#include <sstream>
using namespace std;
int main()
{
    string str("I am coding ...");
    string buf;
    stringstream ss(str); 
    vector<string> vec; 
    while (ss >> buf)
        vec.push_back(buf);
    for (vector<string>::iterator iter = vec.begin(); iter != vec.end(); ++iter)
    {
        cout << *iter << endl;
    }
    return 0;
}
