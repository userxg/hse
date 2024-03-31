- int, double... - has constructors -> they're classes
- constructor returns an object
```C++
class Rational
{
public:				//field constructor -> int, double - classes
	Rational() : numer(0), denom(1) {} //put values instead garbage(works faster)
	Rational(int n, int d); //нет типа по умолчанию
	void print()const; //обязуется не менять поля объекта, если функция не меняет она должна быть константна

private:
	int numer, denom;
};
```
- there're fields of class, that you can initialize only through init list:
	- const fields
	- references - fields of class in which's type default constructor undefined

Initialize class
```c++
class Major
{
public:
	std::string name;

	Major() : name("Undeclared") 
	{
		std::cout << "Undeclared" << "\n";
	}

	Major(std::string name) : name(name) 
	{
		std::cout << "Declared with name";
	}

	Major(const Major& ref) : name(ref.name)
	{
		std::cout << "Copy constructor" << "\n";
	}


};

class Student
{
public:

	Major major;                   //why there is no copy copy constr calls
	Student(std::string major) : major(Major(major)) {}

	void print() const 
	{
		std::cout << major.name << "\n";
	}
};


int main()
{
	Student s1("Math");
	return 0;
}
```