# Th-s Langrange', Koshi's, Lopital's

## Langrange's Th
- f(x) is on `[a,b]` and continuous
- is differentiable on `(a,b)`
=> c exists that **f'(c) = (f(b) - f(a) / b - a** 
### *proof*
- auxiliary F(x) = f(x) - ax 
- F(a) = F(b)
- F'(x) = 0
### geometrical meaning   - point with parallel straight exists 
### the formula of finite increments f(x + deltx) - f(x) = deltf = f'(c)deltX


## Koshi's Th
- f(x) and g(x) is on `[a,b]` and continuous
- is differentiable on `(a,b)` and g'(x) != 0
=> c exists that **f'(c)/g'(c) = (f(b) - f(a) / g(b) - g(a)**
### *proof*
- auxiliary F(x) = f(x) - ag(x) 
- check if g(a) = g(b) -> g'(x) = 0 exists 
- F(a) = F(b)
- F'(x) = 0

## Lopital's for x->a+0 (0/0)
- if f(x) and g(x) on `(a,b)` 
- is differentiable on `(a,b)` and g'(x) != 0
- lim f(x) = lim g(x) = 0
- lim f'(x)/g'(x) = a or inf 
=>**lim f(x)/g(x) = limf'(x) /g'(x)**
### *proof*
- redefine x = a = 0
- choose [[arbitrary]] x
- Apply Koshi's where f(a) = g(a)  = 0
- find lim and replace c to x

## Lopital's for x->+inf (0/0)
- if f(x) and g(x) on `(a,+inf)` 
- is differentiable on `(a,+inf)` and g'(x) != 0
- lim f(x) = lim g(x) = 0
- lim f'(x)/g'(x) = a or inf 
=>**lim f(x)/g(x) = limf'(x) /g'(x)**
### *proof*
- a > 0
- replace y = 1/x
- replace f(1/y) = f(y)
- find lim and back with complex function