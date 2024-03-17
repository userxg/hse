- The adjacency-list representation of a graph consists of an array Adj of V  lists, one for each vertex in V . For each u, the adjacency list contains all the vertices v such that there is an edge (u, v) . 
```c++
class List
{
private:
	struct Node
	{
		Node(int data) : data(data), next(nullptr) {}
		int data;
		Node* next;
	};
	
	Node* head;

public:
	List() : head(nullptr) {}

	void pushHead(int data)
	{
		Node* old_head = head;
		head = new Node(data);
		head->next = old_head;
	}

	void popHead()
	{
		if (Empty()) 
		{
			std::cout << "empty\n";
			return;
		}
		Node* new_head = head->next;
		delete head;
		head = new_head;
	}

	bool Empty() { return head == nullptr; }

	void print() const
	{
		Node* tail = head;
		while (tail)
		{
			std::cout << tail->data << "->";
			tail = tail->next;
		}
		std::cout << "/";
	}
};

class simpleGraph
{
private:
	std::vector<std::vector<int>> adList;
	std::vector<std::vector<bool>> adMatrix;
	int vertex;
	int edges;

public:
	simpleGraph(int n) : vertex(n), edges(0), adList(n), adMatrix(n, std::vector<bool>(n, false)) {}

	void add_undir_edge(int from, int to)
	{
		adList[from].push_back(to);
		adList[to].push_back(from);
		adMatrix[from][to] = true;
		adMatrix[to][from] = true;
	}

	void add_dir_edge(int from, int to)
	{
		adList[from].push_back(to);
		adMatrix[from][to] = true;
	}

	void print_adList() const
	{
		for (int i = 0; i < vertex; ++i)
		{
			std::cout << i << ": ";
			for (auto& vertice : adList[i])
				std::cout << vertice << "->";
			std::cout << "/" << "\n";
		}
	}


};


class CormenGraph
{
private:
	std::vector<List> adList;
	std::vector<std::vector<bool>> adMatrix;
	int vertex;
	int edges;

public:
	CormenGraph(int n) : vertex(n), edges(0), adList(n), adMatrix(n, std::vector<bool>(n, false)) {}

	void add_undir_edge(int from, int to)
	{
		adList[from].pushHead(to);
		adList[to].pushHead(from);
		adMatrix[from][to] = true;
		adMatrix[to][from] = true;
	}

	void add_dir_edge(int from, int to)
	{
		adList[from].pushHead(to);
		adMatrix[from][to] = true;
	}

	//print adList
	void print_adList() const
	{
		for (int i = 0; i < vertex; ++i)
		{
			std::cout << i << ": ";
			adList[i].print();
			std::cout << "\n";
		}
	}
	
};


int main()
{
	List l1;
	for (int i = 1; i < 5; ++i)
		l1.pushHead(i * i);

	l1.print();
	std::cout << "\n";

	for (int i = 1; i < 7; ++i)
		l1.popHead();

	std::cout << "\n";

	CormenGraph gdir(5);

	gdir.add_dir_edge(0, 1);
	gdir.add_dir_edge(0, 4);
	gdir.add_dir_edge(1, 4);
	gdir.add_dir_edge(1, 3);
	gdir.add_dir_edge(1, 2);
	gdir.add_dir_edge(2, 3);
	gdir.add_dir_edge(3, 4);

	gdir.print_adList();

	std::cout << "\n";

	CormenGraph gundir(5);

	gundir.add_undir_edge(0, 1);
	gundir.add_undir_edge(0, 4);
	gundir.add_undir_edge(1, 4);
	gundir.add_undir_edge(1, 3);
	gundir.add_undir_edge(1, 2);
	gundir.add_undir_edge(2, 3);
	gundir.add_undir_edge(3, 4);

	gundir.print_adList();


	std::cout << "\n\n";


	simpleGraph sgdir(5);

	sgdir.add_dir_edge(0, 1);
	sgdir.add_dir_edge(0, 4);
	sgdir.add_dir_edge(1, 4);
	sgdir.add_dir_edge(1, 3);
	sgdir.add_dir_edge(1, 2);
	sgdir.add_dir_edge(2, 3);
	sgdir.add_dir_edge(3, 4);

	sgdir.print_adList();

	std::cout << "\n";

	simpleGraph sgundir(5);

	sgundir.add_undir_edge(0, 1);
	sgundir.add_undir_edge(0, 4);
	sgundir.add_undir_edge(1, 4);
	sgundir.add_undir_edge(1, 3);
	sgundir.add_undir_edge(1, 2);
	sgundir.add_undir_edge(2, 3);
	sgundir.add_undir_edge(3, 4);

	sgundir.print_adList();

	return 0;
}
```