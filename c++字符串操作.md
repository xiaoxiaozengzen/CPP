c++字符创操作
==========
选用`C++`标准程序库中的`string`类，是因为他和`c-string`比较起来，不必担心内存是否足够、字符串长度等等，而且作为一个类出现，他集成的操作函数足以完成我们大多数情况下(甚至是100%)的需要。
我们可以用 `= `进行赋值操作，`==` 进行比较，`+ `做串联。
首先，为了在我们的程序中使用string类型，我们必须包含头文件 。如下：
```shell
`#include` //注意这里不是`string.h` `string.h`是C字符串头文件
```
#定义和构造初始化
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
测试如下：
