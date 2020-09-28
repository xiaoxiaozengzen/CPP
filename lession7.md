# C++ sstream 中处理字符串
**答题的代码如下**
```cpp
#include<string>
#include<iostream>
#include<sstream>
using namespace std;
int maxScore(string scores){
	int max = -1;
	
	int num;
	stringstream ss(scores);
	
	while(ss >> num){
		if (num>max) {max = num;}
	}
	return max;
	
}
int main()
{
	string test("12 14 15 36 74");
	int maxScore(string scores);
	cout << maxScore(test);
}
```

`C++`引入`ostringstream`、`istringstream`、`stringstream`这三个类，要使用他们创建对象就必须包含`<sstream>`这个头文件。

`istringstream`的构造函数原形如下：
`istringstream::istringstream(string str)`;
它的作用是从`string`对象`str`中读取字符，`stringstream`对象可以绑定一行字符串，然后以空格为分隔符把该行分隔开来。

下面我们分离以空格为界限，分割一个字符串。
```cpp
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
```
程序输出

`I`

`am `

`coding`

`...`

另外用`vector`也可以实现
```cpp
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
```

`stringstream`是一个类，需要实例化，然后通过重定向符`>>`或者`<<`来进行输出，输入输出符号另一侧需要你是对应的字符类别，比如：
```cpp
stringstream s(str);
int a;
a<<s;
```
