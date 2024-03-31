# Linked list
idea: 
- There are chain of Nodes
- Head ptr points to first Node (Can be Tail as well)
Operations:
- ListSearch(int key) - `O(n)`
- ListPrepend - `t(1)`
- ListDelete - `t(1)`
# Cormen + cpp
## representation of Double linked list
in Node we have **key**  and pointers **prev** and **next**
```cpp
struct Node
{
	int key;
	Node* next;
	Node* prev;
};
```

- List by themself
```cpp
class List
{
	struct Node
	{
		int key;
		Node* next;
		Node* prev;
	};

public:
	List() : l_head(nullptr) {}
private:
	Node *l_head;
};
```

## Operations
- ListSearch(key) - O(n), returns Node
```cpp
Node* ListSearch(int key)
{
	Node* X = head;
	while (X!=nullptr && X->key != key)
	{
		X = X->next;
	}
	return X;
}
```

- ListPrepend(key) - O(1) - insert given node before head.
```cpp
void ListPrepend(Node* X)
{
	X->prev = NULL;
	X->next = l_head;

	if (l_head != NULL)
		l_head->prev = X;

	l_head = X;
}
```
- List-Insert - `O(1)`  insert given Node X right after Node Y from List.
```cpp
void ListInsert(Node * X, Node * Y)
{
	X->next = Y->next;  //link X to Y.next
	X->prev = Y;   //link X to Y
	if (Y->next != NULL) //link Y.next to X
		Y->next->prev = X;
	Y->next = X;  //link Y to X
}
```
- List-Delete `O(1)`  delete given X from List
```cpp
void ListDelet(Node* X)
{
	if (X->prev != NULL)
		X->prev->next = X->next;
	else l_head = X->next;
	if (X->next != NULL)
		X->next->prev = X->prev;
}
```

## Circular Doubly Linked List
```cpp
struct Node
{
	Node(int key, Node* next, Node* prev) :
		key(key), next(next), prev(prev) {}
	int key;
	Node* next;
	Node* prev;
};

class CircularList
{
private:
	
	Node* sentinel_;

public:
	
	Node* setSentinel() { return sentinel_; }
	CircularList()
	{
		sentinel_ = new Node(0, NULL, NULL);
		sentinel_->next = sentinel_;
		sentinel_->prev = sentinel_;
	}

	void CircInsert(Node* x, Node* y)
	{
		x->prev = y;
		x->next = y->next;
		y->next->prev = x;
		y->next = x;
	}

	Node* CircSearch(int key)
	{
		sentinel_->key = key;
		Node* x = sentinel_->next;
		while (x->key != key)
			x = x->next;
		if (x == sentinel_)
			return NULL;
		return x;
	}

	void CircDelete(Node* x)
	{
		x->prev = x->prev->next;
		x->next->prev = x->prev;
	}

};
int main()
{
	CircularList list;

	Node* y = new Node(10, NULL, NULL );
	Node* x = new Node(11, NULL, NULL );
	list.CircInsert(y, list.setSentinel());
	list.CircInsert(x, y);

	return 0;
}
```
# struct realization
### Creating 
```C++

typedef struct linked_list_node
{
	int val;
	struct linked_list_node * next;
}node;

typedef struct linked_list//because we can create tail
{
	node* head;
}list;


void new_n(list* l)
{
	l->head = nullptr;
}
```
### insertions
```C++
void insert_head(list* l, int val)
{
	node* former_head = l->head;
	l->head = new node();
	l->head->next = former_head;
	l->head->val = val;
}

void insert_tail(list* l, int val)
{
	node* tail = get_tail(l)
	tail->next = new node();
	tail->next->val = val;
	tail->next->next = nullptr;
}
```

### get values
```C++
node* get_tail(list* l)
{
	node* tail = l->head;
	while (tail && tail->next) // check if tail exists
		tail = tail->next;
	return tail;
}

node* get_node_val(list* l, int val)
{
	node* find = l->head;

	while(find && find->next)
	{
		if (find->val == val)
			return find;
		find = find->next;
	}
	return nullptr;
}
```

## delete
```C++
void delete(list* l)
{
	node* del = head;
	while (del)
	{
		node* cur = del;
		del = del->next;
		delete cur;
	}
}
```

# Class realization
## double linked stack
```C++
class List
{
public:
	List() : head(nullptr), tail(nullptr) {};

	void PushHead(int val)
	{
		Node* old_node = head;
		head = new Node(val);
		if (old_node)
			old_node->prev = head;
		else
			tail = head;
		head->next = old_node;
		head->prev = nullptr;
	}


	void PushTail(int val)
	{
		Node* old_node = tail;
		tail = new Node(val);
		if (old_node)
			old_node->next = tail;
		else
			head = tail;
		tail->prev = old_node;
		tail->next = nullptr;
	}

	bool isEmpty() { return !head; }

	void PopHead()
	{
		if (!isEmpty())
		{
			Node* del = head;
			head = head->next;
			if (head)
				head->prev = nullptr;
			delete del;
		}
		else
			cout << "Throw exception";
	}

	void PopTail()
	{
		if (!isEmpty())
		{
			Node* del = tail;
			tail = tail->prev;
			if (tail)
				tail->next = nullptr;
			delete tail;
		}
		else
			cout << "is empty\n";
	}

	void print_full() const
	{
		Node* print = head;
		while (print)
		{
			cout << print->val << " ";
			print = print->next;
		}
	}
	
	int Head_val() const { return head->val; }
	

private:
	struct Node
	{
		Node(int val) : val(val) {}
		Node* next, * prev;
		int val;
	};
	Node* head;
	Node* tail;

public:
	~List()
	{
		Node* del = head;
		while (del)
		{
			Node* cur = del;
			del = del->next;
			delete cur;
		}
	}
};


class Stack {
public:
	Stack() : list() {}
	void Push(int val) { list.PushHead(val); }
	void Pop() { list.PopHead(); }
	int Top() const { return list.Head_val(); }	
	void print_stack() const{ list.print_full(); }
private:
	List list;
};
```