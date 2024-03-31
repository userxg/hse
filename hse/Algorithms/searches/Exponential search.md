1. Check first elem
2. Increase range of searching
3. apply [[binary]] search
```C
int exponential_search(int* a, int target, int n)
{
	if (a[0] == target)
		return 0;
	int bound = 1;
	while (bound < n && a[bound] < target)
		bound *= 2;
	return binary_search(a, target, bound/2, min(bound, n - 1));
}
```
> *Complexity*: **log(n)**

