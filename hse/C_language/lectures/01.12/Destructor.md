## It's being called during destroying object
```C++
~ClassName()
{
}
```
- can be only one, overloading is impossible
## Use case - free memory
```C++
class Number
{
private:
	double *number;
public:

	Number(double num)
	{
		number = new double(num);
		//number = (double*)malloc(sizeof(double));
		//*number = num;

		cout << "Constructor executing!" << endl;
		cout << "Number: " << *number << "\n\n";
	}

	~Number()
	{
		cout << "Destructor executing!" << endl;
		cout << "Number: " << *number << "\n\n";
		//free(number);
		delete number;

	}
};

void test()
{
	Number six(6);
}
int main()
{
	Number* five = new Number(5);
	delete five;

	Number n1(7);

	test();

	return 0;
}
```

- Object is being destroyed in revers order defining variables