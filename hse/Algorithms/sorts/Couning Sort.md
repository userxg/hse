
Counting sort fist determines, for each input element x, the number of elements less than or equal to x. 
It then uses this information to place element x directly into its position in the output array. 
For example, if 17 elements are less than or equal to x, then x belongs in output position 17.
```cpp
void PrintArray(int* arr, int n);

unsigned* CountingSort(unsigned* A, int n, int k)
{
	//non negative int in range of 0 - k
	unsigned* B = new unsigned[n];
	unsigned* C = new unsigned[k + 1];

	//Init of C
	for (int i = 0; i <= k; ++i)
		C[i] = 0;

	//Fill C[i] contains amount of elements equal to i
	for (int j = 0; j < n; ++j)
		C[A[j]] = C[A[j]] + 1;
	
	for (int i = 1; i < k + 1; ++i)
		C[i] = C[i] + C[i - 1];

	for (int j = 0; j < n; ++j)
	{
		B[C[A[j]] - 1] = A[j];
		//Handle duplicate cases
		C[A[j]] = C[A[j]] - 1;
	}

	delete[] C;
	return B;
}


int main()
{
	int n = 6;
	unsigned A[6] = {5, 7, 2, 1, 6, 6};
	unsigned k = 7; //maximum of A
	unsigned* A_sorted = CountingSort(A, n, k);
	PrintArray((int*)A, n);
	PrintArray((int*)A_sorted, n);

	delete[] A_sorted;
	return 0;
}


void PrintArray(int* arr, int n)
{
	for (int i = 0; i < n; ++i)
		std::cout << arr[i] << " ";
	std::cout << "\n";
}
```