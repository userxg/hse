# Linked list
idea: head and linked to it nodes
operations:
- push_head - `t(1)`
- pop_head - `t(1)`
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