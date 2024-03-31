- Called in function the pass and return; not 
- `explicit` - forbid copy const -> we can't pass object in function
- All not special const are *Initialization constrs*
e.g.
```C++
explicit MyVector(const MyVector& ref);

int main()
{
	MyVector v1;
	//called copy consturtor because we have an obj
	MyVector v3(v1);
	MyVector v3 = v1;
	
	MyVector v3(10, 5); //explicit constructor call

	int a = 5;
	MyVector v3 = a; //implicit init by size constructor call
	MyVector v3(a);//explicit
}

explicit //only admits only explicit call 
```
- can be two constrs with *const* or not
- Each object and func has access to private part of another obj that is his type



## friendship
- main has access to data;
```C++

class Some
{
	friend int main();
private:
	int data;
};
```
- Class friends has access to the private of the class
- Friends - other classes, functions,
- Not symmetric, not transitive, you can friend who is not there



