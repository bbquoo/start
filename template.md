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
  위에서 보듯 정수 및 실수 형태는 처음에 정의한 템플릿으로 처리가 가능하지만 char\*의 경우 +연산이 없기때문에 에러가 난다. 
  그래서 아래에 변수만 char\*로 지정하여 부분 특수화 시켜주었다. 위 코드의 결과는 아래와 같다.
```
6
13.6
13.6
hello joinc
```

## 2. 클래스 템플릿
  클래스 템플릿은 클래스의 틀이 되는 용도임. 구조와 구현 알고리즘을 동일하되 멤버들의 타입만 다를 경우 사용 가능함. 
  
> Example 2

```C++
#include <iostream>
using namespace std;

template <typename T>
class PosValue
{
public:
	PosValue(int ax, int ay, T av) : m_X(ax), m_Y(ay), m_Value(av) { }
	void OutValue();
private:
	int m_X, m_Y;
	T m_Value;
};

template <typename T>
void PosValue<T>::OutValue()
{
	printf("x: %d, y: %d\n", m_X, m_Y);
	cout << m_Value << endl;
}

void main()
{
	PosValue<int> iv(1, 1, 2);
	PosValue<char> cv(5, 1, 'C');
	PosValue<double> dv(30, 2, 3.14);
	iv.OutValue();
	cv.OutValue();
	dv.OutValue();

	getchar();
	return;
}
```
  위 예시처럼 클래스 생성자를 호출시 필요한 인수의 타입을 '<>'에 써야한다.
  함수 템플릿과 마찬가지로 클래스 템플릿도 단순한 선언에 불과하며 컴파일러는 이 템플릿 모양을 기억해두었다가 객체가 생성될때 표시된 타입에 맞게 구체화 한다. 템플릿 선언만 있을 경우 템플릿은 무시된다. 클래스안에 추가로 템플릿 추가가 가능하다.
  
### - 클래스 템플릿 특수화
