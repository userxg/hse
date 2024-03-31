# merge sort 
1. Divide array into small pieces
	1. find mid
	2. call two function before mid and after
2. sort each piece
	1. It will be automatically, if we divide into piece 1 elem
3. merge them
	1. find length of each part
	2. fill new arrays
	3. merge this arrays, by replacing elems in original array

```C
void merge_sort(int* a, int n)
{
	merge_sort_recursion(a, 0, n - 1);
}

void merge_sort_recursion(int* a, int low, int high)
{
	if (low < high)
	{
		int mid = (low + high) / 2;
		merge_sort_recursion(a, low, mid);
		merge_sort_recursion(a, mid + 1, high);
		merge_sorted(a, low, mid, high);
	}
}

void merge_sorted(int* a, int low, int mid, int high)
{
	int length_right = mid - low + 1;
	int length_left = high - mid;

	int* right_part = (int*)calloc(length_right, sizeof(int));
	int* left_part = (int*)calloc(length_left, sizeof(int));

	for (int i = 0; i < length_right; ++i)
		right_part[i] = a[low + i];
	for (int i = 0; i < length_left; ++i)
		left_part[i] = a[(mid + 1) + i];

	int pointL = 0, pointR = 0, start = low;
	for (; start <= high; ++start)
	{
		if ((pointL < length_left) && (pointR >= length_right
			|| left_part[pointL] <= right_part[pointR]))
			a[start] = left_part[pointL++];
		else
			a[start] = right_part[pointR++];
	}
}
```
>*Complexity:* **log(n)n**
