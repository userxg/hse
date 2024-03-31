## Lowest Common Multiple
```C
int lcm(int a, int b){ return a*b/gcd(a,b);}
```
Let d = gcd(a ,b)  -> a = d x q1,  b = d x q2 -> (a x b)/d = d x q1 x q2 = k
because if d is maximum q1 and q2 are minimum

## Greatest Common Divisor
1. For implementation
```C
int gcd(int a, int b)
{
	gcd = 1;
	for (int i = 1; i <= a && i <= b; ++i)
	{
		if (a%i == 0 && b%i == 0)
			gcd = i;
	}
	return i;
}
```
2. While implementation
```C
int gcd(int n1, int n2)
{
	while (n1 != n2)
	{
		if (n1 > n2)
			n1 -= n2;
		else
			n2 -= n1;
	}
	return n1;
}
```
> *ex* gcd(12, 8) -> 12  8 -> 4  8 -> 4  4 -> return 4

3. Recursive By Euclidean Algorithm (there is - [[GCD Extended]])
	1. like while algorithm but recursive
```C
int gcd(int a, int b)
{
	//Everything divides 0
	if (a == 0)
		return b;
	if (b == 0)
		return a;

	//base case
	if (a == b)
		return a;

	if (a > b)
		return gcd(a - b, a)
	return gcd(a, b - a)
}
```
	can be linear complexity gcd(x, 1)

or by division
```C
int gcd(int a, int b)
{
	if (b == 0)
		return a; // 6 = 0 (mod 3) 
	return gcd(b, a%b);
}
```
	complexity is O(log (min(a,b)))


