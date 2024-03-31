- 6 merge, timsort
```
MergeSort(A, n)
	MergeSortRecursion(A, 0, n - 1)

MergeSortRecursion(A, l, r)
	if (l <= r)
		m = l + r / 2
		MergeSortRecursion(A, 0, m)
		MergeSortRecursion(A, m + 1, r)
		MergeSorted(A, 0, m, r)
	return

MergeSorted(A, l, m, r)
	Nl = m
	Nr = r - (m + 1)
	Left(Nl)
	Rigth(Nr)
	for i = 0 to Nl
		Left[i] = A[i + l]
	for i = 0 to Nr
		Right[i] = A[i + (m + 1)]

	l , r = 0
	k = l

	while (l < Nl && r < Nr)
		if (Lelf[l] <= Rigth[r])
			A[k] = Left[l]
			k++, l++
		else
			A[k] = Right[r]
			k++, r++

	 while (l < Nl)
		A[k] = Left[l]
		k++, l++
		
	 while (r < Nr)
		A[k] = Left[l]
		k++, l++
```
```
///timsort
InsertionSort(A, l, r);
MergeSorted(A, l, m, r);
TimSortIter(A, n)
	choose RUN = 2^k (optimal 32, 64)
	for i = 1 to n (i+=RUN) //sort subarrays
		InsertionSort(A, i , min(i + RUN, n))
	//increase size 32, 64, n 
	for size = RUN to n (size*=2)
		//choose left, mid and right for Mergefucn
		for l = 0 to n (l += size*2)
			m = l + size - 1
			r = min(m + size, n)
			MergeSorted(A, l, m , r)
```

- 7 Quick sort
```
QuickSort(A, p , r)
	if l >= r
		return 
	pivot = Partition(A, p, r)
	QuickSort(A, l , pivot - 1)
	QuickSort(A, pivot + 1 , r)

Partition(A, p, r)
	x = ChoosePivot(A, p, r)
	i = p - 1
	for j to r - 1 //because r is x
		if A[j] <= x
			i = i + 1 //shift smaller area
			swap(a[i], a[j])
	swap(A[i + 1], A[r])
	return i + 1

ChoosePivot(A, p, r)
	swap(a[r], random A[p..r - 1])
	return a[r]

HoarePartition(A, p, r)
	x  = A[p]
	i = p
	j = r
	while i < j
		while i <= x && i <= r
			i++
		while j > x && j >= p
			j--
		if i < j
			swap(A[i], A[j])
	swap(A[j], A[r])
	return j
```



- 8
```
Euclid(a, b)
	if (b == 0)
		return a;
	return (b , a mod b)
```
```
ax + by = d
a'x' + b'y' = d
a' = a%b = a - [a/b]*b
b' = a
ax + by = d
(a - [a/b]*b)*x' + ay' = d


d = ax + by, d = a => x = 1, y = 0
Euclid-Extended(a, b)
	if (b == 0)
		return (a, 1, 0)
	else
		(d',x',y') = Euclid-Extended(b, a mod b)
		(d, x, y) = (d', y', x' - [a/b]*y')
		return (d, x, y)
a*x + b*y = d
a'*x' + b'*y' = d
a' = b
b' = a%b = a - [a/b]*b
=> x
```
```
eratosphen-seive
for i = 1 to n
	a[i] = i
for i = 1 to sqrt(n)
	if a[i] != 0
	for j = a[i]*a[i] to n (j+=a[i])
		a[j] = 0
O(n*(loglogN))

LCM(a, b)
 return a*b/gcd(a,b)
k - min and a|k, b|k and a*b|k, we need to divide a*b
=> maximum possible is gcd
```

- 9 Is prime?
```
a^b mod n
a * b mod n = (a mod n * b mod n)mod n
Modular-Exponentiation(a, b, n)
	if (b == 0)
		return 1
	if (b mod 2 = 0)
		d = Modular-Exponentiation(a, b/2, n)
		return (d * d) mod n
	else
		d = Modular-Exponentiation(a, b - 1, n)
		return (d * a) mod n
```
```
Fermat's()
for a to n - 1
	if MOD-EXP(a, n - 1, n) != 1
		return 0 //definately no
return 1  //possibly prime
```

```
Miller-Rab(n, s)
for i = 1 to s
	a = Random(3, n - 2)
	if Witness(a, n)
		COMPOSITE surely
	MAYBE PRIME

WITNESS(a, n)
take t >= 1 and u is odd, n - 1 = 2^t * u
u = n - 1
while (u % 2 != 1)
	t++
	u / 2

X0 = MOD-EXP(a, u, n)
for i to t
	Xi = (Xi-1)^2 mod n
	if Xi = 1 && Xi-1 != 1 && Xi-1 != n-1
		TRUE
if Xt != 1
	TRUE
FAlSE
```


