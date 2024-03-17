main from [[over opers]] 
- double overload (inside class)
```C++
Rational::operator double() const
{
	return double(this->numer)/ this->denom;
}
```


- istream overload (only outside class function)
```C++
std::istream& operator>>(std::istream& input, Rational& obj)
{
	int numer, denom;
	input >> numer >> denom;
	obj.set_rational(numer, denom);
	return input;
}
```

# = overload (deep copy)
### algorithm
1. self-assign protection
2. Cleaning previously allocated memory
3. Allocation of a new memory block an work with it
4. Return a modified object
When we work with system object in our class we need to have
1. Default Constructor
2. Copy Constructor
3. Destructor
4. Assign overload


```C++
MyVector& MyVector::operator=(const MyVector& ref)
{
	{
		if (this != &ref) //check
		{
			delete[] this->arr; //clean
			this->arr = new int[this->capacity = ref.capacity]; //new
			for (this->top = 0; this->top < ref.top; ++this->top) //work with new
				this->arr[this->top] = ref[this->top];
		}	
		return *this; //return modified
		
	}
}
```
- but we need to overload `[]`

## `[]` overload
- can be const and not (use `<stdexcept>`)
```C++
int MyVector::operator[](int index) const
{
	if (index >= 0 && index < top)
		return this->arr[index];
	else
		throw std::out_of_range("Wrong index");
}

int& MyVector::operator[](int index)
{
	if (index >= 0 && index < top)
		return this->arr[index];
	else
		std::out_of_range("Wrong index");
}
```

- returns only *reference* to provide access
- inline - non recursive, don't complex function, functions in header can be inline;


# FULL Code VECTOR 

## header
```C++
#pragma once
#include <iostream>

class MyVector
{
	//friend int main();

public:
	MyVector() : top(0), capacity(0), arr(nullptr) { counter++; }
	MyVector(int size);
	MyVector(int size, int value);
	explicit MyVector(const MyVector& ref);
	~MyVector();
	static int getCounter() { return MyVector::counter; }

	//get-set
	int getTop() const{ return this->top; }
	int getCapacity() const { return this->capacity; }
	//void setCapacity(int t);
	void addElement(int value);

	MyVector& operator=(const MyVector& ref);

	int operator[](int index) const;
	int& operator[](int index);
	

private:
	int* arr;
	int top;
	int capacity;
	static int counter;

};


std::istream& operator>>(std::istream& inp, MyVector& obj);
std::ostream& operator<<(std::ostream& out, const MyVector& obj);
```

## cpp
```C++
#include "vector.h"
#include <stdexcept>

int MyVector::counter = 0;

MyVector::MyVector(int size) : top(0), capacity(size), arr(nullptr)
{
	counter++;
	if (capacity)
		arr = new int[capacity];
	//arr = (int*)malloc(size*sizeof(int))
}

MyVector::MyVector(int size, int value) : MyVector(size)
{
	for (;top < capacity; top++)
		arr[top] = value;
}

MyVector::MyVector(const MyVector& ref) : MyVector(ref.capacity)
{
	for (; top < ref.top; top++)
		arr[top] = ref.arr[top];
}



MyVector::~MyVector()
{
	counter--;
	if (arr)
		delete[] arr;
}

//why do nothing if  t < capacity
//void MyVector::setCapacity(int t)
//{
//	if (t > this->capacity)
//	{
//		int* temp = new int[this->capacity = t];
//		/*for (int i = 0; i < this->top; ++i)
//			temp[i] = this->arr[i];*/
//		delete[] this->arr;
//		arr = temp;
//	}
//	top = 0;
//
//}

void MyVector::addElement(int value)
{
	if (this->top == this->capacity)
	{											//capacity can be 0
		int* temp = new int[this->capacity = this->capacity*2 + 1];
		for (int i = 0; i < this->top; ++i)
			temp[i] = this->arr[i];
		delete[] this->arr;
		arr = temp;
	}
	this->arr[top++] = value;
}

MyVector& MyVector::operator=(const MyVector& ref)
{
	{
		if (this != &ref)
		{
			delete[] this->arr;
			this->arr = new int[this->capacity = ref.capacity];
			for (this->top = 0; this->top < ref.top; ++this->top)
				this->arr[this->top] = ref[this->top];
		}	
		return *this;
		
	}
}

int MyVector::operator[](int index) const
{
	if (index >= 0 && index < top)
		return this->arr[index];
	else
		throw std::out_of_range("Wrong index");
}

int& MyVector::operator[](int index)
{
	if (index >= 0 && index < top)
		return this->arr[index];
	else
		std::out_of_range("Wrong index");
}

std::istream& operator>>(std::istream& inp, MyVector& obj)
{
	int size;
	inp >> size;
	
	for (int i = 0; i < size; ++i)
	{
		int temp = 0;
		inp >> temp;
		obj.addElement(temp);
	}
	return inp;
}

std::ostream& operator<<(std::ostream& out, const MyVector& obj)
{
	for (int i = 0; i < obj.getTop(); ++i)
	{
		out << obj[i] << " ";
	}

	return out;
}
```


## main
```C++
#include <iostream>
#include "vector.h"
#include <vector>


void somFunc(MyVector vec)
{

}

int main()
{
	//constructors demonstration
	int a(5);
	MyVector v1;
	MyVector v2(10, 5);
	MyVector v3(v1);

	std::cout << MyVector::getCounter() << std::endl;
	std::cout << v3.getCounter() << std::endl;

	std::vector<int> vec(5, 23);

	//static demonstration
	MyVector* ptr = new MyVector(10, 7);
	std::cout << MyVector::getCounter() << std::endl;

	delete ptr;
	std::cout << ptr->getCounter() << std::endl;
	
	//overload examples
	MyVector vo1(15, 10);
	MyVector vo2(10, 16);

	vo2 = vo1;

	std::cout << vo1 << "\n";
	std::cout << vo2 << "\n";
	vo2[5] = 7;
	//l value
	//func just return & so it doesn't check
	vo2.operator[](3) = 7;
	//if func return private field of the class 

	std::cout << vo2 << "\n";

	return 0;
}
```