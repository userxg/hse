It's an [[alias]] of our variable ***forever***, and we can use it as real variable
- not new variable
- not occupy memory
- they only reference to variable
- `&` - part of the type `int&`

```C++
#include <iostream>

#define LOG(x)  std::cout << x << '\n';

void increment(int& value)
{
	value++;
}

int main()
{
	int a = 0;

	int& ref = a;
	ref = 2;

	const int& size = 65;  //way to declare value
	increment(a);
	increment(ref);
	LOG(a);
	LOG(ref);
}
```

```BASH
4
4
```

- ref to func
```c++

int func(const char * mes){}
int (&reference)(const char*) = func;
```