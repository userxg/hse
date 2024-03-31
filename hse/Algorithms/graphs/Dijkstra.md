

- Task (both using priority_queue & set)
```cpp
#ifdef Dijkstra1

class Solution
{
private:
	struct City
	{
		std::string name;
		float x, y;
		std::vector<std::string> neighbours;
		
		float distance;
		City* parent;
	};
	int vertices;
	std::unordered_map<std::string, City> cities;
	std::string start, finish;

public:

	Solution(int v) : vertices(v) {}

	void run()
	{
		read_graph();

		//Dks_qu();
		Dks_set();

		print_solution();
		//print_graph();
	}
	


private:
	void Dks_set()
	{
		std::set<std::pair<float, std::string>> S_queue;
		cities[start].distance = 0.0;
		S_queue.insert({ cities[start].distance, cities[start].name });

		while (!S_queue.empty())
		{
			std::pair<float, std::string> current = *S_queue.begin();
			S_queue.erase(current);

			for (auto& neighbour : cities[current.second].neighbours)
			{
				float weight_u_v = weight(current.second, neighbour);
				if (cities[neighbour].distance > cities[current.second].distance + weight_u_v)
				{
					S_queue.erase({ cities[neighbour].distance , neighbour});
					cities[neighbour].distance = cities[current.second].distance + weight_u_v;
					cities[neighbour].parent = &cities[current.second];
					S_queue.insert({ cities[neighbour].distance , neighbour });
				}
			}

		}

	}
	void Dks_qu()
	{
		//init
		std::priority_queue < std::pair<float, std::string >, 
			std::vector<std::pair<float, std::string>>, 
			std::greater<std::pair<float, std::string>> > P_queue;

		cities[start].distance = 0.0;
		P_queue.push({ cities[start].distance, cities[start].name });

		while (!P_queue.empty())
		{
			std::pair<float, std::string> current = P_queue.top();
			P_queue.pop();

			for (auto& neighbour : cities[current.second].neighbours)
			{
				if (Relax(current.second, neighbour))
				{
					P_queue.push({ cities[neighbour].distance, cities[neighbour].name });
				}
			}
		}
	}

	bool Relax(std::string u, std::string v)
	{
		float weight_u_v = weight(u, v);
		if (cities[v].distance > cities[u].distance + weight_u_v)
		{
			cities[v].distance = cities[u].distance + weight_u_v;
			cities[v].parent = &cities[u];
			return true;
		}
		return false;
	}



	float weight(std::string u, std::string v)
	{
		float pow1 = std::pow((cities[u].x - cities[v].x), 2);
		float pow2 = std::pow((cities[u].y - cities[v].y), 2);
		float result = sqrt(pow1 + pow2);

		return result;
	}

	void read_graph()
	{
		for (int i = 0; i < vertices; ++i)
		{
			std::pair<std::string, City> input{ "", {"", 0.0, 0.0, {}, std::numeric_limits<float>::max(), nullptr} };
			pars(input);
			cities.insert(input);
		}
		std::cin >> start >> finish;
	}

	void pars(std::pair<std::string, City>& input)
	{
		std::string input_string;
		getline(std::cin, input_string);

		std::stringstream ss(input_string);
		std::string piece;
		int i = 0;
		ss >> piece;
		input.first = piece;
		input.second.name = piece;
		ss >> input.second.x;
		ss >> input.second.y;

		while (ss >> piece)
		{
			input.second.neighbours.push_back(piece);
		}
	}

	void print_solution()
	{
		std::vector<City*> path;
		City* last = &cities[finish];

		while (last)
		{
			path.push_back(last);
			last = last->parent;
		}
		

		if (path.back()->name != start)
		{
			std::cout << "Path:\n" << "No way";
		}
		else
		{
			std::cout << "Path is not greater than " << std::ceil(cities[finish].distance) << "\n";
			std::cout << "Path:\n";
			
			for (int i = path.size() - 1; i >= 0; i--)
			{
				std::cout << path[i]->name << " ";
			}
		}
	}


	void print_graph()
	{
		std::cout << "\nINPUT\n"; 
		for (auto& u : cities)
		{
			std::cout << u.first << " " << u.second.x << " " << u.second.y << " ";
			for (auto& v : u.second.neighbours)
				std::cout << v << " ";
			std::cout << u.second.neighbours.size() << " units";
			std::cout << "\n";
		}
		std::cout << start << " " << finish;
	}

};



int main()
{
	int v = 0;
	std::cin >> v;
	//clear buffer
	std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');

	Solution dks(v);
	dks.run();

	return 0;
}
#endif
```
