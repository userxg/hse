# Modular Exponentiation Recur approach
It's also based on multiplying properties of [mod] 
Our default [[power]]  function just multiplies results and before it multiplies,  we  can find modular to apply [[mod]] property.
So we return modular of multiplications modulars that made from base case 
```C
int ExpRec(int a, int b)
{
	if (b == 0)  return 1;
	if (b%2) return ExpRec(a,b/2) * Exp(a, b/2) * a;
	return ExpRec(a, b/2) * ExpRec(a, b/2);
}

int modExpRec(int a, int b, int p)
{
	if (a == 0 || a%p == 0)  return 0; //added small optimization
	if (b == 0) return 1%p; //base case 
	if (b == 1) return (a)%p; //base case 
	int tmp = modExpRec(a, b/2, p);

	long long int result = tmp * tmp;
	if (b%2) return (int)((result * a)%p);
	return (int) (result%p);
}
//also we can add convertation in possitive value if function return negative
//by addition p  ->  if func returned -7 and p = 10 we just return 3 below
//base case return possitive and others as well
int modExpRec(int a, int b, int p)
{
	if (a == 0 || a%p == 0)  return 0; //small optimization
	if (b == 0) return 1%p; //base case 
	if (b == 1) return (a + p)%p; //base case 
	int tmp = modExpRec(a, b/2, p);

	int result = tmp * tmp;
	if (b%2) return (result * a + p)%p
	return (result + p)%p;
}

//also we 

```

2. short way (we don't store big values)
```C
int power(int x, unsigned int y, unsigned int m)
{
    if (y == 0)
        return 1;
    int p = power(x, y / 2, m) % m;
    p = (p * p) % m;

    return (y % 2 == 0) ? p : (x * p) % m;
}
```

