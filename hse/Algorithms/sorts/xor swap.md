*Method: (Using Bitwise XOR)*
The bitwise XOR operator can be used to swap two variables. The XOR of two numbers x and y returns a number that has all the bits as 1 wherever bits of x and y differ. For example, XOR of 10 (In Binary 1010) and 5 (In Binary 0101) is 1111, and XOR of 7 (0111) and 5 (0101) is (0010).

```C
void xorswap(int* x, int* y)
{
	if (x == y)//if user 
		return;// because we get zero by using XOR
	*x = *x ^ *y;
	*y = *x ^ *y;
	*x = *x ^ *y;
}
```