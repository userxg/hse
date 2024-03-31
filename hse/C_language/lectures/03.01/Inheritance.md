- definition - вариант повторного использование кода, при котором new classes are being creating using other classes, плотная связь, получается иерархия
- Arrows are from *Base* to *Derived* classes - derived class knows that he has Base, but base knows nothing

##  access specifiers
- private is  inherited, but derived don't have access
- protected - available to all childes  
- final - without childes
## inheritance types
- public - наследование интерфейса, public part of base class
- private - наследование реализации, без интерфейса (stack and vector example), developer has, but user don't have access 
- protected 

- Is not inherited
	- constructors
	- destructors
	- assign operator `=`
	- friends

- Срезка
```C++

Point* ptr1 = &c1;
Point* ptr2 = &c2;
Point& ref3 = c2;

std::cout << (*ptr1 == *ptr2) << "\n";

std::cout << sizeof(c1) << "\n";
std::cout << sizeof((Point)c1) << "\n";
std::cout << sizeof(ref3) << "\n";
```