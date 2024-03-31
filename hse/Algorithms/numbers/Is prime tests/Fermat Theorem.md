# Check *N* is prime or not

## Little Fermat's theorem
[**Fermat's Little Theorem:**](https://www.geeksforgeeks.org/fermats-little-theorem/)
If n is a prime number, then for every a, 1 < a < n-1,

**a^(n-1) ? 1 (mod n)**
 **OR** 
**a^(n-1)** % n = 1

### While rand implementation ([[ModExp Recur]])
```C
int isPrime(int n, int k)
{
	if (k > n - 1)
		return -1;
	
	int c = 0;
	while (k > 0)
	{
		c = rand() % k + 1;
		if (modExpRec(c, n - 1, n) != 1)
			return 0;
		--k;
	}
	return 1;
}
```

>**Time Complexity:** O(log m)

