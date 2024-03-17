## Each class has special function that's called ***CONSTRUCTUR*** 

Constructor has a part we can see and we can't one 
- Part that we can't see are allocating memory for object
-  Part we can - is setting up start values of fields
- It works during creating class
- It's being called during creating instance
## default constructor
- Default constructor has:
	- [[Default constructor]]
	- Copy constructor
	- move constructor
- It gets disappear when we create own constructor

## constructor has the same name that class has
1. Constructor must be declared in public (because of access properties)
2. Constructor without parameters, default constructer. It's enough to just create an object we create another constructor with parameters, our default don't calls
- ***Function overload*** - two functions with the same name and different list of parameters (we can create them as many as you want)
- Works in the same order what fields was written.