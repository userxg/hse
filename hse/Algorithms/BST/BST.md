***Idea***: 
A Binary Search Tree is a data structure used in computer science for organizing and storing data in a sorted manner. Each node in a Binary Search Tree has at most **two children**, a left child and a right child, with the **left** child containing values **less than the parent** node and the right child containing values greater than the parent node. This hierarchical structure allows for efficient **searching**, **insertion**, and **deletion** operations on the data stored in the tree.

***Complexity***: t = teta
Search - `O(lgn)`, worst - `O(n)` or `O(h)` where h is height of a tree
Deletion - `O(lgn)`, worst - `O(n)` or `O(h)` where h is height of a tree
Insertion -`O(lgn)`, worst - `O(n)` or `O(h)` where h is height of a tree
Min,Max - `t(N)`
In,Pre,Post walk - `t(N)`

# Cormen + cpp style
***Property:***
```cpp
struct Node
{
	Node* parent;
	int key;
	Node* left; //this->key >= left->key
	Node* right; //this->key <= right->key
};

Node* root;
```
# Operations:

## MIN, MAX -
```cpp
//MIN, MAX
//Assume X is not NILL
Node* Min(Node* X) //X - root of subtree in BST
{
	while (X->left != NULL)
		X = X->left;
	return X;
}
Node* Max(Node* X)
{
	while (X->right != NULL)
		X = X->right;
	return X;
}
```

## Walks
### In-Order-Walk, Pre-Order-Walk, Post-Order-Walk
In-Order-Walk - can return sorted BST keys
```cpp
void InOrderWalk(Node* X)
{
	InOrderWalk(X->left);
	std::cout << "process: " << X->key << "\n";
	InOrderWalk(X->right);
}

void PreOrderWalk(Node* X)
{
	std::cout << "process: " << X->key << "\n";
	PreOrderWalk(X->left);
	PreOrderWalk(X->right);
}

void PostOrderWalk(Node* X)
{
	PostOrderWalk(X->left);
	PostOrderWalk(X->right);
	std::cout << "process: " << X->key << "\n";
}
```

## Search
Find Node with **key** from given X node (root of subtree)
returns Node or NILL
Search in entire BST - TreeSearch(T.root) where T is BST
```cpp
Node* TreeSearch(Node* X, int key)
{
	if (X == NULL || X->key == key)
		return X;
	if (X->key > key) 
		return TreeSearch(X->left, key);
	else 
		return TreeSearch(X->right, key);
}
```

## Predecessor & Successor
As mentioned before In-Order-Walk operation gives sort keys;
Given X we can find:
Predecessor - first node whose key goes right before X.key in sorted keys
Successor - first node whose key goes right after X.key in sorted keys
- find Min of right (left for Predecessor)
- if no right it means X node is the biggest one in some subtree, therefore we go up though the tree until root of this subtree becomes a left child
	- thus parent of that root is our Successor, because right subtree of a parent is bigger than it.
```cpp
Node* TreeSuccessor(Node* X)
{
	if (X->right != NULL) //return the smallest Node with
		return Min(X->right);  //the smallest key 
	else
	{//find the lowest ancestor of x
		Node* Y = X->parent; //whose left child is an ancestor of x
		while (Y != NULL && Y->right == X)
		{
			X = Y;
			Y = X->parent;
		}
	}
}
```

```cpp
Node* TreePredecessor(Node* X)
{
	if (X->left != NULL)
		return Min(X->left);
	else
	{
		Node* Y = X->parent;
		while (Y != NULL && Y->left == X)
		{
			X = Y;
			Y = X->parent;
		}
	}
}
```

## Tree-Insert
Insert given Node into Tree
1. find an appropriate parent for Z
2. Make Y parent Z
3. Make Z root or correct child of Y or
```cpp
void TreeInsert(Node* Z)
{
	Node* X = root_;
	Node* Y = NULL;
	while (X != NULL) //find an appropriate parent for Z
	{
		Y = X;
		if (Z->key < Y->key)
			X = X->left;
		else
			X = X->right;
	}

	Z->parent = Y; //Make Y parent Z

	if (Y == NULL) //check empty tree
		root_ = Z;
	else if (Z->key < Y->key) //make Z correct child of Y
		Y->left = Z;
	else
		Y->right = Z;
}
```
`O(lgn)`, worst - `O(n)` or `O(h)` where h is height of a tree
## Deletion
Remove Z from Tree
There 3 main cases
1. Z no has one children
	- Just remove Z from the Tree
2. Z has one child
	- elevate that child to take Z's position in the tree by modifying Z's parent to replace Z by Z's child
3. Z has both children
	 - find Successor Y of Z, because Y is minimum it doesn't have left child, but it's key still higher than Z's left child
	 - Make Y's right child as a Y's parent left child
	 - Make Z's left child as a new Y's left child 
	 - Replace Z by Y
