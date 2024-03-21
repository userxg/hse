idea: LIFO principle
operations:
- push - `t(1)`
- pop - `t(1)`
- Top - `t(1)`
- isEmpty - `t(1)`

Has size, top, array
# Cormen
- array implementation
```cpp
class Stack
{
private:
	int size; //amount
	int top; // index
	int* arr;
public:
	Stack(int size) : size(size)
	{
		arr = new int[size];
	}
	bool StackEmpty() { return top == 0; }
	void Push(int x)
	{
		if (top == size)
			std::cout << "Overflow";
		else
			arr[top++] = x;
	}
	int Pop()
	{
		if (StackEmpty())
		{
			std::cout << "Undeflow";
			//throw error
		}
		else
		{
			top = top - 1;
			return arr[top];
		}		
	}
};
```


```C++
#include <iostream>
#include <string>
#include <cstdlib>
#include <sstream>
using namespace std;
enum variables {max_polish = 500, base_opreations_size = 15};


template <typename DataType>

class Stack
{
private:
	struct Node
	{
		Node(DataType elem) : element(elem) {}
		Node* next;
		DataType element;
	};
	Node* head;
	int size;

public:
	Stack() : head(nullptr), size(){};

	void push(DataType elem)
	{
		Node* old_node = head;
		head = new Node(elem);
		head->next = old_node;
		size++;
	}

	void pop()
	{
		if (!isEmpty())
		{
			Node* del = head;
			head = head->next;
			delete del;
			size--;
		}
	}

	
	DataType top() const 
	{
		if (!isEmpty())
			return head->element;
		return 0; 
	}

	bool isEmpty() const
	{
		return size == 0;
	}



private:

public:
	~Stack()
	{
		Node* del = head;
		while (del)
		{
			Node* cur = del;
			del = del->next;
			delete cur;
		}
	}
};
```


# Polish Notation 
## use case of stack

1. make reverse output
	1. if operator -> stack
	2. if operand -> output line
	3. while priority of operator <= priority of stack.top() - > in output line
	4. (  - the lowest priority
	5. ) - all things -> in output
2. read output
	1. if operand -> stack 
	2. if operator -> grab value for counting result of operator

more [info](https://github.com/il-bychkov/algorithms/blob/main/practice/6_simple_data_structures/readme_ru.md)

```C++

struct Leksema
{
	Leksema() : operation("0"), value(), priority(-1) {}
	string operation;
	int value;
	char priority;
};

struct postfix
{
	postfix() : leksems(), size() {}
	Leksema* leksems[max_polish];
	int size;
};

//int find_priority(string operation,)

int main()
{
	postfix main_origin;
	postfix* main = &main_origin;

	string expression = "";
	getline(cin, expression);
	

	

	//creating postfix
	int index = 0;
	Stack<Leksema*> stack_operations;
	int expression_length = expression.length();

	//read 
	for (; index < expression_length;)
	{

		if (expression[index] >= '0' && expression[index] <= '9')
		{
			Leksema* number_elem = new Leksema();
			string number_s = "";
			int number = 0; //change to double
			while (expression[index] >= '0' && expression[index] <= '9') //add check .
			{
				number_s = number_s + expression[index];
				index++;
			}


			stringstream convert;  //good way to convert
			convert << number_s;
			convert >> number;

			number_elem->value = number;
			main->leksems[main->size++] = number_elem;
			//cout << main->leksems[main->size-1]->value << " ";

		}

		if (expression[index] == '*' || expression[index] == '/' || expression[index] == '+' || expression[index] == '-')
		{
			Leksema* operation_elem = new Leksema();
			operation_elem->operation = expression[index];

			switch (expression[index])
			{
			case '*':
				operation_elem->priority = 2;
				break;
			case '/':
				operation_elem->priority = 2;
				break;
			case '-':
				operation_elem->priority = 1;
				break;
			case '+':
				operation_elem->priority = 1;
				break;
			}
			// pop elemets that higher in priority
			while (!stack_operations.isEmpty() && operation_elem->priority <= stack_operations.top()->priority)
			{
				Leksema* stack_operation = stack_operations.top();
				main->leksems[main->size++] = stack_operation;
				stack_operations.pop();
			}

			stack_operations.push(operation_elem);
		}

		if (expression[index] == '(')
		{
			Leksema* operation_elem = new Leksema();
			operation_elem->operation = "(";
			operation_elem->priority = 0;
			stack_operations.push(operation_elem);
		}

		if (expression[index] == ')')
		{
			//pop elems until we get '('
			while (!stack_operations.isEmpty() && stack_operations.top()->priority > 0)
			{
				Leksema* stack_operation = stack_operations.top();
				main->leksems[main->size++] = stack_operation;
				stack_operations.pop();
			}

			//pop '('
			stack_operations.pop();
		}

		

		index++;
	}
	//pop lefted elems
	while (!stack_operations.isEmpty())
	{
		Leksema* stack_operation = stack_operations.top();
		main->leksems[main->size++] = stack_operation;
		stack_operations.pop();
	}




	Stack <int> stack_numbers;
	int result = main->leksems[0]->value;
	
	for (int i = 0; i < main->size; i++)
	{
		if (main->leksems[i]->operation == "0")
			stack_numbers.push(main->leksems[i]->value);
		else
		{
			char operation = main->leksems[i]->operation[0];
			int number2 = stack_numbers.top();
			stack_numbers.pop();
			int number1 = stack_numbers.top();
			stack_numbers.pop();
			switch (operation)
			{
			case '*':
				result = number1 * number2;
				stack_numbers.push(result);
				break;
			case '/':
				result = number1 / number2;
				stack_numbers.push(result);
				break;
			case '-':
				result = number1 - number2;
				stack_numbers.push(result);
				break;
			case '+':
				result = number1 + number2;
				stack_numbers.push(result);
				break;
			}
		}
	}


	//expression
	cout << "Expression:" << "\n" << expression << "\n";
	//output postfix
	cout << "Reverse Polish Notation:" << "\n";
	for (int i = 0; i < main->size; ++i)
	{
		if (main->leksems[i]->operation == "0")
		{
			cout << main->leksems[i]->value << " ";
		}
		else
		{
			cout << main->leksems[i]->operation << " ";
		}
	}
	cout << "\n";

	cout << "Result:" << "\n" << result;

	return 0;
}

```
