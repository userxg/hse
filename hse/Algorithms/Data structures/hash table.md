# hash table

Hash - data structure that is based on Dictionary principle 
as array but index is our key
Hash function - generate index in array by key

- Operations
	- put(key, value) - O(1), worst case O(n) because of collision
	- delete(key, value) O(1) - O(n)
	- get value(key) O(1) - O(n)
![[Pasted image 20240321153126.png|400]]
**open addressing** При возникновении коллизии ищем первый доступный пустой слот и помещаем туда ключ/значение.
During delete mark as "DEL"
PUT can put in "DEL" and free cell
Get - the same find as in Delete
## simple rolling hash
```C++
lld Hash(string key, int q, int p)
{
	lld hash = 0;
	int k = key.length();
	lld power_p = 1;
	for (int i = 0; i < k; ++i)
	{
		hash = (hash + (key[i] - 96)*power_p)%q;
		power_p = (power_p * p) % q;
	}
	return hash%q;
}
```
# realization

### task
Задача: В рамках данной задачи будет происходить эмуляция работы хэш-таблиц. В качестве хэш-функции используется полиномиальный cкользящий хеш.

Существует 3 доступных вида операций над хэш-таблицами:

PUT X Y - поместить в таблицу ключ X со значением Y GET X - вернуть значение по ключу X DEL X - удалить значение по ключу X

Во входном файле описана последовательность производимых операций, необходимо вывести короткий результат каждой из этих операций.

## Формат ввода

Первая строка входных данных содержит 3 числа, разделённых пробелами: q p n, где q и p - параметры хэш-функции, а n - число операций, которые будут описаны ниже.

Далее идут n строк, каждая из которых описывает отдельную операцию, пример:

PUT asdasd 3

GET asdasd

DEL asdasd

Ключами в рассматриваемой хэш-таблице являются строки, значениями - целые неотрицательные числа.

## Формат вывода

Ответом на задачу является лог, описывающий результаты каждой операции. Началом каждой строки будет являться значение ключа и хэш-код данного ключа

PUT X Y:

- если ключ X помещён без коллизий, то вывести key=X hash=??? operation=PUT result=inserted value=Y (подставить корректный хэш-код)

- если ключ X помещён с коллизиями, нужно вывести номер свободной ячейки, куда был в итоге помещён ключ и значение: key=X hash=??? operation=PUT result=collision linear_probing=1 value=Y

- если ключ X не был помещён по причине переполнения, вывести: key=X hash=??? operation=PUT result=overflow

GET X:

- если ключ X найден без коллизий, то вывести key=X hash=??? operation=GET result=found value=??? (подставить корректный хэш-код и значение)

- если ключ X найден с коллизиями, то вывести в какой ячейке был найден ключ и значение key=X hash=??? operation=GET result=collision linear_probing=34 value=??? (подставить хэш, ячейку где был найден linear_probing, значение)

- если ключ X не был найден с коллизиями, то вывести на какой ячейке остановился поиск и value=no_key key=X hash=??? operation=GET result=collision linear_probing=34 value=no_key (подставить хэш, ячейку где был найден linear_probing, значение)

- если ключ X не найден: key=X hash=??? operation=GET result=no_key

DEL X:

- если ключ Х найден и удалён без коллизий: key=X hash=??? operation=DEL result=removed

- если ключ Х найден и удалён c коллизиями: key=X hash=??? operation=DEL result=collision linear_probing=26 value=removed

- если ключ X не найден с коллизиями: key=X hash=??? operation=DEL result=collision linear_probing=26 value=no_key

- если ключ X не найден без коллизий: key=X hash=??? operation=DEL result=no_key

