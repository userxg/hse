idea:  - 

**complexity** 
time - `O(V + E)`
space - `t(V)` - store visited


## Breadth-first search
From Cormen 20.2
- class
```C++
class Bfs
{
private:
	struct Vertex
	{
		int vertice;
		int distance;
		char color;
		Vertex* predecessor;
	};

	int vertices;
	std::vector<Vertex> bfs_tree;
	std::queue<Vertex> q;

public:
	Bfs() : vertices(0), bfs_tree(0){}


	//takes O(V + E) linear time
	void bfs_travers(std::vector<std::pair<int, std::vector<int>>> g, int source)
	{
		vertices = g.size();
		bfs_tree.resize(vertices);

		setBfs_g(g);
		bfs_tree[source].color = 'g';
		bfs_tree[source].distance = 0;

		q.push(bfs_tree[source]);

		while (!q.empty())//travers each vertice  O(V)
		{
			Vertex u = q.front();
			q.pop();
			for (auto& neighbour : g[u.vertice].second)//sum of all lists E or 2E
			{
				if (bfs_tree[neighbour].color == 'w')
				{
					bfs_tree[neighbour].color = 'g';
					bfs_tree[neighbour].distance = u.distance + 1;
					bfs_tree[neighbour].predecessor = &bfs_tree[u.vertice];
					q.push(bfs_tree[neighbour]);
				}
			}
			bfs_tree[u.vertice].color = 'b';
		}
	}

	void print_path(int source, int vertice) const
	{
		if (print_path_recur(source, vertice))
			std::cout << "/";
		else
			std::cout << "no path exisits from \"" << source << "\" to \"" << vertice << "\" \n";
	}

	bool print_path_recur(int source, int vertice) const
	{

		if (vertice < vertices && bfs_tree[vertice].vertice == bfs_tree[source].vertice)
			std::cout << source << "->";
		else if (vertice >= vertices || bfs_tree[vertice].predecessor == nullptr)
			return false;
		else
		{
			print_path_recur(bfs_tree[source].vertice, bfs_tree[vertice].predecessor->vertice);
			std::cout << vertice << "->";
		}
		return true;
	}

private:
	void setBfs_g(std::vector<std::pair<int, std::vector<int>>> g)
	{
		for (int i = 0; i < vertices; ++i)
		{
			bfs_tree[i].vertice = i;

			bfs_tree[i].color = 'w';
			bfs_tree[i].distance = std::numeric_limits<int>::max();
			bfs_tree[i].predecessor = nullptr;
		}
	}
};
```


- main
```C++
int main()
{
	int n = 5;
	int from = 2, to = 4, weight = 10;

	////weghted_graph adList
	std::vector<std::vector<std::pair<int, int>>> w_gl(n);
	//vertice and weight
	w_gl[from].push_back({ to, weight });

	//weghted_graph adList
	std::vector<std::vector<int>> w_gm(n, std::vector<int>(n, 0));

	w_gm[from][to] = weight;

	

	int vertices = 0;
	int edges = 0;

	std::cin >> vertices >> edges;

	std::vector<std::pair<int, std::vector<int>>> g(vertices);


	for (int i = 0; i < edges; ++i)
	{
		int from = 0, to = 0;
		std::cin >> from >> to;
		g[from].first = from;
		g[from].second.push_back(to);
		g[to].second.push_back(from);
	}

	std::cout << "Graph:\n";
	for (int i = 0; i < vertices; ++i)
	{
		std::cout << g[i].first << " - ";
		for (int& v : g[i].second)
			std::cout << v << " ";
		std::cout << "\n";
	}


	Bfs bfs;
	bfs.bfs_travers(g, 0);

	int source = 0, vertice  = 0;
	std::cout << "check shortets path from source to vertice\n";
	std::cout << "source: ";
	std::cin >> source;
	std::cout << "vertice: ";
	std::cin >> vertice;
	std::cout << "path:\n";

	bfs.print_path(source, vertice);

	return 0;
}
```


