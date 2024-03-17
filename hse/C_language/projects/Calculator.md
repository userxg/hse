вводится строка сносим пробелы ( в ней ищем F,A, B, C , D....)

1. Вводиться строка
	2. Проверяем на валидность (через стек)
	3. Ищем в в ней буквы `[A - Z]` (добавляя в копилку функций)
3. Если валидна -> спрашиваем выражение для каждой A-Z
	1. Построчный ввод выражений
		2. Проверяем на валидность 
		3. Ищем `[a - z]` (добавляем в копилку переменных)
4. Спрашиваем значения
	- Вычисляем (Поднимаясь вверх =  вычисляем A-Z --> вычисляем строку) - скрутка стека
	- Если не подходят в функцию
		1.  выводим ошибку с инструкцией и в
		2. Возвращаемся на шаг 4



## ex:
```bash
Enter expression:
sin(F) + cos(A + B)- (H*log(A, B)) #ввёл ползователь

Enter definitions of functions F, A, B: # выводим F =  дальше вводит пользователь
F = x^2x + sdf
A = z + y;
B = -z;

Enter values of variables x, y, z:
x = 0.5
y = 10
z = 34

[ERROR]Number in function log must be higher than zero
Enter values again
Enter values of variables x, y, z:
x = ..
y = ...
z = ...


```

Ответ в интерфейсе как [тут](https://www.youtube.com/watch?v=V6zO9lRl2Sg)


класс функий
класс определения 
класс 
класс вывода

- std::stold() - convert string to long double .
- create array of operations
- stack_opereations - strings
- setprecision
- overloading operator

needs
- ld stack
- leksema stack
- struct (leksema + size)
- set


## fix
- double unary minus (may be through cin.ignore)
- remove continue in the last while
- 2 -3 2
- 5 5 + 3
- 5* -1 - exception
- 64^-1
```C++
6
^
-
exception
-
1
otvet: -1
```
```


C унарным минусом можно разобраться значительно проще. если "-" стоит в начале формулы(первый символ), то заменяем его "0-". если в формуле встречается последовательность "(-", то ее заменяем на "(0-". В нынешнем виде представленный строковый калькулятор не правильно обрабатывает унарный мину в скобках правильным образом(насколько помню в 3 части автор это не исправил) например: 3*(-2+3) = 4.


в коде ошибка не читал пока комментов (-2+3)+(-6*3) не сработает надо когда мы писали правила для скобки поставить флаг=1 тогда заработает 
```C++
if (box=='('){ objeckt.tip_char = box; objeckt.tip_double = '0'; stack_operation.push(objeckt); cin.ignore(); flag=1; continue; }
```