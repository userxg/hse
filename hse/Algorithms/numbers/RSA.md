# Encryption and Decryption algorithm
> Use (public key + message) - > encrypted message
> Use (private key + en msg) - > message
## Generating Key
### Public key 
1. Select two Prime Numbers: `P, Q`
2. Compute Product: `N = P * Q`
3. Calculate Totient using [[Euler funtion]] = `T = (P - 1)*(Q - 1)`
4. Select ***Public key***: `2 < E < T,  gcd(E, T) == 1`
	- Less than Totient.
	- Must not be a factor of the Totient (to be co-prime)

### Private key
5. Select D that `E * D = 1 mod(Totient)`
	1. find d using [[GCD Extended]]
```
1) P,Q  
2) N = P * Q  
3) T = f(N) = (p - 1) (q - 1)  
4) 2 < E < T,  gcd(E, T) = 1  
5) DE (mod T) = 1 -> DE = T*K + 1 -> ED - T*K = 1

now Encrypt M^e mod n
Decrypt C^d mod n
```

Rsa for six letters 
```C++
#include <iostream>
#include <cmath>
#include <string>
#include <cstdint>
#include <stdio.h>
using namespace std;
typedef unsigned long long ull;
//typedef long long __int128;

__int128 gcdExd(__int128 a, __int128 b, __int128* x, __int128* y);
__int128 exp(__int128 x, __int128 y, __int128 p);

int main()
{
	__int128 p = 0, q = 0, e_start = 0;
	__int128 d = 0;
	__int128 x = 0;
	__int128 y = 0;

	string msg = "";
	std::cin >> (ull)p >> (ull)q >> e_start;
	std::cin >> msg;
	__int128 msg_len = msg.length();
	__int128 n = p * q; //product
	__int128 totient = (p - 1) * (q - 1);

	while (e_start < totient)
	{
		if (gcdExd(e_start, totient, &x, &y) == 1)
			break;
		++e_start;
	}
	d = (x % totient + totient) % totient;
	//while (d < 0) d += totient;
	__int128 e = e_start;

//use scanf for __in128
	std::cout << "Private: " << (ull)d << ' ' << n << '\n';
	std::cout << "Public: " << (ull)e << ' ' << n << '\n';


	std::cout << "Initial bytes: ";
	for (int i = 0; i < msg.length(); ++i)
		std::cout << (int)msg[i] << ' ';
	std::cout << '\n';

	string word = "";
	for (__int128 i = 0; i < msg_len; ++i)
	{
		string buf = "00000000";
		char x = msg[i];
		__int128 j = 7;
		while (x > 0)
		{
			if (x % 2 == 1) buf[j] = '1';
			else buf[j] = '0';
			x /= 2;
			--j;
		}
		word.append(buf);

	}

	__int128 word_len = word.length();
	__int128 msg_num = 0;
	for (__int128 i = 0; i < word_len; ++i)
	{
		if (word[word_len - i - 1] == '1') msg_num += pow(2, i);
	}



	__int128 encrypted = exp(msg_num, e, n);

	string buf = "";
	while (encrypted > 0)
	{
		if (encrypted % 2 == 1) buf.append("1");
		else buf.append("0");
		encrypted /= 2;
	}
	__int128 len_en = buf.length();
	__int128 len_bit_en = (len_en + 8 - 1) / 8 * 8;
	for (__int128 i = 0; i < len_bit_en % len_en; ++i)
		buf.append("0");

	string enc_bin = "";
	for (__int128 i = 0; i < len_bit_en; ++i)
	{
		if (buf[len_bit_en - 1 - i] == '1') enc_bin.append("1");
		else enc_bin.append("0");
	}

	std::cout << "Encrypted bytes: ";
	int bite = 0;
	for (__int128 i = 0; i < len_bit_en / 8; ++i)
	{

		for (__int128 j = 0; j < 8; ++j)
		{
			if (enc_bin[i * 8 + (7 - j)] == '1') bite += pow(2, j);
		}
		std::cout << bite << ' ';
		bite = 0;
	}
	return 0;
}


__int128 gcdExd(__int128 a, __int128 b, __int128* x, __int128* y)
{
	if (b == 0)
	{
		*x = 1;
		*y = 0;
		return a;
	}
	__int128 x1 = 0, y1 = 0;
	__int128 gcd = gcdExd(b, a % b, &x1, &y1);

	*x = y1;
	*y = x1 - (a / b) * y1;

	return gcd;
}
__int128 exp(__int128 x, __int128 y, __int128 p)
{
	if (y == 0)
		return 1;
	__int128 k = exp(x, y / 2, p) % p;
	k = (k * k) % p;

	return (y % 2 == 0) ? k : (x * k) % p;
}
```