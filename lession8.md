
此外，插一句，c++内存被分为5个区，分别是堆、栈、自由存储区、全局/静态存储区和常量存储区。

这是我的代码
===
```cpp
#include <string>
#include <cstring>
#include <stdio.h>
#include <ctype.h>
#include <iostream>
using namespace std;

//move each char by offset
char * encode(string s,int offset){//返回字符指针，指向一个字符串数组
	char *res = new char[s.size()];//定义一个s大小的字符串数组，用字符指针res指向他
	
	int index = 0;
	for (int i=0; i<s.size();i++){
		 int true_offset = s[i]+(offset%26);
	        if (s[i]<=122 && s[i]>=97){
				
				true_offset = (true_offset > 122) ? true_offset-26: true_offset;
				true_offset = (true_offset < 97) ? true_offset+26: true_offset;
				
				res[index] = (char) true_offset;
				
	        }
	        else if(s[i]<=90 && s[i]>=65){
				
				true_offset = (true_offset > 90) ? true_offset-26: true_offset;
				true_offset = (true_offset < 65) ? true_offset+26: true_offset;
				
				res[index] = (char) true_offset;
	        }
			else{
				res[index] = s[i];
			}
			index++;
	}
	
	return res;
}
```

# warning: ISO C++ forbids converting a string constant to 'char*' [-Wwrite-strings]
在C++中，
```cpp
char* p = "abc";　　// valid in C, invalid in C++
```
会跳出警告：`warning: ISO C++ forbids converting a string constant to 'char*' [-Wwrite-strings]`

改成下面会通过`warning`
```cpp
char* p = (char*)"abc";  // OK
```
或者改成下面：
```cpp
char const *p = "abc";　　// OK
```
原因解析：

		我们在学习`c`或者`c++`的时候都知道，如果在赋值操作的时候，等号两边的变量类型不一样，那么编译器会进行一种叫做 `implicit conversion` 的操作来使得变量可以被赋值。

 

在我们上面的表达式中就存在这样的一个问题，等号右边的`"abc"`是一个不变常量，在`c++`中叫做`string literal`，`type`是`const char *`，而p则是一个`char`指针。如果强行赋值会发生什么呢？没错，就是将右边的常量强制类型转换成一个指针，结果就是我们在修改一个`const`常量。编译运行的结果会因编译器和操作系统共同决定，有的编译器会通过，有的会抛异常，就算过了也可能因为操作系统的敏感性而被杀掉。


像这种直接将`string literal` 赋值给指针的操作被开发者们认为是deprecated，只不过由于以前很多代码都有这种习惯，为了兼容，就保留下来了。

 
