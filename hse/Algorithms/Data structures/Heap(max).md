# priority queue

idea: parent has k children they less/more than parent
parent = (child - 1) / 2
left = parent* 2 + 1
right = parent* 2 + 2
## complexity
1. *Insert* `O(logN)` 
	- N - high of tree, base how many branches we have
	- Swap - `O(1)`
	- SiftUp - `O(lonN)`
2. *Extract *- `O(logN)` 
	- N - high of tree, base how many branches we have
	- Swap - `O(1)`
	- SiftDown - `O(lonN)`
3. Get Max/Min - `O(1)`


## Cormen's version (maxHeap)

```cpp
class HeapMax
{
private:
	int* heap;
	int m_Size;

public:

	int Parent(int i) { return (i - 1)/2; }
	int Left(int i) { return i * 2 + 1; }
	int Right(int i) { return i * 2 + 2; }

	void BuildHeap(int* arr, int size)
	{
		m_Size = size;
		for (int i = size / 2 - 1; i > 0; --i)
			MaxHeapify(arr, i);
	}
	
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

	void MaxHeapify(int* arr, int i)
	{
		int l = Left(i);
		int r = Right(i);
		int largest = i;
		if (l < m_Size && heap[l] > heap[largest])
			largest = l;
		if (r < m_Size && heap[r] > heap[largest])
			largest = r;
		if (largest != i)
		{
			Swap(heap[i], heap[largest]);
			MaxHeapify(arr, largest);
		}
	}

	HeapMax(int size) : m_Size(size)
	{
		heap = new int[size];
	}


	void Swap(int& x, int& y)
	{
		int temp = x;
		x = y;
		y = temp;
	}
};
```

```C++
#include <iostream>
#include <vector>
#include <string>
typedef unsigned long int INT;
class Heap
{
private:
	std::vector<INT> heap_;
	int size_;
public:
	Heap(int limit) : size_()
	{
		heap_.resize(limit);
	}

	void insert(INT elem)
	{
		heap_[size_] = elem;
		SiftUp(size_);
		size_++;
	}

	INT Max()
	{
		if (!Empty())
			return heap_[0];
		std::cout << "exception\n";
	}

	INT get_Max()
	{
		if (Empty()) { return -1; }
		INT max = Max();
		size_--;
		Swap(heap_[0], heap_[size_]);
		SiftDown(0);
		return max;
	}



	void print() const
	{
		for (int i = 0; i < size_; ++i)
			std::cout << heap_[size_] << " ";
		std::cout << std::endl;
	}

private:
	void SiftUp(int child)
	{
		if (child == 0) return;
		int parent = (child - 1) / 2;

		if (heap_[child] > heap_[parent])
		{
			Swap(heap_[child], heap_[parent]);
			SiftUp(parent);
		}
	}

	void SiftDown(int parent)
	{
		int child_1 = parent * 2 + 1;
		int child_2 = parent * 2 + 2;
		int lowest = parent;
		//find the smalest one
		if (child_1 < size_ && heap_[child_1] < heap_[lowest])
			lowest = child_1;
		if (child_2 < size_ && heap_[child_2] < heap_[lowest])
			lowest = child_2;
		if (parent != lowest)
		{
			Swap(heap_[lowest], heap_[parent]);
			SiftDown(lowest);
		}
	};

	bool Empty() { return size_ == 0; }


	void Swap(INT& a, INT& b)
	{
		INT tmp = a;
		a = b;
		b = tmp;
	}
};

int main()
{
	int size = 0, value = 0;
	std::cin >> size;
	Heap heap(size);
	std::string cmd = "";

	for (int i = 0; i < size; ++i)
	{
		std::cin >> cmd;

		if (cmd == "Insert")
		{
			std::cin >> value;
			heap.insert(value);
		}
		if (cmd == "ExtractMax")
		{
			std::cout << heap.get_Max() << std::endl;
		}
	}
	
	return 0;
}
```

