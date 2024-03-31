```cpp
class Entity
{

public:
	int x;
	bool alive;
	Entity(int x) : x(x), alive(true)
	{}
};

class Animal : public Entity
{
public:
	Animal(int x) : Entity(x) {}
};



int main()
{
	Entity* ent1 = new Entity(1);
	Animal* ent2 = new Animal(2);	
	std::vector<Entity*> ents;
	ents.push_back(ent1);
	ents.push_back(ent2);

	ents[1]->alive = false;
	for (int i = 0; i < ents.size(); ++i)
	{
		if (!ents[i]->alive)
			ents.erase(ents.begin() + i);
	}

	for (auto& ent : ents)
		std::cout << ent->x << "\n";

	return 0;
}
```
