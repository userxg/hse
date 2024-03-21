# Disjoint with optimization

idea: store date in disjoint subsets
## complexity
1. *MAKE_UNION* `t(1)` 
	- put in i index i
2. *FIND*- `O(N)` - without path compression 
	- N - high of tree, base how many branches we have
	- Swap - `O(1)`
	- SiftDown - `O(lonN)`
3. Get Max/Min - `O(1)`

## path compresion
5. *MakeSet* `O(1)` 
	- Assign elem of array by x
6. *Find*- `O(logN)` or *nearly constant*
	- with path compression and rank
7. Union - as a Find
# disjoint task with
- Path optimization
- Rank optimization 
```cpp
class Disjoint
{
private:
	std::vector<int> a;
	std::vector<int> rank;
	std::vector<int> vals;
	int max = 0;
	int requests = 0;
public:
	Disjoint(int range, int m) : requests(m)
	{
		int input_val = 0;
		
		a.resize(range + 1);
		rank.resize(range + 1);
		vals.resize(range + 1);
		for (int i = 1; i < range + 1; ++i)
		{

			Make_Set(i);
			std::cin >> input_val;
			if (input_val > max)
				max = input_val;
			vals[i] = input_val;
		}
	}

	void work()
	{
		int dest = 0, src = 0;
		for (int i = 0; i < requests; ++i)
		{
			std::cin >> dest >> src;
			Union(dest, src);
		}
	}
	

	int	 Find(int x)
	{
		if (x != a[x])
			a[x] = Find(a[x]);
		return a[x];
	}

	void Union(int x, int y)
	{
		int root_x = Find(x);
		int root_y = Find(y);
		if (root_x == root_y)
		{
			std::cout << max << std::endl;
			return;
		}
		if (rank[root_x] < rank[root_y])
		{
			vals[root_y] += vals[root_x];
			vals[root_x] = 0;
			if (vals[root_y] > max)
				max = vals[root_y];

			a[root_x] = root_y;
			std::cout << max << std::endl;
		}
		else
		{
			bool equal = rank[root_x] == rank[root_y];
			//change values
			vals[root_x] += vals[root_y];
			vals[root_y] = 0;
			if (vals[root_x] > max)
				max = vals[root_x];

			//change root
			a[root_y] = root_x;
			if (equal) rank[root_x]++;

			std::cout << max << std::endl;
		}
	}
private:
	void Make_Set(int x)
	{
		a[x] = x;
		rank[x] = 0;
	}
};
int main()
{
	int n = 0, m = 0;
	std::cin >> n >> m;
	Disjoint D(n, m);
	D.work();
	return 0;
}
```


Task:
Ваша цель в данной задаче — реализовать симуляцию объединения таблиц в базе данных. В базе данных есть n таблиц, пронумерованных от 1 до n, над одним и тем же множеством столбцов (атрибутов). Каждая таблица содержит либо реальные записи в таблице, либо символьную ссылку на другую таблицу. Изначально все таблицы содержат реальные записи, и i-я таблица содержит ri записей. Ваша цель — обработать m запросов типа (destinationi , sourcei):

1. Рассмотрим таблицу с номером destinationi. Пройдясь по цепочке символьных ссылок, найдём номер реальной таблицы, на которую ссылается эта таблица:
    
    пока таблица destinationi содержит символическую ссылку: destinationi←symlink(destinationi)
    
2. Сделаем то же самое с таблицей sourcei.
3. Теперь таблицы destinationi и sourcei содержат реальные записи. Если destinationi≠sourcei, скопируем все записи из таблицы sourcei в таблицу destinationi, очистим таблицу sourcei и пропишем в неё символическую ссылку на таблицу destinationi.
4. Выведем максимальный размер среди всех n таблиц. Размером таблицы называется число строк в ней. Если таблица содержит символическую ссылку, считаем её размер равным нулю.

Задача из курса «Алгоритмы: теория и практика. Структуры данных»: [https://stepik.org/course/1547/syllabus](https://stepik.org/course/1547/syllabus)

## Формат ввода

Первая строка содержит числа n и m — число таблиц и число запросов, соответственно. Вторая строка содержит n целых чисел r1,…,rn — размеры таблиц. Каждая из последующих m строк содержит два номера таблиц destinationi и sourcei, которые необходимо объединить (1≤n,m≤100000; 0≤ri≤10000; 1≤destinationi, sourcei≤n).

## Формат вывода

Для каждого из m запросов выведите максимальный размер таблицы после соответствующего объединения.

### Пример 1

|Ввод<br><br> ![Скопировать ввод](https://yastatic.net/lego/_/La6qi18Z8LwgnZdsAr1qy1GwCwo.gif)|Вывод<br><br> ![Скопировать вывод](https://yastatic.net/lego/_/La6qi18Z8LwgnZdsAr1qy1GwCwo.gif)|
|---|---|
|5 5<br>1 1 1 1 1<br>3 5<br>2 4<br>1 4<br>5 4<br>5 3|2<br>2<br>3<br>5<br>5|

### Пример 2

| Ввод<br><br> ![Скопировать ввод](https://yastatic.net/lego/_/La6qi18Z8LwgnZdsAr1qy1GwCwo.gif) | Вывод<br><br> ![Скопировать вывод](https://yastatic.net/lego/_/La6qi18Z8LwgnZdsAr1qy1GwCwo.gif) |
| ---- | ---- |
| 5 5<br>1 2 3 4 5<br>3 5<br>2 4<br>1 4<br>5 4<br>5 3 |  |
