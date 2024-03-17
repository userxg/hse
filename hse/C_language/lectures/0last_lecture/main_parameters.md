- you can enter something in cmd and it's will be a command line arguments
## intro

```C
int main(int argc, char* argv[])
{
	printf("argc: %d\n", argc);
	return 0;
}
```

**int argc** - count of arguments (is counting automatically)
**char argv[]**  our array of strings(exactly arguments)
we need to find folder with the project and run executable file
```PowerShell
cd "full path project"
example.exe 1 s "thrid param with spaces"
```
*output*
> 4
 * because name of executable file it's a first parameter and "1 2 3" three else

---
## how to debug
this way isn't convenient, because we can't debug 
in VS you can:
1. Open solution's properties([[property]]) ->
2. Debugging  
3. Write in *command arguments* some arguments (e.g. 1 2 3)
4. run or debug program (not from cmd, in cmd you need to pass args)
outputting arguments 
```C
int main(int argc, char* argv[])
{
	for (int i = 0; i < argc; i++)
		printf("%s\n", argv[i]);
	return 0;
}
```
*output*
>"full file path"
>1
>2
>3

---
## way to use
often we pass something convert it (*with atoi() e.g.*)  and do something
```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int min(int a, int b) { return ((a < b) ? a : b); }
int max(int a, int b) { return ((a > b) ? a : b); }



int main(int argc, char* argv[])
{
	if (argc != 3)
	{
		printf("2 arguments requierd!");
		exit(-1);
	}
	int lower = min(atoi(argv[1]), atoi(argv[2]));
	int higher = max(atoi(argv[1]), atoi(argv[2]));
	
	for (int i = lower; i < higher; ++i)
		printf("%d\n", i);
	return 0;
}
```
	exit(int x)- terminates program with code "x" (from stdlib.h)
```PowerShell
example.exe 10 8
```
*output*
>8
>9


