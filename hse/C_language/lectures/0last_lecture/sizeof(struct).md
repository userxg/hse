## why?
What will sizeof() return?
```C
struct data
{
	char x;
	int y;
	char z;
};


int main()
{
    printf("%zu", sizeof(struct data));
    return 0;
}
```

> *12*

because there are paddings between char x and int y, in this case **data** was aligned([[align]]) to the biggest size (in this case it's int = 4 byte)
> ![[Pasted image 20240105085218.png]]

* If we have two structs nested([[nest]]) one into the other size will be aligned in the same way
```C
struct data
{
    double x;
};

  

struct data2
{
    char x;
    char J;
    int z;
    struct data y;
};

  
  

int main()
{
    printf("%zu\n", sizeof(struct data));
    printf("%zu", sizeof(struct data2));
    return 0;
}
```
output sizeof(data2) will be

>8
>16

because (X J 0 0 Z Z Z Z Y Y Y Y Y Y Y Y)
