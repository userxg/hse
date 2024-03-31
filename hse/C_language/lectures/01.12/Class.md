## short info 
- Like as a structure but consist of methods
- Data in class is called ***Fields***

```C++

class BankAccount
{
	//attributes
public: //we can access from main  account1.string
	string name;
	int balance;//member varialbes
	
//methods
	void withdraw(int amount)
	{
		balance = balance - amount;  // access and work with member variable
	}

	void print_bill()
	{
		cout << name << " has " << balance << " dollars " << '\n';
	}

private://hiden things we don't have acсess
	int some_variabe;
};

int main()
{
	BankAccount account1; //object - instance of class

	account1.name = "User";
	account1.balance = 3000;

	cout << account1.name << " has " << account1.balance << " dollars " << '\n';

	BankAccount account2;
	account2.name = "White user";
	account2.balance = 1000;

	cout << account2.name << " has " << account2.balance << " dollars " << '\n';
	account2.balance = account2.balance - 100; //we can replace it with method
	cout << account2.name << " has " << account2.balance << " dollars " << '\n';

	account2.withdraw(700); //created withdrow method
	cout << account2.name << " has " << account2.balance << " dollars " << '\n';

	account1.withdraw(300);
	account1.print_bill();

	Rational r1;
	return 0;
}

```

- Each class has special function that's called ***CONSTRUCTUR***  - [[Constructor]]

## encapsulation - hide data 
- ***Private and Public*** - are access specifiers  (Private as a default).
- we can make sure is variable truth
```C++
class Employee
{
public:
	string name;

	void set_salary(double potetional_salary)
	{
		//we can make sure is variable truth
		if (potetional_salary < 0)  salary = 0;
		else salary = potetional_salary;
	}

	double get_salary()
	{
		return salary;
	}

	void print_bonus()
	{
		cout << "Bonus: " << calculate_bonus() << endl;
	}
//it's encapsulation
private:// 
	double salary;
	
	double calculate_bonus()
	{
		return salary * 0.10;
	}
};

```
- it's common to see getter and setter functions for private variables, they responsible for managing access to that data

## Class member function
### we can declare our function outside of class if it's public
### and in our declared functions we can use privates
```C++
class Rectangle
{
private:
	int width;
	int length;

	double area()
	{
		return length * width;
	}
public:
	void set_dimensions(int l = 10, int w = 5)
	{
		length = l;
		width = w;
	}

	double perimeter();
	void print_area();
};

double Rectangle::perimeter()//declaring funtion outside of class
{
	return 2 * (length + width);
}

void Rectangle::print_area() //in this function we use private function
{
	cout << "Area: " << area() << '\n';
}
```

## Value as a default in set function 
```C++
class AboutSet
{
private:
	int value1, value2;

public:
	void setValues(int x, int y = 5)//if we call this function and don't set y, y will be 5
	{
		value1 = x;
		value2 = y;
	}

	void print_vs();
};

void AboutSet::print_vs()
{
	cout << "Value1: " << value1;
	cout << "Value2: " << value2;
}

int main()
{

	AboutSet inst1;
	int1.print_vs();
	inst1.setValues(3);
	inst1.print_vs();  
	return 0;
}
```

output:
```BASH
Value1: -858993460   #garbage
Value2: -858993460   #garbage
Value1: 3
Value2: 5
```
