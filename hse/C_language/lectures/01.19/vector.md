# Implementation


- Header
```C++
class MyVector
{
public:
	MyVector() : top(0), capacity(0), arr(nullptr) {} //fields constructor
	MyVector(int size);
	MyVector(int size, int value);
	MyVector(const MyVector& ref);  //copy constructor
	~MyVector(); //destructor
};
```
- `~` bitwise [[negation]] 
- [[Destructor]] 
- nullptr - Null pointer since c++
- [[Constructor]]
- 