>complexity: O(V + E) linear time

test
5
6
0 1
0 2
0 3
1 4
2 4
3 4


check shortest path
0 8 - no path
3 4 - 3->4
0 4  - 0->1->4

- BFS TASK
```C++
#ifdef MAZE

std::vector<short> dx = { 0, -1, 1, 0};
std::vector<short> dy = {-1, 0 , 0, 1};

struct Neigbour
{
	int x, y;
};

struct cell
{
	int x, y;
	int dest;
};



int main()
{

	int row_size = 0, column_size = 0;
	std::cin >> row_size >> column_size;
	int vertices = row_size * column_size;
	cell start;
	cell finish;

	std::vector<std::vector<int>> graph(vertices);


	std::vector<std::vector<char>> maze(row_size, std::vector<char>(column_size));
	std::vector<std::vector<int>> real_maze(row_size, std::vector<int>(column_size, -1));

	for (int i = 0; i < row_size; ++i)
	{
		for (int j = 0; j < column_size; ++j)
		{
			std::cin >> maze[i][j];

			//in bfs
			switch (maze[i][j])
			{
			case 'S':
				start = { j, i , 0};
				break;
			case 'F':
				finish = { j , i, -1};
				break;
			default:
				break;
			}
		}
	}


	//in make graph
	for (int i = 0; i < row_size; ++i)
	{
		for (int j = 0; j < column_size; ++j)
		{
			if (maze[i][j] == '#')
				continue;
			for (int k = 0; k < 4; ++k)
			{
				Neigbour neighbour = { dx[k] + j, dy[k] + i };

				if (neighbour.x >= 0 && neighbour.x < column_size 
					&& neighbour.y >= 0 && neighbour.y < row_size && maze[neighbour.y][neighbour.x] != '#')
				{
					graph[i * column_size + j].push_back(neighbour.y * column_size + neighbour.x);
				}
			}

		}
	}


	//bfs travers
	std::queue<cell> q;
	std::vector<std::vector<bool>> visited(row_size, std::vector<bool>(column_size, false));
	q.push(start);

	real_maze[start.y][start.x] = 0;

	while (!q.empty())
	{
		cell cur = q.front();
		visited[cur.y][cur.x] = true;
		q.pop();
		if (cur.x == finish.x && cur.y == finish.y)
			break;
		for (int k = 0; k < 4; ++k)
		{
			cell neighbour = { dx[k] + cur.x, dy[k] + cur.y , real_maze[cur.y][cur.x]};

			//wrong neighbour
			if (neighbour.x < 0 || neighbour.x >= column_size || neighbour.y < 0 || neighbour.y >= row_size
				|| visited[neighbour.y][neighbour.x])
				continue;

			//neighbour is wall
			if (maze[neighbour.y][neighbour.x] == '#')
			{
				real_maze[neighbour.y][neighbour.x] = -1;
				visited[neighbour.y][neighbour.x] = true;
				continue;
			}//isn't visited
			else
			{
				neighbour.dest = cur.dest + 1;
				visited[neighbour.y][neighbour.x] = true;
				real_maze[neighbour.y][neighbour.x] = neighbour.dest;
				q.push(neighbour);
			}

		}
	}


	std::cout << "Initial labyrinth:\n";
	for (int i = 0; i < row_size; ++i)
	{
		for (int j = 0; j < column_size; ++j)
			std::cout << maze[i][j];
		std::cout << "\n";
	}

	std::cout << "Graph:\n";
	for (int i = 0; i < vertices; ++i)
	{
		std::cout << i << " - ";
		if (graph[i].empty())
			std::cout << "None";
		for (int& v : graph[i])
			std::cout << v << " ";
		std::cout << "\n";
	}

	std::cout << "BFS result is:\n";
	
	for (int i = 0; i < row_size; ++i)
	{
		for (int j = 0; j < column_size; ++j)
			std::cout << real_maze[i][j] << " ";
		std::cout << "\n";
	}

	return 0;
}
#endif // MAZE

```