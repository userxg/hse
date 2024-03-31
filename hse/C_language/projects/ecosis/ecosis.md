## ideas
- may be make tracking units
- chasing - while x_wolf != x_pig: x_wolf(++ or --) and for y the same
- create array grid array of chars to track entities positions with all entities the same size
- grid game
- create animation for going from one cell to another

## redo
new grid system
implement delta time
new spawn of childs (with check function)
death of plants
moveTawords

FrameGrids
Live function
change class members

separate LiveUpdate

Engine  - first initialization in constructor

Moving straight algorithm
```c++
// Example program
#include <iostream>
#include <cmath>

struct Vector2 {
    double x;
    double y;
};

Vector2 operator*(double scale, const Vector2& vec)
{
    return Vector2{scale * vec.x, scale * vec.y};
}

std::ostream& operator<<(std::ostream& os, const Vector2& vec)
{
    return os << "(" << vec.x << ", " << vec.y << ")";   
}

Vector2 operator+(const Vector2& a, const Vector2& b)
{
    return Vector2{a.x + b.x, a.y + b.y};   
}
Vector2 operator-(const Vector2& a, const Vector2& b)
{
    return Vector2{a.x - b.x, a.y - b.y};   
}
Vector2 operator/(const Vector2& vec, double scale)
{
    return Vector2{vec.x / scale, vec.y / scale};
}

double magntiude_squared(const Vector2& vec)
{
    return vec.x * vec.x + vec.y * vec.y;
}

Vector2 normalize(const Vector2& vec)
{
    if (vec.x == 0.0 && vec.y == 0.0)
        return Vector2{0.0, 0.0};
        
    return vec / std::sqrt(magntiude_squared(vec));
}


class Object {
  public:
    void MoveTowards(const Vector2& target, double speed);
    
    Vector2 position;
};

void Object::MoveTowards(const Vector2& target, double speed)
{
    Vector2 delta = target - this->position;
    if (magntiude_squared(delta) < speed * speed)
    {
        // set to target if our speed would go beyond the target
        this->position = target;
    }
    else
    {
        this->position = this->position + speed * normalize(delta);  
    }
}

int main()
{
    double timestep = 1.0 / 60.0; // or whatever... see "fix your timestep" article
    Object player;
    player.position = Vector2{100, 100};
    
    Vector2 target {200, 300};
    double speed = 320;
    
    for (int i = 0; i < 50; i++)
    {
        player.MoveTowards(target, speed * timestep);
        std::cout << player.position << '\n';
    }
}
```