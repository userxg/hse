# process exception

- use some class that describes an error
- throw - keyword for dealing with excpetions
```C++
#include <stdexcept>

Rational::Rational(int n, int d):numer(n)
{
	if (!d) throw std::invalid_argument("Cannot divide by zero"); //дальше невозможно без обработки
	denom = d; 
}

```
# catch exception
- we try
- then catch
- cerr - error stream
- what - output message 
```C++
while(True)
try
{
	Rational r1(1, 0) //some code you need to try
}
catch(std::invalid_argument ex)
{
	std::cerr << ex.what() << "\n";
}
```

Try catch - unified operator (so while we work fine)