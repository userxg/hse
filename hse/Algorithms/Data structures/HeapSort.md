idea: 
- Build Heap using n/2 leaf property (because `[n/2-n]` is the lowest row the are trivial BHs)
- Unload values from heap to array, decreasing size

## complexity
`O(nLogN)`

## implementations
- Build
```cpp
void BuildHeap(int* arr, int size)
{
	m_Size = size;
	for (int i = size / 2 - 1; i > 0; --i)
		MaxHeapify(arr, i);
}
```

- Sort
```cpp
void HeapSort(int* arr, int size)
{
	BuildHeap(arr, size);
	for (int i = size - 1; i > 0; --i)
	{
		Swap(arr[0], arr[i]);
		--m_Size;
		MaxHeapify(arr, 0);
	}
}
```
MaxHeapify - just a SiftDown in [[Heap(max)]]
