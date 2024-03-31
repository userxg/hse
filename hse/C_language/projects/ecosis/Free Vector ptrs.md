```cpp
class Entity
{
private:
	int x_, y_;
public:
	Entity() :
		x_(0), y_(0)
	{
		std::cout << "Created " << "\n";
	}

	~Entity() {std::cout << "Destroyed\n"; }
};

void AddEntities(std::vector<Entity*>& entities)
{
	Entity* e1 = new Entity();
	Entity* e2 = new Entity();

	entities.push_back(e1);
	entities.push_back(e2);
}


int main()
{	
	std::vector<Entity*> entities;
	AddEntities(entities);

	for (auto& entity : entities)
		delete entity;

	return 0;
}
```