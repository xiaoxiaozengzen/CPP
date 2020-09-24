
此外，插一句，c++内存被分为5个区，分别是堆、栈、自由存储区、全局/静态存储区和常量存储区。
---
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
