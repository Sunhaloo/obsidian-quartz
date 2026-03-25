---
id: Python - Binary Search Tree
aliases: Binary Search Tree implemented using Classes
tags:
  - data-structures
  - oop
  - python
  - binary-tree
author: S.Sunhaloo
date: 2026-03-23
status: Completed
---

## List of Contents

- [[#Creation Of Class Node]]
- [[#Creation Of Binary Search Tree Class]]
- [[#Function / Method Related To Binary Search Tree]]
	- [[#Data Insertion Methods]]
		- [[#Insert Method]]
	- [[#Search Methods]]
		- [[#Contains Dunder Method]]
		- [[#Search Method]]
	- [[#Data Removal Methods]]
		- [[#Successor Private Method]]
		- [[#Predecessor Private Method]]
		- [[#Private Delete Method]]
		- [[#Delete Method]]
	- [[#Traversal Methods]]
		- [[#Private In-Order Traversal]]
		- [[#Private Pre-Order Traversal]]
		- [[#Private Post-Order Traversal]]
		- [[#Traverse Method]]
	- [[#Miscellaneous Methods]]
		- [[#Iteration Dunder Method]]
		- [[#Representation Dunder Method]]
- [[#Creation Of Binary Search Tree and Usage]]

---

> [!NOTE]
> This is note is only going to show about the implementation of the **binary search tree** *data structure* using Python classes.
> 
> Please refer to online resources or even use Large Language Models to learn more about 'Binary Search Tree ( BST )'.

> [!WARNING]
> As you know by now, in Python there are **no strict** ways to enforce '*private*' methods like in other programming languages such as [[Java Data View | Java Data View]].
> 
> Therefore, how can we *have* **private methods** in this codebase?
> 
> Therefore, we do a little **gentleman's agreement** whereby, if we write a function / method that starts with and `_` character. For example, `_some_method` or `_helper_function`...
> 
> We as **programmers** are going to agree that we **won't** use this method *outside* the **current** `class`. Therefore, this is the reason as to why we "*can*" have **private methods** in Python!

---

> [!INFO] Resource(s)
> - Neural Nine: https://www.youtube.com/watch?v=a0_3vaBUW_s
> - My Notes: [[Trees and Binary Trees]]
> - Python Generators ( *I don't know about this - need to learn it one day* ):
> 	- Bro Code: https://www.youtube.com/watch?v=G1lJeEIl05o
> 	- Official Documentation: https://docs.python.org/3/reference/simple_stmts.html
> 	- b001: https://www.youtube.com/watch?v=HnggP09mKpM
> 	- Neural Nine: https://www.youtube.com/watch?v=byhiRuoSQzA
> 	- StackOverflow: https://stackoverflow.com/questions/7362900/behaviour-of-pythons-yield
> 	- Medium Article: https://ntsh-vicky.medium.com/basic-of-python-generators-895990675d15

# Creation Of Class Node

Below you are going to find the *class* implementation of a **node**.

```python
# our binary search tree's nodes
class Node:
    # our constructor
    def __init__(self, key):
        # define the pointers ( pointers that point to nodes below )
        self.left = None
        self.right = None

        # define the pointer ( pointers that point to node above )
        self.parent = None

        # define the key for the current node
        # INFO: the `key` is used for searching and insertion
        self.key = key

        # define the "actual" value for the current node
        self.value = None

    # dunder method to be able to display the node
    def __repr__(self):
        return f"({self.key}, {self.value})"
```

- Therefore to **create** some *nodes*, we can simply create our objects of class `Node`:

```python
# our main function
def main():
    # create our first ever binary search tree ( root ) node
    # NOTE: add this point in time, we only have the `key` supplied to `root_node`
    root_node: Node = Node(1)

    # set the value for the `root_node`
    root_node.value = "Root Node"

    # display the first / root node
    print(root_node)

    # create the first left and right parent node
    # WARNING: I have not yet linked anything ==> this is just to show creation
    first_left_node = Node(1)
    first_right_node = Node(2)

    # give / specify values for both the first left and right parent node
    first_left_node.value = ["I", "am", "the", "first", "parent", "node"]
    first_right_node.value = 27

    # display the left and right parent node
    print(first_left_node)
    print(first_right_node)


# source the main function
if __name__ == "__main__":
    main()
```

> [!NOTE] Should The Key Be The Value?
> 
> So, if you go around the internet and [Google](https://google.com) around. You are going to see that there are binary trees with nodes that has a **number** *inside* a **circle**.
> 
> But in above `Node` class, we see the we are passing the `key` but inside the code, we **don't** see this:
> 
> ```python
> # we DON'T see this
> self.key = value
> ```
> 
> - Instead we see something like this; this is my *lecturer's* code:
> 
> ```python
> def __init__(self, key):
>	self.value = key  
>	self.left = None  
>	self.right = None
> ```
> 
> > Yes, that's everything my lecturer wrote compared to Neural Nine's code!
> 
> Here, you could say that the code given by my **lecturer** is the *same* as the drawing of binary ( search ) trees whereby we have a **number** *inside* a **circle**.
> 
> But compared to the above code, we see that we have a specific `self.key` variable and `self.value` variable.
> 
> You could think of this as a [[Python - Dictionaries | dictionary]] whereby the *value* has an associated **key**.
> 
> Therefore, when we are going to do *insertion*, *deletion* and *searching* of **data**... Its going, to be more "*concrete*"!
> 
> > [!TIP] Summary
> > - Lecturer's implementation is **conceptual** and used to make people *understand* the code while "*our's*" is a **production-grade** code
> > - With the lecturer's `Node` implementation, you are **not** going to be able to hold *multiple* **data types** in your Binary Search Tree
> > 	- This is due to the lack of `self.key = key`!
> 
> > I mean, you can see how the its just *a* `Node` and I think a node **should** be able to *hold* **any** data types!

# Creation Of Binary Search Tree Class

Here is how we are going to create the actual 'Binary Search Tree' data structure.

```python
# our binary search tree class / data structure ==> "linking" our `Node`
class BinarySearchTree:
    # the constructor for the binary search tree class
    def __init__(self):
        # INFO: initially the 'BST' data structure is empty
        self.root = None
```

- Therefore, to create an **empty** binary search tree, we can simply create an *object* of the `BinarySearchTree` class:

```python
# our main function
def main():
    # create object of type `BinarySearchTree` to initialise our linked list
    my_binary_search_tree: BinarySearchTree = BinarySearchTree()


# source the main function
if __name__ == "__main__":
    main()
```

---

# Function / Method Related To Binary Search Tree

## Data Insertion Methods

### Insert Method

```python
# insert method to insert data into binary search tree ( based on nodes )
def insert(self, key, value):
	# check if the "root" node has data or not
	if self.root is None:
		# create the actual `Node` and supply the `key`
		self.root = Node(key)
		# specify the actual value to go with the node-key pair
		self.root.value = value

	# if the "root" node is not empty
	else:
		# always start from the "root" node
		current_node = self.root

		# iterate through the binary tree indefinitely until `None` found
		while True:
			# if the search key is less than the current node's key
			if key < current_node.key:
				# check if we have reached the left node and there is no more
				if current_node.left is None:
					# create the actual `Node` and supply the `key`
					current_node.left = Node(key)
					# specify the actual value to go with the node-key pair
					current_node.left.value = value
					current_node.left.parent = current_node

					# simply `break` from the `while` loop
					break

				# if we do have more nodes down below
				else:
					current_node = current_node.left

			# if the search key is greater than the current node's key
			elif key > current_node.key:
				# check if we have reached the right node and there is no more
				if current_node.right is None:
					# create the actual `Node` and supply the `key`
					current_node.right = Node(key)
					# specify the actual value to go with the node-key pair
					current_node.right.value = value
					current_node.right.parent = current_node

					# simply `break` from the `while` loop
					break

				# if we do have more nodes down below
				else:
					current_node = current_node.right

			# if the `key` needs to be "updated" with new values
			else:
				# simply change the value at that `Node`
				current_node.value = value

				# simply `break` from the `while` loop
				break
```

> [!TIP]- Time Complexity = O(Height of Tree)
> - The **overall** *running* time complexity for this method is going to be O(*height of tree*)
> - **Best** Case: O(1)
> 	- Occurs when the we have *nothing* at the **root**
> - **Average** Case: O(log n)
> 	- Occurs when the binary search tree is a **balanced tree**
> 	- Each *step* **eliminates** *half* of remaining nodes
> - **Worst** Case: O(n)
> 	- Occurs if data is inserted in **sorted** manner; creating a *linear tree*

## Search Methods

### Contains Dunder Method

```python
# dunder method to check if a node is present or not through `key`
def __contains__(self, key) -> bool:
	# always start from the "root" node
	current_node = self.root

	# iterate through the binary tree indefinitely until `Node` found
	while current_node is not None:
		# if the search key is less than the current node's key
		if key < current_node.key:
			# update the current node to the node "below"
			current_node = current_node.left

		# if the search key is greater than the current node's key
		elif key > current_node.key:
			# update the current node to the node "below"
			current_node = current_node.right

		else:
			# if we find the `key` ==> exit the `while` loop
			return True

	# if we did not find the `key`
	return False
```

> [!TIP]- Time Complexity = O(Height of Tree)
> - The **overall** *running* time complexity for this method is going to be O(*height of tree*)
> - **Best** Case: O(1)
> 	- Occurs when the we have *nothing* at the **root** or `key` is at the **root**
> - **Average** Case: O(log n)
> 	- Occurs when the binary search tree is a **balanced tree**
> - **Worst** Case: O(n)
> 	- Basically if the binary search tree *becomes* a [[Python - Singly Linked Lists | linked list]]
> 	- This means that we have a long "*left*" or "*right*" line of nodes!

### Search Method

```python
# search method to search for the actual `Node`
def search(self, key):
	# always start from the "root" node
	current_node = self.root

	# iterate through the binary tree indefinitely until `Node` found
	while True:
		# check if the current / "root" node is "empty" or the key itself
		if current_node is None or current_node.key == key:
			# simply return the "root" node itself
			return current_node

		# if the search key is less than the current node's key
		elif key < current_node.key:
			# check if we have reached leaf node else return the proper node
			if current_node.left is None:
				return None

			else:
				current_node = current_node.left

		# if the search key is greater than the current node's key
		else:
			# check if we have reached leaf node else return the proper node
			if current_node.right is None:
				return None

			else:
				current_node = current_node.right
```

> [!TIP]- Time Complexity = O(Height of Tree)
> - The **overall** *running* time complexity for this method is going to be O(*height of tree*)
> - **Best** Case: O(1)
> 	- Occurs when the we have *nothing* at the **root** or `key` is at the **root**
> - **Average** Case: O(log n)
> 	- Occurs when the binary search tree is a **balanced tree**
> - **Worst** Case: O(n)
> 	- Basically if the binary search tree *becomes* a [[Python - Singly Linked Lists | linked list]]
> 	- This means that we have a long "*left*" or "*right*" line of nodes!

## Data Removal Methods

### Successor Private Method

```python
# "private" method that finds the ( in-order ) successor of a node
# first moves to the right then keep staying left
def _successor(self, node: Node):
	# check if the node exists before proceding with search
	if node is None:
		raise ValueError("\n\t<< Successor Could NOT Be Found!!! >>\n")

	# check if the right side of node has data or not
	if node.right is None:
		return None

	else:
		# TIP: move one time to the right then move only on the left sub-tree
		
		# get the current node ==> move to that right node
		current_node = node.right

		# iterate through the left side of each node that comes after
		while current_node.left is not None:
			current_node = current_node.left

		# finaly return the current node
		return current_node
```

> [!TIP]- Time Complexity = O(Height of Tree)
> - The **overall** *running* time complexity for this method is going to be O(*height of tree*)
> - **Best** Case: O(1)
> 	- Occurs when the node has **no** *right* **child** or **no** *left* **sub-tree**
> - **Average** Case: O(log n)
> 	- Occurs when the binary search tree is a **balanced tree**
> - **Worst** Case: O(n)
> 	- Basically if the binary search tree *becomes* a [[Python - Singly Linked Lists | linked list]]
> 	- This means that we have a long "*left*" or "*right*" line of nodes!

### Predecessor Private Method

> [!NOTE]
> Even though that we did **not** use this *method* in any place at all during this implementation of the 'Binary Search Tree'.
> 
> I think that this is the best place to add the `_predecessor` here as we have the `_successor` just above.

```python
# "private" method that finds the ( in-order ) predecessor of a node
# first moves to the left then keep staying right
def _predecessor(self, node: Node):
	# check if the node exists before proceding with search
	if node is None:
		raise ValueError("\n\t<< Predecessor Could NOT Be Found!!! >>\n")

	# check if the left side of node has data or not
	if node.left is None:
		return None

	else:
		# TIP: move one time to the left then move only on the right sub-tree
		
		# get the current node ==> move to that left node
		current_node = node.left

		# iterate through the left side of each node that comes after
		while current_node.right is not None:
			current_node = current_node.right

		# finaly return the current node
		return current_node
```

> [!TIP]- Time Complexity = O(Height of Tree)
> - The **overall** *running* time complexity for this method is going to be O(*height of tree*)
> - **Best** Case: O(1)
> 	- Occurs when the node has **no** *left* **child** or **no** *right* **sub-tree**
> - **Average** Case: O(log n)
> 	- Occurs when the binary search tree is a **balanced tree**
> - **Worst** Case: O(n)
> 	- Basically if the binary search tree *becomes* a [[Python - Singly Linked Lists | linked list]]
> 	- This means that we have a long "*left*" or "*right*" line of nodes!

### Private Delete Method

```python
# "private" method to be able to delete and "re-link" nodes ( if need be )
def _delete(self, node: Node):
	# first condition ==> node is a leaf node
	if node.left is None and node.right is None:
		# check if we are the "root" node
		if node.parent is None:
			# "delete" the value from the root node
			# WARNING: from what I can see, we are not actually deleting
			# I think we are just breaking the binary search tree and therefore
			# let Python's garbage collector do the work for us
			self.root = None

		# if the node is NOT the "root" node
		else:
			# check if the "current" node's parent is located
			if node.parent.right == node:
				node.parent.right = None

			else:
				node.parent.left = None

			# "delete" the parent node and make sure that we have no references
			node.parent = None

	# second condition ==> if ( parent ) node has one child node
	elif node.left is None or node.right is None:
		# check where the child node is located ==> cool one liner
		child_node = node.left if node.left is not None else node.right

		# check if the "current" node is the "root" node
		if node.parent is None:
			# NOTE: happens if "root" node has only 1 child node ( in this case )
			# make the child node become the root node
			child_node.parent = None
			self.root = child_node

		# if the "current" node is not the "root" node
		else:
			# check if the node that we are trying to delete has a parent
			# INFO: this means that the `child_node` can either be to the left / right
			if node.parent.right == node:
				node.parent.right = child_node

			else:
				node.parent.left = child_node

			# re-link the child's parent to the actual node's parent
			child_node.parent = node.parent

		# finally, cut all the "in-between" of the connections
		node.parent = node.left = node.right = None

	# third condition ==> if ( parent ) node has two child node
	else:
		# call the successor function to find smallest node is right sub-tree
		successor = self._successor(node)

		# copy the data from successor to the actual node
		node.key = successor.key
		node.value = successor.value

		# delete the "other" successor node ==> either 0 or 1 child
		# INFO: this basically either triggers first / second condition
		self.delete(successor)
```

> [!TIP]- Time Complexity = O(Height of Tree)
> - The **overall** *running* time complexity for this method is going to be O(*height of tree*)
> - **Best** Case: O(1)
> 	- Occurs when the node to be *deleted* if found at the **root** or its the **left** node ( *i.e, the only node is the tree* )
> - **Average** Case: O(log n)
> 	- Occurs when the binary search tree is a **balanced tree**
> - **Worst** Case: O(n)
> 	- Basically if the binary search tree *becomes* a [[Python - Singly Linked Lists | linked list]]
> 	- This means that we have a long "*left*" or "*right*" line of nodes!

### Delete Method

```python
# delete method to search for a key and calls `_delete` "private" method
def delete(self, key):
	# intialise a node that is going to be the `Node` variable after searching
	node = self.search(key)

	# check if the node "returned" has data or not
	if node is None:
		# meaning that the node with key `key` is not available
		raise KeyError("\n\t<< Key Does NOT Exists!!! >>\n")

	# else if we have data inside `node`
	# ==> call "private" method to delete and "re-link" nodes ( if need be )
	self._delete(node)
```

> [!TIP]- Time Complexity = O(Height of Tree)
> - The **overall** *running* time complexity for this method is going to be O(*height of tree*)
> - **Best** Case: O(1)
> 	- Occurs if the tree has a **single** node and its the one ( *key* ) that you are **deleting**
> - **Average** Case: O(log n)
> 	- Occurs when the binary search tree is a **balanced tree**
> - **Worst** Case: O(n)
> 	- Basically if the binary search tree *becomes* a [[Python - Singly Linked Lists | linked list]]
> 	- This means that we have a long "*left*" or "*right*" line of nodes!

---

> [!INFO]
> Given that this is Python and we **don't** have to declare things. Therefore, we **don't** really care if we implement the `_delete` *first* and the `delete` method *second* or *vice-versa*.
> 
> I think in a **compiled** programming language we would have to do code this differently because **each** of them calls each other and in a compiled programming language... Maybe we would have to first *just* **declare** these functions so that the *compiler* or the *[preprecessor](https://en.wikipedia.org/wiki/Preprocessor)*

---

## Traversal Methods

### Private In-Order Traversal

```python
# "private" method that traverses the tree "in-order"
def _in_order_traversal(self, node):
	# TIP: left node --> root node --> right node
	# check if the node has data or not
	if node is not None:
		# pause the function and "exhaust" entire left sub-tree first
		yield from self._in_order_traversal(node.left)

		# actually get the value as a tuple
		yield (node.key, node.value)

		# pause the function and "exhaust" entire right sub-tree second
		yield from self._in_order_traversal(node.right)
```

> [!TIP]- Time Complexity = O(n)
> - The **overall** *running* time complexity for this method is going to be O(n) ( *where $n$ is the total nodes in tree* )
> - **Best** Case: O(n)
> 	- Occurs when you have to *visit* **every** single *node* found in the tree and there is **no** *early exit*
> - **Average** Case: O(n)
> 	- Occurs when the binary search tree is a **balanced tree**
> - **Worst** Case: O(n)
> 	- Basically if the binary search tree *becomes* a [[Python - Singly Linked Lists | linked list]]
> 	- This means that we have a long "*left*" or "*right*" line of nodes!

### Private Pre-Order Traversal

```python
# "private" method that traverses the tree "pre-order"
def _pre_order_traversal(self, node):
	# TIP: root node --> left node --> right node
	# check if the node has data or not
	if node is not None:
		# actually get the value as a tuple
		yield (node.key, node.value)

		# pause the function and "exhaust" entire left sub-tree first
		yield from self._pre_order_traversal(node.left)

		# pause the function and "exhaust" entire right sub-tree second
		yield from self._pre_order_traversal(node.right)
```

> [!TIP]- Time Complexity = O(n)
> - The **overall** *running* time complexity for this method is going to be O(n) ( *where $n$ is the total nodes in tree* )
> - **Best** Case: O(n)
> 	- Occurs when you have to *visit* **every** single *node* found in the tree and there is **no** *early exit*
> - **Average** Case: O(n)
> 	- Occurs when the binary search tree is a **balanced tree**
> - **Worst** Case: O(n)
> 	- Basically if the binary search tree *becomes* a [[Python - Singly Linked Lists | linked list]]
> 	- This means that we have a long "*left*" or "*right*" line of nodes!

### Private Post-Order Traversal

```python
# "private" method that traverses the tree "post-order"
def _post_order_traversal(self, node):
	# TIP: left node --> right node --> root node
	# check if the node has data or not
	if node is not None:
		# pause the function and "exhaust" entire left sub-tree first
		yield from self._post_order_traversal(node.left)

		# pause the function and "exhaust" entire right sub-tree second
		yield from self._post_order_traversal(node.right)

		# actually get the value as a tuple
		yield (node.key, node.value)
```

> [!TIP]- Time Complexity = O(n)
> - The **overall** *running* time complexity for this method is going to be O(n) ( *where $n$ is the total nodes in tree* )
> - **Best** Case: O(n)
> 	- Occurs when you have to *visit* **every** single *node* found in the tree and there is **no** *early exit*
> - **Average** Case: O(n)
> 	- Occurs when the binary search tree is a **balanced tree**
> - **Worst** Case: O(n)
> 	- Basically if the binary search tree *becomes* a [[Python - Singly Linked Lists | linked list]]
> 	- This means that we have a long "*left*" or "*right*" line of nodes!

### Traverse Method

```python
# traverse method to traverse the binary search tree in different ways
def traverse(self, order: str):
	# check what type of traversal we want
	if order == "in-order":
		# pause the function and traverse the tree in order of "in-order"
		yield from self._in_order_traversal(self.root)

	elif order == "pre-order":
		# pause the function and traverse the tree in order of "pre-order"
		yield from self._pre_order_traversal(self.root)

	elif order == "post-order":
		# pause the function and traverse the tree in order of "post-order"
		yield from self._post_order_traversal(self.root)

	# if user entered a traversal method that does not exists
	else:
		raise ValueError("\n\t << Unknown Order Entered!!! >>\n")
```

> [!TIP]- Time Complexity = O(n)
> - The **overall** *running* time complexity for this method is going to be O(n) ( *where $n$ is the total nodes in tree* )
> - **Best** Case: O(n)
> 	- Occurs when you have to *visit* **every** single *node* found in the tree and there is **no** *early exit*
> - **Average** Case: O(n)
> 	- Occurs when the binary search tree is a **balanced tree**
> - **Worst** Case: O(n)
> 	- Basically if the binary search tree *becomes* a [[Python - Singly Linked Lists | linked list]]
> 	- This means that we have a long "*left*" or "*right*" line of nodes!

## Miscellaneous Methods

### Iteration Dunder Method

```python
# dunder method to be able to iterate through the binary search tree
def __iter__(self):
	# pause the function and get the nodes in sorted manner
	yield from self._in_order_traversal(self.root)
```

> [!TIP]- Time Complexity = O(n)
> - The **overall** *running* time complexity for this method is going to be O(n)
> - Best Case: O(n)
> - Worst Case: O(n)

### Representation Dunder Method

```python
# dunder method to be able to display the node
def __repr__(self):
	# iterate through binary search tree in order, convert to list, then to string
	return str(list(self._in_order_traversal(self.root)))
```

> [!TIP]- Time Complexity = O(n)
> - The **overall** *running* time complexity for this method is going to be O(n)
> - Best Case: O(n)
> - Worst Case: O(n)

# Creation Of Binary Search Tree and Usage

## Actual Code

> [!NOTE]
> Compared to our lecturer's binary tree whereby it would technically only support `int`eger numbers.
> 
> Our code does really behave like a *proper* binary search tree as we are able to store **any** *type of data*.
> 
> But because I lack creativity and other things... I just decided to use Formula 1 driver's names!
> 
> > What I am trying to say is that... This 'Binary Search Tree' is good and can handle **any** *type of data*!

```python
# our binary search tree's nodes
class Node:
    # our constructor
    def __init__(self, key):
        # define the pointers ( pointers that point to nodes below )
        self.left = None
        self.right = None

        # define the pointer ( pointers that point to node above )
        self.parent = None

        # define the key for the current node
        # INFO: the `key` is used for searching and insertion
        self.key = key

        # define the "actual" value for the current node
        self.value = None

    # dunder method to be able to display the node
    def __repr__(self):
        return f"({self.key}, {self.value})"


# our binary search tree class / data structure ==> "linking" our `Node`
class BinarySearchTree:
    # the constructor for the binary search tree class
    def __init__(self):
        # INFO: initially the 'BST' data structure is empty
        self.root = None

    # insert method to insert data into binary search tree ( based on nodes )
    def insert(self, key, value):
        # check if the "root" node has data or not
        if self.root is None:
            # create the actual `Node` and supply the `key`
            self.root = Node(key)
            # specify the actual value to go with the node-key pair
            self.root.value = value

        # if the "root" node is not empty
        else:
            # always start from the "root" node
            current_node = self.root

            # iterate through the binary tree indefinitely until `None` found
            while True:
                # if the search key is less than the current node's key
                if key < current_node.key:
                    # check if we have reached the left node and there is no more
                    if current_node.left is None:
                        # create the actual `Node` and supply the `key`
                        current_node.left = Node(key)
                        # specify the actual value to go with the node-key pair
                        current_node.left.value = value
                        current_node.left.parent = current_node

                        # simply `break` from the `while` loop
                        break

                    # if we do have more nodes down below
                    else:
                        current_node = current_node.left

                # if the search key is greater than the current node's key
                elif key > current_node.key:
                    # check if we have reached the right node and there is no more
                    if current_node.right is None:
                        # create the actual `Node` and supply the `key`
                        current_node.right = Node(key)
                        # specify the actual value to go with the node-key pair
                        current_node.right.value = value
                        current_node.right.parent = current_node

                        # simply `break` from the `while` loop
                        break

                    # if we do have more nodes down below
                    else:
                        current_node = current_node.right

                # if the `key` needs to be "updated" with new values
                else:
                    # simply change the value at that `Node`
                    current_node.value = value

                    # simply `break` from the `while` loop
                    break

    # dunder method to check if a node is present or not through `key`
    def __contains__(self, key) -> bool:
        # always start from the "root" node
        current_node = self.root

        # iterate through the binary tree indefinitely until `Node` found
        while current_node is not None:
            # if the search key is less than the current node's key
            if key < current_node.key:
                # update the current node to the node "below"
                current_node = current_node.left

            # if the search key is greater than the current node's key
            elif key > current_node.key:
                # update the current node to the node "below"
                current_node = current_node.right

            else:
                # if we find the `key` ==> exit the `while` loop
                return True

        # if we did not find the `key`
        return False

    # search method to search for the actual `Node`
    def search(self, key):
        # always start from the "root" node
        current_node = self.root

        # iterate through the binary tree indefinitely until `Node` found
        while True:
            # check if the current / "root" node is "empty" or the key itself
            if current_node is None or current_node.key == key:
                # simply return the "root" node itself
                return current_node

            # if the search key is less than the current node's key
            elif key < current_node.key:
                # check if we have reached leaf node else return the proper node
                if current_node.left is None:
                    return None

                else:
                    current_node = current_node.left

            # if the search key is greater than the current node's key
            else:
                # check if we have reached leaf node else return the proper node
                if current_node.right is None:
                    return None

                else:
                    current_node = current_node.right

    # "private" method that finds the ( in-order ) successor of a node
    # first moves to the right then keep staying left
    def _successor(self, node: Node):
        # check if the node exists before proceding with search
        if node is None:
            raise ValueError("\n\t<< Successor Could NOT Be Found!!! >>\n")

        # check if the right side of node has data or not
        if node.right is None:
            return None

        else:
            # TIP: move one time to the right then move only on the left sub-tree

            # get the current node ==> move to that right node
            current_node = node.right

            # iterate through the left side of each node that comes after
            while current_node.left is not None:
                current_node = current_node.left

            # finaly return the current node
            return current_node

    # "private" method that finds the ( in-order ) predecessor of a node
    # first moves to the left then keep staying right
    def _predecessor(self, node: Node):
        # check if the node exists before proceding with search
        if node is None:
            raise ValueError("\n\t<< Predecessor Could NOT Be Found!!! >>\n")

        # check if the left side of node has data or not
        if node.left is None:
            return None

        else:
            # TIP: move one time to the left then move only on the right sub-tree

            # get the current node ==> move to that left node
            current_node = node.left

            # iterate through the left side of each node that comes after
            while current_node.right is not None:
                current_node = current_node.right

            # finaly return the current node
            return current_node

    # "private" method to be able to delete and "re-link" nodes ( if need be )
    def _delete(self, node: Node):
        # first condition ==> node is a leaf node
        if node.left is None and node.right is None:
            # check if we are the "root" node
            if node.parent is None:
                # "delete" the value from the root node
                # WARNING: from what I can see, we are not actually deleting
                # I think we are just breaking the binary search tree and therefore
                # let Python's garbage collector do the work for us
                self.root = None

            # if the node is NOT the "root" node
            else:
                # check if the "current" node's parent is located
                if node.parent.right == node:
                    node.parent.right = None

                else:
                    node.parent.left = None

                # "delete" the parent node and make sure that we have no references
                node.parent = None

        # second condition ==> if ( parent ) node has one child node
        elif node.left is None or node.right is None:
            # check where the child node is located ==> cool one liner
            child_node = node.left if node.left is not None else node.right

            # check if the "current" node is the "root" node
            if node.parent is None:
                # NOTE: happens if "root" node has only 1 child node ( in this case )
                # make the child node become the root node
                child_node.parent = None
                self.root = child_node

            # if the "current" node is not the "root" node
            else:
                # check if the node that we are trying to delete has a parent
                # INFO: this means that the `child_node` can either be to the left / right
                if node.parent.right == node:
                    node.parent.right = child_node

                else:
                    node.parent.left = child_node

                # re-link the child's parent to the actual node's parent
                child_node.parent = node.parent

            # finally, cut all the "in-between" of the connections
            node.parent = node.left = node.right = None

        # third condition ==> if ( parent ) node has two child node
        else:
            # call the successor function to find smallest node is right sub-tree
            successor = self._successor(node)

            # copy the data from successor to the actual node
            node.key = successor.key
            node.value = successor.value

            # delete the "other" successor node ==> either 0 or 1 child
            # INFO: this basically either triggers first / second condition
            self.delete(successor)

    # delete method to search for a key and calls `_delete` "private" method
    def delete(self, key):
        # intialise a node that is going to be the `Node` variable after searching
        node = self.search(key)

        # check if the node "returned" has data or not
        if node is None:
            # meaning that the node with key `key` is not available
            raise KeyError("\n\t<< Key Does NOT Exists!!! >>\n")

        # else if we have data inside `node`
        # ==> call "private" method to delete and "re-link" nodes ( if need be )
        self._delete(node)

    # "private" method that traverses the tree "in-order"
    def _in_order_traversal(self, node):
        # TIP: left node --> root node --> right node
        # check if the node has data or not
        if node is not None:
            # pause the function and "exhaust" entire left sub-tree first
            yield from self._in_order_traversal(node.left)

            # actually get the value as a tuple
            yield (node.key, node.value)

            # pause the function and "exhaust" entire right sub-tree second
            yield from self._in_order_traversal(node.right)

    # "private" method that traverses the tree "pre-order"
    def _pre_order_traversal(self, node):
        # TIP: root node --> left node --> right node
        # check if the node has data or not
        if node is not None:
            # actually get the value as a tuple
            yield (node.key, node.value)

            # pause the function and "exhaust" entire left sub-tree first
            yield from self._pre_order_traversal(node.left)

            # pause the function and "exhaust" entire right sub-tree second
            yield from self._pre_order_traversal(node.right)

    # "private" method that traverses the tree "post-order"
    def _post_order_traversal(self, node):
        # TIP: left node --> right node --> root node
        # check if the node has data or not
        if node is not None:
            # pause the function and "exhaust" entire left sub-tree first
            yield from self._post_order_traversal(node.left)

            # pause the function and "exhaust" entire right sub-tree second
            yield from self._post_order_traversal(node.right)

            # actually get the value as a tuple
            yield (node.key, node.value)

    # traverse method to traverse the binary search tree in different ways
    def traverse(self, order: str):
        # check what type of traversal we want
        if order == "in-order":
            # pause the function and traverse the tree in order of "in-order"
            yield from self._in_order_traversal(self.root)

        elif order == "pre-order":
            # pause the function and traverse the tree in order of "pre-order"
            yield from self._pre_order_traversal(self.root)

        elif order == "post-order":
            # pause the function and traverse the tree in order of "post-order"
            yield from self._post_order_traversal(self.root)

        # if user entered a traversal method that does not exists
        else:
            raise ValueError("\n\t << Unknown Order Entered!!! >>\n")

    # dunder method to be able to iterate through the binary search tree
    def __iter__(self):
        # pause the function and get the nodes in sorted manner
        yield from self._in_order_traversal(self.root)

    # dunder method to be able to display the node
    def __repr__(self):
        # iterate through binary search tree in order, convert to list, then to string
        return str(list(self._in_order_traversal(self.root)))


# our main function
def main():
    # create object of type `BinarySearchTree` to initialise our linked list
    my_binary_search_tree: BinarySearchTree = BinarySearchTree()

    # insert data using the `insert` method into the binary search tree
    my_binary_search_tree.insert(27, "Aryton Senna")
    my_binary_search_tree.insert(44, "Lewis Hamilton")
    my_binary_search_tree.insert(5, "Sebastien Vettel")
    my_binary_search_tree.insert(33, "Max Verstappen")
    my_binary_search_tree.insert(7, "Kimi Raikonnen")
    my_binary_search_tree.insert(77, "Valteri Bottas")
    my_binary_search_tree.insert(16, "Charles Leclerc")
    my_binary_search_tree.insert(4, "Lando Shitter Norris")

    print("\n\t -- After Insertion --\n")

    # display the binary search tree directly
    # NOTE: displaying using the `__repr__` dunder method ==> 'in-order'
    print(my_binary_search_tree)

    print("\n\t -- In-Order Traversal --\n")

    # display the binary search tree while traversing through it
    # NOTE: traversing using 'in-order' method
    for node in my_binary_search_tree.traverse("in-order"):
        print(node)

    print("\n\t -- Pre-Order Traversal --\n")

    # display the binary search tree while traversing through it
    # NOTE: traversing using 'pre-order' method
    for node in my_binary_search_tree.traverse("pre-order"):
        print(node)

    print("\n\t -- Post-Order Traversal --\n")

    # display the binary search tree while traversing through it
    # NOTE: traversing using 'post-order' method
    for node in my_binary_search_tree.traverse("post-order"):
        print(node)

    # delete some nodes from the binary search tree
    my_binary_search_tree.delete(4)
    my_binary_search_tree.delete(7)
    my_binary_search_tree.delete(5)

    print("\n\t -- After Deletion --\n")

    # display binary search tree after some deletion
    print(my_binary_search_tree)

    # search for a key
    # INFO: searching for a key that exists else program would top as it hits error
    print(f"Node with key '77' data: {my_binary_search_tree.search(77)}")


# source the main function
if __name__ == "__main__":
    main()
```

---

# Socials

- **GitHub**: https://www.github.com/Sunhaloo
- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo

---

S.Sunhaloo
Thank You!