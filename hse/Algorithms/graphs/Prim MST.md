Test
3 3
0 1 5
1 2 3
0 2 1

```C++
struct Node
{
	int weight;
	int node;
};


class Prim
{
public:
	int prim(int node, std::vector<std::vector<Node>> graph)
	{
		int n = graph.size();
		std::vector<bool> visited(n, false);
		std::priority_queue < std::pair<int, int>, std::vector < std::pair<int, int>>, std::greater<std::pair<int, int>>> P_queue;
		std::pair<int, int> root = { 0 ,node };

		P_queue.push(root);
		
		int MST_sum = 0;
		//V
		while (!P_queue.empty())
		{
			std::pair<int, int> node = P_queue.top();
			//log V
			P_queue.pop();

			int u = node.second;
			int weight = node.first;

			if (visited[u]) continue;

			visited[u] = true;
			MST_sum += weight;
			//E
			for (auto& v : graph[u])
			{
				if (!visited[v.node])//Log V
					P_queue.push({ v.weight, v.node });
			}
		}
		return MST_sum;
	}
//VlogV + ElogV = ElogV
};
```

- main
```C++
int main()
{
	int n, m;
	std::cout << "Nodes: ";
	std::cin >> n;
	std::cout << "\nEdges: ";
	std::cin >> m;	
	
	std::vector<std::vector<Node>> graph(n);

	

	std::cout << "Enter graph: \n";
	for (int i = 0; i < m; ++i)
	{
		int from = 0, to = 0, weight = 0;
		std::cin >> from >> to >> weight;
		graph[from].push_back({weight, to});
		graph[to].push_back({ weight, from });
	}

	Prim solution;
	
	std::cout << solution.prim(0, graph);



	return 0;
}
```