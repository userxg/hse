
# pointer to current thing

- use case if we decided to make arguments the same name of class fields
```C++
Rational::Rational(int numer, int denom) : numer(numer)
{
	if (!denom)
		throw std::invalid_argument("wrong data");
	this->denom = denom;
}
```