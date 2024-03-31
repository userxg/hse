```C++
	void dfs(int at)
	{
		if (visited[at]) return;
		visited[at] = true;

		std::cout << at << " ";
		std::vector<int> neighbours = list[at].second;
		for (int next : neighbours)
			dfs(next);
	}
```

- Cormen Version (Without parents and time)
```C++
class Dfs
{

	std::vector<char> color;
	int vertices;

public:
	Dfs(): vertices(0){}

	void Dfs_run(std::vector<std::vector<int>>& g)
	{
		vertices = g.size();;
		color.resize(vertices);

		//mark as white, means isn't discovered
		for (int u = 0; u < vertices; ++u)
			color[u] = 'w';

		for (int u = 0; u < vertices; ++u)
		{
			if (color[u] == 'w')
				Dfs_visit(g, u);
		}
	}


	void Dfs_visit(std::vector<std::vector<int>>& g, int u)
	{
		color[u] = 'g'; //mark as gray, means is on Dfs path now
		std::cout << u << "->";
		for (int& v : g[u])
		{
			if (color[v] == 'w')
				Dfs_visit(g, v);
		}

		color[u] = 'b'; //mark as black, means is completly discover
	}

};

int main()
{
	int vertices, edges;
	std::cin >> vertices;
	std::cin >> edges;

	std::vector<std::vector<int>> g(vertices);

	for (int i = 0; i < edges; ++i)
	{
		int from = 0, to = 0;
		std::cin >> from >> to;
		g[from].push_back(to);
		g[to].push_back(from);
	}


	std::cout << "\nGraph:\n";
	for (int u = 0; u < vertices; ++u)
	{
		std::cout << u << " - ";

		for (int& v : g[u])
			std::cout << v << " ";
		std::cout << "\n";
	}

	std::cout << "Dfs log:\n";
	Dfs dfs;
	dfs.Dfs_run(g);

	return 0;
}
```


- DFS TASK
```C++
#ifdef HORSE
class Dfs
{
	struct cell
	{
		int i, j;
	};
	std::vector<short> di;
	std::vector<short> dj;


	int vertices;
	std::vector<char> color;
	std::vector<int> path;
	std::vector<int> parent;
	std::vector<std::vector<int>> g;

	cell start;
	int S;

public:
	Dfs(int S) : vertices(S* S), S(S), g(vertices),
		start{ 0, 0 }, color(vertices, 'w'), path(vertices, 0), parent(vertices, 0),
		di{ -2, -2, -1, -1,  1, 1,  2, 2 },
		dj{ -1,  1, -2,  2, -2, 2, -1, 1 }
	{}

	void Dfs_work()
	{
		std::cin >> start.j >> start.i;

		make_graph();
		print_graph();

		if (Dfs_run())
			print_path();

		else 
			std::cout << "Hamiltonian path:\n" << "No way";
	}

private:

	bool Dfs_run()
	{

		//check only one vertice
		int start_vertice = start.i * S + start.j;
		parent[start_vertice] = start_vertice;
		path[start_vertice] = -1;
		return Dfs_visit(start_vertice);
	}

	bool Dfs_visit(int u)
	{
		color[u] = 'g';
		path[u] = path[parent[u]] + 1;

		bool stop = false;

		if (path[u] == (vertices - 1))
			return true;
		//visit list
		for (int& v : g[u])
		{
			if (color[v] == 'w')
			{
				parent[v] = u;
				stop = Dfs_visit(v);
				if (stop)
					return true;
			}
		}

		color[u] = 'w';
		//path[u] = 0;
		//parent[u] = -1;
		return false;
		//std::cout << u << "->";
	}

	void make_graph()
	{
		for (int i = 0; i < S; ++i)
		{
			for (int j = 0; j < S; ++j)
			{
				for (int k = 0; k < 8; ++k)
				{
					cell neighbour = { di[k] + i, dj[k] + j };
					if (neighbour.i >= S || neighbour.i < 0 || neighbour.j >= S || neighbour.j < 0)
						continue;

					g[i * S + j].push_back(neighbour.i * S + neighbour.j);
				}
			}
		}
	}

	void print_graph()
	{
		std::cout << "Graph:\n";
		for (int u = 0; u < vertices; ++u)
		{
			
			

			std::cout << u << " - ";
			for (int& v : g[u])
				std::cout << v << " ";
			std::cout << "\n";
			
			
		}
	}

	void print_path()
	{
		std::cout << "Hamiltonian path:\n";
		for (int i = 0; i < S; ++i)
		{
			for (int j = 0; j < S; ++j)
			{
				std::cout << path[i * S + j] << " ";
			}
			std::cout << "\n";
		}
	}
};



int main()
{
	int S;
	std::cin >> S;
	Dfs dfs(S);

	dfs.Dfs_work();

	return 0;
}
#endif // HORSE
```