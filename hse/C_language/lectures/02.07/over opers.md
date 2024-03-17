- allow to use standard operations with our classes 
Overloaded operator - is function  у которой чётко определено имя

## rules
- operator + symbol
- as member of class or as external function
- ` ->, [], () = `  only as member of class
- We can't
	- `. .*  :: sizeof typedef  ? :`  we can't overload
	- создавать новые лексемы операторов (e.g `! ? . p`)
	- изменять арность (number of operands)
	- изменять приоритет
	- ассоциативность
	- менять смысл для встроенных типов

- if i get new obj -> return  obj
- if i change cur obj -> return obj&

- `=` we can use without [[prior]] overload
## stream overload
- `<<` can be overloaded only outside
```C++
std::ostream& operator<<(std::ostream& out, const Rational& obj)
{
	obj.overprint();
	return out;
}
```
## increment and decrement overload

they exist in two forms
*prefix* like other operations returns &
*postfix* - gets fiction *int* parameter(no name, can't pass) returns obj

```C++
Rational& Rational::operator++()
{
	//*this += 1;
	return (*this+=1);
}

Rational Rational::operator++(int)
{
	Rational copy = *this;
	(*this).operator++();
	return copy;
}
```


# full code

## rational.h
```C++
#pragma once
class Rational
{
public:
	Rational() : numer(0), denom(1) {}
	Rational(int , int);
	void print() const;
	void overprint() const;
//bynary
	Rational operator+(const Rational& right) const;
	Rational operator-(const Rational& right) const;
	Rational operator*(const Rational& right) const;
	Rational operator/(const Rational& right) const;
	
	//r + n
	Rational operator+(int n) const;
	//n  + r outside the class

	Rational& operator+=(const Rational& rigth);
	Rational& operator+=(const int& n);
//unary
	Rational& operator++(); //prefix
	Rational operator++(int);//postfix
	
	Rational& operator-();


private:
	int numer, denom;

private:
	int GCD(int, int) const;
	void reduce();
};

//outside class overload
Rational operator+(const int& n, const Rational& r);

std::ostream& operator<<(std::ostream& out, const Rational& obj);
std::istream& operator>>(std::istream& inp, Rational& obj);
```

## rational.cpp
```C++
#include <iostream>
#include <exception>
#include "rational.h"

Rational::Rational(int numer, int denom) : numer(numer)
{
	if (!denom)
		throw std::invalid_argument("wrong data");
	this->denom = denom;
}

void Rational::print() const
{
	std::cout << numer << "/" << denom << "\n";
}

void Rational::overprint() const
{
	std::cout << numer << "/" << denom;
}

Rational Rational::operator+(const Rational& right) const
{
	Rational result;
	result.numer = ((this->numer * right.denom) + (this->denom * right.numer));
	result.denom = (denom * right.denom);
	result.reduce();
	return result;
}

Rational Rational::operator-(const Rational& right) const
{
	Rational result;
	result.numer = ((this->numer * right.denom) - (this->denom * right.numer));
	result.denom = (denom * right.denom);
	result.reduce();
	return result;
}

Rational Rational::operator*(const Rational& right) const
{
	Rational result;
	result.numer = numer * right.numer;
	result.denom = denom * right.denom;
	result.reduce();
	return result;
}

Rational Rational::operator/(const Rational& right) const
{
	if (!right.numer) throw std::invalid_argument("Can't divide by zero\n");

	Rational result;
	result.numer = numer * right.denom;
	result.denom = denom * right.numer;
	result.reduce();
	return result;
}

Rational Rational::operator+(int n) const
{
	Rational res;
	res.numer = numer + denom * n;
	res.denom = denom;
	res.reduce();
	return res;
}

Rational& Rational::operator+=(const Rational& rigth) 
{
	*this = this->operator+(rigth);
	return *this;
}

Rational& Rational::operator+=(const int& n)
{
	*this = *this + n;
	return *this;
}

Rational& Rational::operator++()
{
	//*this += 1;
	return (*this+=1);
}

Rational Rational::operator++(int)
{
	Rational copy = *this;
	(*this).operator++();
	return copy;
}

Rational& Rational::operator-()
{
	this->numer = -numer;
	return *this;
}



Rational operator+(const int& n, const Rational& r)
{
	return r + n;
}

std::ostream& operator<<(std::ostream& out, const Rational& obj)
{
	obj.overprint();
	return out;
}

std::istream& operator>>(std::istream& inp, Rational& obj)
{
	int numer = 0, denom = 0;
	std::cin >> numer >> denom;
	Rational new_data(numer, denom);
	obj = new_data;
	return inp;
}

void Rational::reduce()
{
	int gcd = GCD(denom, numer);
	numer /= gcd;
	denom /= gcd;
}

int Rational::GCD(int a, int b) const
{
	if (a == 0)
		return b;
	return GCD((b%a), a);
}
```


## main.cpp

```C++
#include <iostream>
#include <exception>
#include "rational.h"

int main()
{

	Rational r1(4, 5);
	//r1.print();
	Rational r2(2, 5);

	Rational r3 = r1 + r2;
	r3 = r1 + r2; //works assignment
	r3 = r1.operator+(r2);
	(r1 + r2).print();
	(r1 - r2).print();
	(r1 * r2).print();
	(r1 / r2).print();

	Rational r4 = { 0, 5 };
	try
	{
		(r1 / r4).print();
	}
	catch (std::invalid_argument ex)
	{
		std::cout << ex.what();
	}
	

	Rational r5(1, 5);
	Rational r6;
	r6 = r5 + 2; // 1/5  + 10/5 = 11/5
	r6.print();

	r6 += r5;//11/5 + 1/5
	r6.print();

	r6 = 2 + r6; //12/5 + 2 = 22/5
	std::cout << r6 << "\n" <<  r1 << "\n";


	std::cout << "something: " << (r6 += 1) << "\n";//27/5
	std::cout << r6++ << "\n";//returns copy and then put it into << function as &


	Rational r7; // test cin;
	std::cin >> r7;
	std::cout << r7 << "\n";
//ask about it
	std::cout <<  -(-(-r7)) << "\n";
	return 0;
}
```