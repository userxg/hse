# Principles

- Queue is a linear data structure which follows FIFO method
- Data/element is stored first in the queue will be accessed first
- The ends of a queue are called *Front* and *Rear*.
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
using namespace std;
#define N 10

typedef struct queue
{
	int A[N];
	int max_size;
	int el_count;
	int front;
	int rear;
}QUEUE;

bool isEmpty(QUEUE* q)
{
	return q->el_count == 0;
}

bool isFull(QUEUE* q)
{
	return q->el_count == q->max_size;
}

void enqueue(QUEUE* q, int val)
{
	if (isFull(q))
	{
		cout << "is FULL\n";
		return;
	}

	q->A[q->rear] = val;
	q->rear = (q->rear + 1) % q->max_size;
	q->el_count++;
}
```

