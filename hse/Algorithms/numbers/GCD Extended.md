## **Extended Euclidean Algorithm:**
> *Extended Euclidean algorithm also finds integer coefficients x and y such that: ax + by = gcd(a, b)*

- plain GCD
```C
int gcd(int a, int b)
{
	if (a == 0)
		 return b;
	return (b%a, a);
}
```
we can upgrade it

**Examples:**  
> **Input:** a = 30, b = 20  
> **Output:** gcd = 10, x = 1, y = -1  
> (Note that 30*1 + 20*(-1) = 10)
> 
> **Input:** a = 35, b = 15  
> **Output:** gcd = 5, x = 1, y = -2  
> (Note that 35*1 + 15*(-2) = 5)

```C
int gcdExt(int a, int b, int* x, int* x)
{
//base case because a*x + b*y = d -> a*0 + b*1 = d;
	if (a == 0)
	{
		*x = 0;
		*y = 1;
		return b;
	}
	int x1 = 0, y1 = 0;
	gcd = gcdExt(b%a, a, &x1, &y1);

	*x = y1 - (b/a)*x1;
	*y = x1;
	return gcd; // sneaking gcd
}
```

>compare 1-st and 2-nd step
>ax + by = d
>a1x1 + b1y1 = d
>*we know b%a = b - (b/a)a*
>*in our function a1 = (b%a) and b1 = a*
>=> we get a system
>ax + by = d
>(b - (b/a)a)x1 + ay1 = d
>transform system and we get
>x = y1 - (b/a)x1;
>y = x1;

**Time Complexity:** O(log N)