1. Find middle
2. Compare mid and target
3. Cut range
```C
int bynary_search(int* a, int target, int n)
{
	int low = 0, high = n - 1, mid = 0;
	while (low <= high)
	{
		mid = (low + high) / 2; // found middle
		if (a[mid] == target)
			return mid;
		else if (a[mid] < target)
			low = mid + 1;  // cut low
		else
			high = mid - 1; // cut high
	}
	return -1;
}
```
> *complexity:* **log(n)**

