# Find primes
1. Fill an array with number 1 - n
2. Starting with **second entry** in the array, set all its multiples to zero
3. Proceed to the next non-zero element and set all its multiples to zero
	1. Because 2 fist strikes off 2^2, 3 strikes off 3^2, 5 first time strikes off 5^2, we can start our loop second loop from `a[i]^2`, (mean if `a[i]` = 3 we check 9 at once)
4. Repeat steps

## First implementation
```C
void fill_seive(int* a, int n)
{
    for (int i = 0; i < n; ++i) // fill array
        a[i] = i + 1;
    for (int i = 1; i < srqt(n); ++i) // start function (sqrt optimizes)
    {
        if (a[i] != 0)
        {
            for (int j = a[i] * a[i]; j < n; j += a[i])
            {
                a[j - 1] = 0;
            }
        }
    }     
}
```
We can use [[sqrt]] to optimize it
> *Complexity*: `O(n*log log n)`