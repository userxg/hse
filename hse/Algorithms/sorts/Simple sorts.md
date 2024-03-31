# Selection sorting
1. take all array and find minimum or max
2. swap with 1-st 
3. take all array after 1-st and do 1 and 2 step
4. do 3 until length of array
```C
void select_sort(int* a, int n)
{
	for (int i = 0; i < n - 1; ++i)
	{
		int index = i;
		for (int j = i + 1; j < n; ++j)
		{
			if (a[j] < a[index])
				index = j;
		}
		swap(&a[i], &a[index]);
	}
}
```
> *swap - [[xor swap]]*
> *Complexity:  **O(N^2)***


# Bubble sorting
## 1-st implementation
```C
void BubbleSort(int* arr, int n)
{
	bool didSwap = true;
	while (didSwap)
	{
		didSwap = false;
		for (int i = 0; i < n - 1; ++i)
		{
			if (arr[i] > arr[i + 1])
			{
				std::swap(arr[i], arr[i + 1]);
				didSwap = true;
			}
		}
	}
}
```

## 2-st implementation
```C
void bubble_sort2(int* a, int n)
{
	for (int i = 0; i < n - 1; ++i)
	{
		int swaped = 0;
		for (int j = 0 ; j < n - 1; ++j)
		{
			if (a[j] > a[j + 1])
			{
				swap(&a[j], &a[j + 1]);
				swaped = 1;
			}
		}
		if (!swaped)
			break;// best case
	}
}

```

> *Complexity:* O(N^2)
> *Best case*: O(N)


# Insertion sorting
1. Think that 1-st elem is sorted
2. move array
```C
void insert_sort(int* a, int n)
{
	for (int i = 1; i < n; ++i)// from 2-nd elem because 1-st is sorted
	{
		int index = i - 1;
		int key = a[i]; //our elem
		while (index >= 0 && a[index] > key)
		{
			a[index + 1] = a[index]; //move array 
			--index;
		}
		a[index + 1] = key;
	}
}
```

> *Complexity:* O(N^2)
> *Best case*: O(N)