idea: storing data as row

## complexity
1. Insert `O(N)` 
2. *Delete*- `O(N)`
3. Find - O(1)

```C
#define SIZE 4
void Insert(int* arr, int* size,  int val, int index)
{
	for (int i = *size - 1; i > index; --i)
	{
		arr[i] = arr[i - 1];
	}
	*size += 1;
}

void Delete(int* arr, int* size, int index)
{
	for (int i = index; i < *size - 1; ++i)
	{
		arr[i] = arr[i + 1];
	}
	*size -= 1;
}

int main()
{
	int size = 4;
	int arr[SIZE] = { 1 ,2 ,3 ,4 };

	Insert(arr, &size, 5, 0);

	return 0;
}
```