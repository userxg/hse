# Principles

- Queue is a linear data structure which follows FIFO method
- Data/element is stored first in the queue will be accessed first
- The ends of a queue are called (Head)*Front* and *Rear*.
- Insertion takes place at the Rear(Tail)
- Access and remove from the Front
### operations
- enqueue - insertion `t(1)`
- dequeue - remove `t(1)`
- showqueue - show front `t(1)`
- isEmpty `t(1)`
# Implementation
## Using Array (cycle queue)
```C
class Queue
{
private:
	int size; //amount
	int head; // index
	int tail;
	int* arr;
	int el_counter;
public:
	Queue(int size) : size(size)
	{
		arr = new int[size];
	}
	
	bool Full() { return el_counter == size; }
	bool Empty() { return el_counter == 0; }

	void Enqueue(int x)
	{
		if (Full()) return;
		arr[tail] = x;
		tail = (tail + 1) % size;
	}
	
	int Dequeue()
	{
		if (Empty()) return; //error;

		int x = arr[head];
		head = (head + 1) % size;
		el_counter--;
	}
};
```

