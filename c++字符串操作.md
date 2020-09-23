c++字符创操作
==========
选用`C++`标准程序库中的`string`类，是因为他和`c-string`比较起来，不必担心内存是否足够、字符串长度等等，而且作为一个类出现，他集成的操作函数足以完成我们大多数情况下(甚至是100%)的需要。
我们可以用 `= `进行赋值操作，`==` 进行比较，`+ `做串联。
首先，为了在我们的程序中使用string类型，我们必须包含头文件 。如下：
```shell
#include //注意这里不是string.h string.h是C字符串头文件
```

---

# 定义和构造初始化

声明一个字符串变量很简单：
```shell
string Str;
```
这样我们就声明了一个字符串变量，但既然是一个类，就有构造函数和析构函数。上面的声明没有传入参数，所以就直接使用了`string`的默认的构造函数，这个函数所作的就是把`Str`初始化为一个空字符串。
`String`类的构造函数和析构函数如下：
```shell
string s; //生成一个空字符串s
string s(str) //拷贝构造函数 生成str的复制品
string s(str,stridx) //将字符串str内“始于位置stridx”的部分当作字符串的初值
string s(str,stridx,strlen) //将字符串str内“始于stridx且长度顶多strlen”的部分作为字符串的初值
string s(cstr) //将C字符串作为s的初值
string s(chars,chars_len) //将C字符串前chars_len个字符作为字符串s的初值。
string s(num,c) //生成一个字符串，包含num个c字符
string s(beg,end) //以区间beg;end(不包含end)内的字符作为字符串s的初值
s.~string() //销毁所有字符，释放内存
```
**测试如下：**
```shell
# include <iostream>
# include <string>
using namespace std;
int main()
{
    string str1 = "yesterday once more";
    string str2 ("my heart go on");
    string str3 (str1,6); // = day once more
    string str4 (str1,6,3); // = day

    char ch_music[] = {"Roly-Poly"};

    string str5 = ch_music; // = Roly-Poly 
    string str6 (ch_music); // = Roly-Poly
    string str7 (ch_music,4); // = Roly
    string str8 (10,'i'); // = iiiiiiii
    string str9 (ch_music+5, ch_music+9); // = Poly

    str9.~string();

    //cout<<str9<<endl; // 测试输出

    getchar();
    return 0;
}
```

---

# 字符串操作函数

这里是C++字符串的重点

##`=`,`assign()` //赋以新值

`“=”`的用法不作详细说明,`assign`用法如下：
```shell
# include <iostream>
# include <string>
using namespace std;
int main()
{
    string str1 = "yesterday once more";
    string str2 ("my heart go on");
    string str3,str4;

    str3.assign(str2,3,6);  // = heart
    str4.assign(str2,3,string::npos); // = heart go on (从2开始到结尾赋给str4)
    str4.assign("gaint"); // =gaint
    str4.assign("nico",5); // = nico，超出长度会发生什么。。。
    str4.assign(5,'x'); // = xxxxx
    cout<<str4<<endl;

    getchar();
    return 0;
}
```

## `swap()` //交换两个字符串的内容

```shell
# include <iostream>
# include <string>
using namespace std;
int main()
{
    string str1 = "yesterday once more";
    string str2 ("my heart go on");

    str2.swap(str1);
    cout<<str1<<endl; // = my heart go on
    cout<<str2<<endl; // = yesterday once more

    getchar();
    return 0;
}
```

## `+=,append(),push_back()` //在尾部添加字符

增加字符（这里说的增加是在尾巴上），函数有 `+=、append()、push_back()`。举例如下：
```shell
s+=str;//加个字符串
s+=”my name is jiayp”;//加个C字符串
s+=’a’;//加个字符
s.append(str);
s.append(str,1,3);//不解释了同前面的函数参数assign的解释
s.append(str,2,string::npos)//不解释了
s.append(“my name is jiayp”);
s.append(“nico”,5);
s.append(5,’x’);
s.push_back(‘a’);//这个函数只能增加单个字符
```
