# input/output and std

```CPP
using namespace std; // we use entire namespace

int main()
{
	int a = 0;
	std::cout << "Hello" << endl;
	std::cin >> a;
}

```
- `cout` - object of class iostream,  It is used to display the output to the standard output device i.e. monitor.
- `<<` overloaded insertion operator
- `>>` overloaded extraction operator (extract from stream)
- `endl` stream manipulator
## declaring dynamic array

```C++ 
using namespace std; // we use entire namespace

typedef struct something
{
	int x;
	int a[5];
}N;

int main()
{
	int n = 0;
	N k = { 10 };
	N* arr = new N({ 7, {1 , 2, 3, 4, 5} });
	int* var = new int(123);
	N** nEw = new N * [8];
	//N** nEw = (N**)malloc(8 * sizeof(N*));

	mal[0] = &k;
	nEw[0] = &k;

	delete[] nEw;
	delete[] arr;
	return 0;
}
```