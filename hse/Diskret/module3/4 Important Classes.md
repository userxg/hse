## T0
- f(0..0) = 0
- 0, diz, kon, xor, x
- Th: is closed

## T1
- f(1..1) = 1
- 1, diz, kon, ~, x, ->
- Th: is closed

## M - monotone funcs
- F is monotone if (a <= b) => (f(a) <= f(b))
- only neighbouring can be counted ( difference in only one symbol) (00 <= 01) 
- Th: is closed


## S - self-dual funcs
- F is self-dual if `f = f*` - > **!f(x..x) = f(!x...x)** e.g (if (000) = 1 -> (111) = 0)
- Th: is closed

## L - Lineal funcs
- F - is lineal if can be represented as Polynomial with only single quotients
- %2, 0, 1, x~x, !x, x 
- Th: is closed

