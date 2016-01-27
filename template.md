#템플릿(template)
  템플릿(template)이란 무엇인가를 만들기 위한 틀이라는 뜻(템플릿은 붕어빵틀, 템플릿을 가지고 만든 객체는 붕어빵)
## 1.함수 템플릿
  리턴 타입 및 변수의 형만 다른 함수를 여러 형으로 만들어야 한다면 각각 함수를 정의할 필요없이 함수 템플릿을 하나 만들어 여러 함수로 사용이 가능함.

> Example 1

```C++
#include <iostream>
#include <stdio.h>
#include <string.h>

using namespace std;

template <class T>
T Sum(T a, T b)
{
    return a + b;
}

template <>
char *Sum(char *a, char * b)
{
    return strcat(a, b);
}

int main()
{
    char a[80]="hello";
    char *b = " joinc";
    cout << Sum(1, 5) << endl;
    cout << Sum(8.1, 5.5) << endl;
    cout << Sum(8.1, 5.5) << endl;
    cout << Sum(a, b) << endl;
}
```

