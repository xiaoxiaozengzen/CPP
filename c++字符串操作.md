c++字符创操作
==========
选用`C++`标准程序库中的`string`类，是因为他和`c-string`比较起来，不必担心内存是否足够、字符串长度等等，而且作为一个类出现，他集成的操作函数足以完成我们大多数情况下(甚至是100%)的需要。
我们可以用 `= `进行赋值操作，`==` 进行比较，`+ `做串联。
首先，为了在我们的程序中使用string类型，我们必须包含头文件 。如下：
```cpp
#include //注意这里不是string.h string.h是C字符串头文件
```
---

# 定义和构造初始化

声明一个字符串变量很简单：
```cpp
string Str;
```
这样我们就声明了一个字符串变量，但既然是一个类，就有构造函数和析构函数。上面的声明没有传入参数，所以就直接使用了`string`的默认的构造函数，这个函数所作的就是把`Str`初始化为一个空字符串。
`String`类的构造函数和析构函数如下：
```cpp
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
```cpp
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

## `=`,`assign()` //赋以新值

`“=”`的用法不作详细说明,`assign`用法如下：
```cpp
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

```cpp
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
```cpp
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
## insert() //插入字符
在`string`中间的某个位置插入字符串，可以用`insert()`函数，这个函数需要指定一个安插位置的索引，被插入的字符串将放在这个索引的后面。
`s.insert(0,”my name”);`
`s.insert(1,str);`
这种形式的`insert()`函数不支持传入单个字符，这时的单个字符必须写成字符串形式。注意：为了插入单个字符，`insert()`函数提供了两个对插入单个字符操作的重载函数：`insert(size_type index,size_type num,chart c)`和`insert(iterator pos,size_type num,chart c)`。其中`size_type`是无符号整数，`iterator`是`char*`,所以，这么调用`insert`函数是不行的：`insert(0,1, ’j’)`;这时候第一个参数将转换成哪一个呢？所以必须这么写：`insert((string::size_type)0,1,’j’)`！第二种形式指出了使用迭代器安插字符的形式，在后面会提及。顺便提一下，`string`有很多操作是使用STL的迭代器的，他也尽量做得和`STL`靠近。
## erase() //删除字符
```cpp
s.erase(13);//从索引13开始往后全删除
s.erase(7,5);//从索引7开始往后删5个
```
## clear() //删除全部字符**
用法不作说明；
## replace() //替换字符
```cpp
string s=”il8n”;
s.replace(1,2,”nternationalizatio”);//从索引1开始的2个替换成后面的
C_string s = internationalization
```
## + //串联字符串
## ==,!=,<,<=,>,>=,compare() //比较字符串
`C++`字符串支持常见的比较操作符`（>,>=,<,<=,==,!=）`，甚至支持`string`与`C-string`的比较(如 `str<”hello”)`。在使用`>,>=,<,<=`这些操作符的时候是根据“当前字符特性”将字符按字典顺序进行逐一得比较。字典排序靠前的字符小，比较的顺序是从前向后比较，遇到不相等的字符就按这个位置上的两个字符的比较结果确定两个字符串的大小。
另一个功能强大的比较函数是成员函数`compare()`。他支持多参数处理，支持用索引值和长度定位子串来进行比较。他返回一个整数来表示比较结果，返回值意义如下：0-相等 >0-大于 <0-小于。举例如下：
```cpp
string s(“abcd”);
s.compare(“abcd”); //返回0
s.compare(“dcba”); //返回一个小于0的值
s.compare(“ab”); //返回大于0的值
s.compare(s); //相等
s.compare(0,2,s,2,2); //用”ab”和”cd”进行比较小于零
s.compare(1,2,”bcx”,2); //用”bc”和”bc”比较。
```
## size(),length() //返回字符数量
现有的字符数，函数是`size()`和`length()`，他们等效。
## max_size() //返回字符的可能最大个数???
`max_size()` 这个大小是指当前`C++`字符串最多能包含的字符数，很可能和机器本身的限制或者字符串所在位置连续内存的大小有关系。我们一般情况下不用关心他，应该大小足够我们用的。但是不够用的话，会抛出`length_error`异常
## empty() //判断字符串是否为空
`Empty()`用来检查字符串是否为空。
## capacity() //返回重新分配之前的字符容量
`capacity()`重新分配内存之前 `string`所能包含的最大字符数。
## reserve() //保留一定量内存以容纳一定数量的字符
这个函数为`string`重新分配内存。重新分配的大小由其参数决定，默认参数为`0`，这时候会对`string`进行非强制性缩减。
## [ ], at() //存取单一字符
可以使用下标操作符`[]`和函数`at()`对元素包含的字符进行访问。但是应该注意的是操作符`[]`并不检查索引是否有效（有效索引`0~str.length()`），如果索引失效，会引起未定义的行为。而`at()`会检查，如果使用 `at()`的时候索引无效，会抛出`out_of_range`异常。
```cpp
 string str1 = "Iphone 5";
   cout<<str1[2]<<endl; // = h
   cout<<str1.at(4)<<endl; // = n

    string stuff;
    getline(cin,stuff); // 输入一行字符赋值给stuff
    getline(cin,stuff,'!'); // 输入一行字符以“！”结束
    cout<<stuff<<endl;
```
## >>,getline() //从stream读取某值
## << //将谋值写入stream
## copy() //将某值赋值为一个C_string
```cpp
c_str() //将内容以C_string返回
data() //将内容以字符数组形式返回
```
`C++`提供的由`C++`字符串得到对应的`C_string`的方法是使用`data()`、`c_str()`和`copy()`，其中，`data()`以字符数组的形式返回字符串内容，但并不添加`’\0’`。`c_str()`返回一个以`‘\0’`结尾的字符数组，而`copy()`则把字符串的内容复制或写入既有的c`_string`或字符数组内。`C++`字符串并不以`’\0’`结尾。我的建议是在程序中能使用`C++`字符串就使用，除非万不得已不选用`c_string`。
## substr() //返回某个子字符串
```cpp
substr(),形式如下：
s.substr();//返回s的全部内容
s.substr(11);//从索引11往后的子串
s.substr(5,6);//从索引5开始6个字符
```
## 查找函数
查找函数很多，功能也很强大，包括了：
```cpp
find()
rfind()
find_first_of()
find_last_of()
find_first_not_of()
find_last_not_of()
```
这些函数返回符合搜索条件的字符区间内的第一个字符的索引，没找到目标就返回`npos`。所有的函数的参数说明如下：
第一个参数是被搜寻的对象。第二个参数（可有可无）指出`strin`g内的搜寻起点索引，第三个参数（可有可无）指出搜寻的字符个数。比较简单，不多说不理解的可以向我提出，我再仔细的解答。当然，更加强大的`STL`搜寻在后面会有提及。
最后再说说`npos`的含义，`string::npos`的类型是`string::size_type`,所以，一旦需要把一个索引与`npos`相比，这个索引值必须是`string::size)type`类型的，更多的情况下，我们可以直接把函数和`npos`进行比较（如：`if(s.find(“jia”)== string::npos)`）。
