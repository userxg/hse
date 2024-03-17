## Mechanics
#### Factorial example
1. Separate into we can and can't
		> we can multiply 
1. Find base problem and return result upward
		> when argument will be 0 return 1

```C
int fact(int x)
{
	if (x == 0) // base statment
		return 1;
	else
		return x * fact(x - 1); // action what we can
}
```

When we go deep *stack*  spins out and then spin in.
```C
f(3) -> f(2) -> f(1) -> f(0) //spin out

f(0) returen 1 => 
//spin in
1*f(1) = 1 * 1 = 1
1 * f(2) = 1 * 2 = 2
2 * f(3) = 2 * 3 = 6
```


## fibonacci
each pair of rabbits starts to [[bear]] new pair after 2 month of existing because they must become adults
1 - pair 1-st  | 0 month  |  1 thing
1 1st->1ST 1   |  1-st grew up  |  2 second       
2 1ST -> 2st 2    |   1- st bore 2-st | 3-rd
3 1ST -> 3st, 2ST 3    1st bore 3-st and 2ST has just grown up   4
5 1ST- > 4st, 2ST -> 5st, 3ST   5
8 1ST-> 6st, 2ST->7st, 3ST->8st, 4ST, 5ST
.....
or its just a sequence where 1-st + 2-nd -> 3-rd and so on
0 1 1 2 3 5 8 13
0 1 2 3 4 5 6  7
1. we can add f(n-1) + f(n-2)
2. stop when x == 1 || x == 2 because 1-st and 2-nd numbers of the sequence it's 1

```C
int fib(int x)
{
	if (x < 1)
		return 0;
	if (x == 1 || x == 2)
		return 1;
	else
		return fib(x - 1) + fib(x - 2);
}
```
But it isn't effective

## power 

1. We can multiply
2. We know N^0 = 1

```C
int power(int a, int b)
{
	if (b == 0)
		return 1;
	else
		return a * power(a, b - 1);
}
```

When we go deep *stack*  spins out and then spin in.
```C
f(3, 2) -> f(3 , 1) -> f(3, 0) -> 1 //spin out
1 -> 1 * 3 -> 3 * 3 -> 9  //spin in
```