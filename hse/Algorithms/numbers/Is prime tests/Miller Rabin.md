# Given a number *N*, check if it is prime or not.

- If true - probably prime, or if false - composite.
- a - k is an input parameter that determines accuracy level. Higher value of k indicates more accuracy.
```
For n to be prime, either
    a^d % n = 1 
         OR 
    a^(d*2i) % n = -1 
for some i, where 0 <= i <= r-1.
```

## Algorithm
1. Find *odd* m that `n - 1 = 2^r * d`
2. check if either `a^m (mod n) == 1  holds or a^(m*2^[0 - r]) (mod n) == -1 == n - 1`
3. if it doesn't hold -> n is composite
```C
int milllerPrime(int n, int k)
{
	if (n < 4)
		return n == 2 || n == 3;
	if (n % 2 == 0)
		return 0;


	int m = n - 1;
	int r = 0; // power
	int x = 0; //property
	int a = 0; //random number

	while ((m & 1) == 0)//find d like n - 1 = 2^r * d 
	{
		++r;
		m >>= 1;
	}
	
	while (k > 0)
	{
		milCycle(n, m) //check different K
		--k; // decrease k range
	}

	return 1; // as in Fermat theorems we checked all cases so they 
}

int milCycle(int n, int m)
{
	int a = rand() % (n - 3) + 2;

	int x = modExpRec(a, m, n);

	if (x == 1 || x == n - 1)  return 1;

	while (m < n - 1)
	{
		x = (x * x) % n;//we have mod property

		if (x == 1)  return 0;
		if (x == n - 1)  return 1; //this K says that n is probably prime

		m <<= 1;
	}
	return 0; //because we've already checked all d powers and found nothing
}

```
> **Time Complexity:** `O(k*logn)`

[source](https://www.geeksforgeeks.org/primality-test-set-3-miller-rabin/)
[[mod]] - property