### Transplant
Implement some subroutine for replacing node u by v
```cpp
void Transplant(Node* u, Node* v)
{
	if (u->parent == NULL) //u is root of a tree
		root_ = v;
	else if (u == u->parent->left)//find appropriate place for v
		u->parent->left = v; //v becomes left child of u's parent
	else
		u->parent->right = v;//v becomes right child of u's parent
	
	if (v != NULL)//assign u's parent to v and check if v is just empty
		v->parent = u->parent;
}
```
### Tree Delete
```cpp
void TreeDelete(Node* Z)
{
	if (Z->left == NULL) //case 1-2
		Transplant(Z, Z->right);
	else if (Z->right == NULL) //case 1-2
		Transplant(Z, Z->left);
	else
	{
		Node* Y = TreeSuccessor(Z);//find Successor
		if (Y != Z->right)//case Y is not a Z's child
		{
			Transplant(Y, Y->right); //make Y's right subtree
			//as a left Y's parent subtree

			Y->right = Z->right; //make Z's right child
			Z->right->parent = Y;//as a new Y's right child
		}
		Transplant(Z, Y);//Replace Z by Y
		Y->left = Z->left;//Make Z's left child 
		Y->left->parent = Y;//as a child of Y
	}
}
```

# Full code
```cpp
struct Node
{
	Node(Node* parent, int key, Node* left, Node* right) :
		parent(parent), key(key), left(left), right(right) {}
	Node* parent;
	int key;
	Node* left;
	Node* right;
};

class BST
{
private:

	Node* root_;
public:

	BST(): root_(NULL) {}
	BST(Node* X) : root_(X) {}

	
	Node* Min(Node* X) 
	{
		while (X->left != NULL)
			X = X->left;
		return X;
	}
	Node* Max(Node* X)
	{
		while (X->right != NULL)
			X = X->right;
		return X;
	}


	void InOrderWalk(Node* X)
	{
		InOrderWalk(X->left);
		std::cout << "process: " << X->key << "\n";
		InOrderWalk(X->right);
	}

	void PreOrderWalk(Node* X)
	{
		std::cout << "process: " << X->key << "\n";
		PreOrderWalk(X->left);
		PreOrderWalk(X->right);
	}

	void PostOrderWalk(Node* X)
	{
		PostOrderWalk(X->left);
		PostOrderWalk(X->right);
		std::cout << "process: " << X->key << "\n";
	}

	Node* TreeSearch(Node* X, int key)
	{
		if (X == NULL || X->key == key)
			return X;
		if (X->key > key) 
			return TreeSearch(X->left, key);
		else 
			return TreeSearch(X->right, key);
	}

	Node* TreeSuccessor(Node* X)
	{
		if (X->right != NULL) 
			return Min(X->right);  
		else
		{
			Node* Y = X->parent;
			while (Y != NULL && Y->right == X)//
			{
				X = Y;
				Y = X->parent;
			}
		}
	}

	Node* TreePredecessor(Node* X)
	{
		if (X->left != NULL)
			return Min(X->left);
		else
		{
			Node* Y = X->parent;
			while (Y != NULL && Y->left == X)
			{
				X = Y;
				Y = X->parent;
			}
		}
	}

	void TreeInsert(Node* Z)
	{
		Node* X = root_;
		Node* Y = NULL;
		while (X != NULL) 
		{
			Y = X;
			if (Z->key < Y->key)
				X = X->left;
			else
				X = X->right;
		}

		Z->parent = Y; 

		if (Y == NULL) 
			root_ = Z;
		else if (Z->key < Y->key) 
			Y->left = Z;
		else
			Y->right = Z;
	}

	void Transplant(Node* u, Node* v)
	{
		if (u->parent == NULL)
			root_ = v;
		else if (u == u->parent->left)
			u->parent->left = v;
		else
			u->parent->right = v;
		
		if (v != NULL)
			v->parent = u->parent;
	}

	void TreeDelete(Node* Z)
	{
		if (Z->left == NULL)
			Transplant(Z, Z->right);
		else if (Z->right == NULL)
			Transplant(Z, Z->left);
		else
		{
			Node* Y = TreeSuccessor(Z);
			if (Y != Z->right)
			{
				Transplant(Y, Y->right);

				Y->right = Z->right;
				Z->right->parent = Y;
			}
			Transplant(Z, Y);
			Y->left = Z->left;
			Y->left->parent = Y;
		}
	}
};
int main()
{
	BST bst;
	std::vector<Node*> Nodes =
	{
		new Node(NULL, 10, NULL, NULL),
		new Node(NULL, 5, NULL, NULL),
		new Node(NULL, 15, NULL, NULL)
	};

	for (auto& node : Nodes)
		bst.TreeInsert(node);
	bst.TreeDelete(Nodes[2]);

	for (auto& node : Nodes)
		delete node;
	return 0;
}
```