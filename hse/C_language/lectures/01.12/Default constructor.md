# We need to set up default variables

```C++
class ClassName{
public:
	ClassName()
	{
		first = "some value of any type";
		second = 3;
	}
}

int main()
{
	ClassName cl1; //Now in cl1 we have data in two fields
}

```

2. When we create another constructor with parameters, our default don't calls

```C++
class ClassName{
public:
	ClassName()
	{
		first = "some value of any type";
		second = 3;
	}
	ClassName(type s)
	{
		second = s;
	}
}
```

4. We can initialize in two ways our object

```c++
int main()
{
	ClassName cl1; //Now in cl1 we have data in two fields
	///same thing
	ClassName c12 = {4};
	ClassName cl3(5);  
}
```

5. We can create and definition outside and use default values
## Example

```C++
class Cat
{
private:
	string name;
	string color;
	string favorite_toy;

public:
	void print_cat()
	{
		cout << "Name: " << name << endl;
		cout << "Color: " << color << endl;
		cout << "Favourite Toy: " << favorite_toy << endl;
	}

	Cat()
	{
		name = "Unknown";
		color = "Unknown";
		favorite_toy = "Unknown";
	}
	Cat(string n)
	{
		name = n;
		color = "No color";
	}
	/// OUTSIDE 
	Cat(string n, string c, string t = "Laser Pointer");
};

Cat::Cat(string n, string c, string t)
{
	name = n;
	color = c;
	favorite_toy = t;
}

int main()
{
	Cat cat1;


	cout << "Cat1..." << endl; 
	cat1.print_cat();

	Cat cat2 = { "Name" };
	// Cat cat2("Name");
	cout << "Cat2..." << endl;
	cat2.print_cat();

	Cat cat3("User", "White");

	cout << "Cat3..." << endl;
	cat3.print_cat();
	return 0;
}

```

_output_

```bash
Cat1...
Name: Unknown
Color: Unknown
Favourite Toy: Unknown
Cat2...
Name: Name
Color: No color
Favourite Toy:
Cat3...
Name: User
Color: White
Favourite Toy: Laser Pointer
```

- **_Function overload_** - two functions with the same name and different list of parameters (we can create them as many as you want)

- delete constructor
```C++
Log() = delete;
```