# Iterative Modular Exponentiation

1. For small numbers
```C
int modExpIter(int a, int b, int p)
{
	int res = 1;// This thing store all our odd steps
	while (b > 0)
	{
		if (b % 2 == 1)
			res = res * a;
		
		a = (a * a); //we've already multiplied this in ^2 so we need to 
		b = b >> 1;  // decrease ->  b =/ 2
	}
}
```
>_Time Complexity:_ O(log2 a), where *a* represents the value of the given input.

2. For big numbers we can use special type of a (int_128) or do the following

```C
int modulExpIter(int a, int b, int p)
{
    int result = 1;
    
    a = a % p; 
    
    if (a == 0)  return 0; // a divisible by p;

    while (b > 0)
    {
        if (b & 1)  // if b & 1 == 1 or if b & 00001 == 1 (conjuntion)
            result = (result*a) % p; 
            
		a = (a * a) % p;
        b = b >> 1;
    }
    return result;
}
```
Why (is it so - this [video]) and [mod] 
Recursive way - [[ModExp Recur]]