## solution
```C++
#include <iostream>
#include <string>
#include <cstdint>
#include <cmath>
#include <cstdlib>
#include <sstream>
using namespace std;

#define HASH


#ifdef HASH

typedef unsigned long long lld;


typedef struct element
{
	string key;
	lld value;
}elem;




void Put(elem* tb, string key, int q, int p);
void Get(elem* tb, string key, int q, int p);
void Del(elem* tb, string key, int q, int p);


lld Hash(string key, int q, int p);


int main()
{
	int q = 0, p = 0, n = 0;
	cin >> q >> p >> n;
	string examp = "eapusmby";
	elem* table = new elem[q];

	//table[0];
	//cout << Hash(examp, q, p);
	for (int i = 0; i < n; ++i)
	{
		string commad = "";
		string key = "";
		lld value = 0;

		cin >> commad >> key;

		if (commad == "PUT")
		{
			Put(table, key, q, p);
		}
		if (commad == "GET")
		{
			Get(table, key, q, p);

		}
		if (commad == "DEL")
		{
			Del(table, key, q, p);
		}
	}

	delete[] table;
	return 0;
}


void Put(elem* tb, string key, int q, int p)
{
	lld value = 0;
	cin >> value;
	lld hash = Hash(key, q, p);

	if (tb[hash].key == "" || tb[hash].key == "DEL")
	{
		tb[hash].key = key;
		tb[hash].value = value;
		cout << "key=" << key << " hash=" << hash << " operation=PUT result=inserted value=" << value << "\n";
		return;
	}
	else
	{
		int linear_probing = (hash + 1)%q;
		while (tb[linear_probing].key != tb[hash].key)
		{
			if (tb[linear_probing].key == "" || tb[linear_probing].key == key
				|| tb[hash].key == "DEL")                                         //check if the same key rewrite
			{
				tb[linear_probing].key = key;
				tb[linear_probing].value = value;
				cout << "key=" << key << " hash=" << hash << " operation=PUT ";
				cout << "result=collision" << " linear_probing=" << linear_probing << " value=" << value << "\n";
				return;
			}
			linear_probing = (linear_probing + 1)%q;
		}

		//overflow
		cout << "key=" << key << " hash=" << hash << " operation=PUT result=overflow" << "\n";
	}
}


void Get(elem* tb, string key, int q, int p)
{
	lld value = 0;
	lld hash = Hash(key, q, p);

	if (tb[hash].key == key)
	{
		cout << "key=" << key << " hash=" << hash << " operation=GET result=found value=" << tb[hash].value << "\n";
		return;
	}

	if (tb[hash].key == "")
	{
		cout << "key=" << key << " hash=" << hash << " operation=GET result=no_key" << "\n";
		return;
	}


	if (tb[hash].key != "")
	{
		int linear_probing = (hash + 1) % q;
		while (tb[linear_probing].key != tb[hash].key)
		{
			if (tb[linear_probing].key == key)
			{
				cout << "key=" << key << " hash=" << hash << " operation=GET ";
				cout << "result=collision" << " linear_probing=" << linear_probing << " value=" << tb[linear_probing].value << "\n";
				return;
			}

			if (tb[linear_probing].key == "")
			{
				cout << "key=" << key << " hash=" << hash << " operation=GET ";
				cout << "result=collision" << " linear_probing=" << linear_probing << " value=no_key"<< "\n";
				return;
			}

			linear_probing = (linear_probing + 1) % q;
		}
	}

	//overflow situation

	cout << "key=" << key << " hash=" << hash << " operation=GET ";
	cout << "result=collision" << " linear_probing=" << hash - 1 << " value=no_key" << "\n"; //maybe hash
	


}

void Del(elem* tb, string key, int q, int p)
{
	lld value = 0;
	lld hash = Hash(key, q, p);

	if (tb[hash].key == key)
	{
		tb[hash].key = "DEL";
		tb[hash].value = 0;
		cout << "key=" << key << " hash=" << hash << " operation=DEL result=removed" << "\n";
		return;
	}

	if (tb[hash].key == "")
	{
		cout << "key=" << key << " hash=" << hash << " operation=DEL result=no_key" << "\n";
		return;
	}

	if (tb[hash].key != "")
	{
		int linear_probing = (hash + 1) % q;
		while (tb[linear_probing].key != tb[hash].key)
		{
			if (tb[linear_probing].key == key)
			{
				tb[hash].key = "DEL";
				tb[hash].value = 0;
				cout << "key=" << key << " hash=" << hash << " operation=DEL ";
				cout << "result=collision" << " linear_probing=" << linear_probing << " value=removed" << "\n";
				return;
			}

			if (tb[linear_probing].key == "")
			{
				cout << "key=" << key << " hash=" << hash << " operation=DEL ";
				cout << "result=collision" << " linear_probing=" << linear_probing << " value=no_key" << "\n";
				return;
			}
			linear_probing = (linear_probing + 1) % q;
		}
	}

	cout << "key=" << key << " hash=" << hash << " operation=DEL ";
	cout << "result=collision" << " linear_probing=" << hash - 1 << " value=no_key" << "\n"; //maybe hash

}





lld Hash(string key, int q, int p)
{
	lld hash = 0;
	int k = key.length();
	lld power_p = 1;
	for (int i = 0; i < k; ++i)
	{
		hash = (hash + (key[i] - 96)*power_p)%q;
		power_p = (power_p * p) % q;
	}
	return hash%q;
}


```