- Exists only in DAG = directed acyclic graph
- if edge (u,v) means u can be only before v
```C++
class Topological
{
private:
	std::stack<int> stack; //can be replaced with list or anything else
	std::vector<int> visited;
	std::vector<int> answer;
	int n;

public:
	Topological(int n, std::vector<std::vector<int>> graph) : n(n), visited(n, false)
	{
		Sort(graph);
	}

	std::vector<int> topoSort()
	{
		while (!stack.empty())
		{
			answer.push_back(stack.top());
			stack.pop();
		}
		return answer;
	}

private:
	void Sort(std::vector<std::vector<int>> graph)
	{
		for (int i = 0; i < n; ++i)
		{
			if (!visited[i])
			{
				dfs(graph, i);
			}
		}
	}

	void dfs(std::vector<std::vector<int>> graph, int u)
	{
		visited[u] = true;
		for (auto& v : graph[u])
		{
			if (!visited[v])
				dfs(graph, v);
		}
		stack.push(u);
	}

	
};

//Complex O(V + E);
```
//test
6
6
5 0
4 0
4 1
3 1
2 3
5 2

main
```C++
int main()
{
	int n, m;
	std::cout << "Nodes: ";
	std::cin >> n;
	std::cout << "\nEdges: ";
	std::cin >> m;

	std::vector<bool> visited(n, false);
	std::vector<std::vector<int>> graph(n);

	

	std::cout << "Enter graph: \n";
	for (int i = 0; i < m; ++i)
	{
		int from = 0, to = 0;
		std::cin >> from >> to;
		graph[from].push_back(to);
	}

	Topological topol(n, graph);

	std::cout << "\nLinear ordering: ";
	for (auto& el : topol.topoSort())
	{
		std::cout << el << " ";
	}
	return 0;
}
```
