# definition
a = b (mod n) if and only if n | a - b (n divides a - b)
a, b, n are integer; n > 1
- a is [[congruent]] to b if n divides ( a - b )
- d | a  means a is divided into d  or d divides a
### ex
5 = 2 (mod 3)   ->   (5 - 2) / 3 = integer
4 = -1 (mod 5) - >  (4 - (-1)) / 5 = integer
### ex
find all possible values of n if *11 = 5 (mod n)*
n | 11 - 5 =>  n | 6 , n > 1  =>  n = 1, 2, 3

- Modular Arithmetic deals with remainders
- Divide ***a** by ***n*** and let the [[quotient]] be ***q*** and the remainder ***r***, then we have 
> a = n x q + r which implies(imply) a = r (mod n)
> *ex*: 13 by 5 ->  13 = *2* x 5 + 3 -> 13 = 3 (mod 5)
> -3 = -8 (mod 5) ->  -3 = 5 x N + (-8) (n = 1)

- ## important property
> (a + b) mod p = ( (a mod p) + (b mod p) ) mod p 
> (a - b) mod p = ( (a mod p) - (b mod p) ) mod p 
> (ab) mod p = ( (a mod p) (b mod p) ) mod p 

```
For example a = 50,  b = 100, p = 13
50  mod 13  = 11
100 mod 13  = 9           11             9
                          |              |
(50 * 100) mod 13 = ( (50 mod 13) * (100 mod 13) ) mod 13 
or (5000) mod 13 = ( 11 * 9 ) mod 13
or 8 = 8

31^500 % 30 = 1         500times
31 % 30 = 1 -> ( 31%30 * 1 *...* 1 ) %30 = 1^500 % 30 = 1

11^7 mod 13 = 2
-2^7 mod 13 = -128 mod 13 = 2


```

---
more about [here](https://www.youtube.com/watch?v=gmHscLG3ceg&list=PLynSqvOa5siHPX2F5quoZgPy90oVyVidE&index=1)(playlist)
Solving [[Iterative ModExp]]  but with [math](https://www.youtube.com/watch?v=_gYUlvcnjs0) and [this](https://www.youtube.com/watch?v=bg0P_3UiG5I) 