---
id: Python - Singly Linked Lists
aliases: Implementation of Singly Linked Lists in Python
tags:
  - data-structures
  - lists
  - oop
  - python
author: S.Sunhaloo
date: 2025-09-16
status: Completed
---

## List of Contents

- [[#Creation Of Class Node]]
- [[#Creation Of Linked List Class]]
- [[#Function / Method Related To Linked List]]
	- [[#Data Insertion Methods]]
		- [[#Insert At The Start - Prepend Method]]
		- [[#Insert At The End - Append Method]]
		- [[#Insert At Any Position Using Index - Insert Method]]
		- [[#Insert In Orderly Manner - Insert Ordered Method]]
	- [[#Data Removal Methods]]
		- [[#Delete At The Start - Delete Head Method]]
		- [[#Delete At The End - Pop Method]]
		- [[#Delete At Any Position Using Index - Delete Index Method]]
			- [[#Combining Both Pop Method and Delete Index Method - Updated Pop Method]]
		- [[#Delete At Any Position Using Data - Delete Data Method]]
	- [[#Modification Methods]]
		- [[#Modify Data Using Index - Modify Index Method]]
		- [[#Modify Data Using Data - Modify Data Method]]
	- [[#Miscellaneous Methods]]
		- [[#Display The Whole Linked List - Print Method]]
		- [[#Check If Linked List Empty Or Not - Check Empty Method]]
		- [[#Length Of Whole Linked List - Length Method]]
- [[#Creation Of Linked List and Usage]]

---

> [!INFO] Resource(s)
> - http://projectpython.net/chapter17/
> - https://www.youtube.com/watch?v=1iz9SRWdpX8
> - https://www.youtube.com/watch?v=N6dOwBde7-M
> - https://www.youtube.com/watch?v=WwfhLC16bis
> - https://www.youtube.com/watch?v=qp8u-frRAnU

> [!WARNING]
> <h6 align="center" style="color: white;"> Confusion Between Head Node and Head Pointer</h6>
> 
> The '**node**' is the very *first* node in the linked list while the head '**pointer**' is the pointer that "*locates*" the first **node**!

# Creation Of Class Node

Below you are going to find the *class* implementation of a **node**.

```python
# our linked list nodes
class Node:
    # our constructor method
    def __init__(self, data) -> None:
        # the actual node data / element inside node
        # INFO: in this case, head cannot start without any data
        self.data = data
        # class variable to "point" to the next node
        self.next = None
```

- Therefore to **create** some *nodes*, we can simply create our objects of class `Node`:

```python
# our main function
def main():
    # create our first ever linked list node
    head_node = Node("First - Head Node")

    # create some other nodes ( with a variety of data types )
    second_node = Node(69)
    third_node = Node(69.69)
    forth_node = Node([1, 2, 3, 4])
    fifth_node = Node({"x": 1, "y": 2})
	
    # last node does not point to anything
    last_node = Node([{1, 2, 3}, (4, 5, 6)])


# source the main function
if __name__ == "__main__":
    main()
```

> [!INFO] Initially Empty Or Not Empty?
> In the above `Node` class, we can see that **need** to pass the `data` attribute to the object.
>
> But looking that the video resources above and also they way that my lecturer created their **initial** `head` node. They did **not** pass any data to it!
>
> > Meaning that *initially* the `head` node was **empty**!
>
> - The simplest way to allow for this; is to just set a **default value** for `data`:
>
> ```python
> # other code above
>    # our constructor method
>    def __init__(self, data = None) -> None:
> 	   # other code below
> ```
>
> > The *rest* of the code is the **same**!
>
> But as we are going to create a `LinkedList` class... I am simply going to use the class `Node` that we implemented above

# Creation Of Linked List Class

Given that we now have our class of `Node` and given that we also know that a **Linked List** is basically a bunch of *nodes* together.

> We can therefore implement our `LinkedList` class like so!

```python
# our linked list class ==> to be able to link our nodes together
class LinkedList:
    # the constructor for the linked list class
    def __init__(self):
        # INFO: at the start of an EMPTY linked list
        # the head points to nothing! ( Yes... "pointer" to the first node )
        self.head = None
```

> This is literally how we can *define* and **implement** our class of `LinkedList`!

- Therefore, to create an **empty** linked list, we can simply create an *object* of the `LinkedList` class:

```python
# our main function
def main():
    # create object of type `LinkedList` to initialise our linked list
    my_llist: LinkedList = LinkedList()


# source the main function
if __name__ == "__main__":
    main()
```

> [!INFO] Again! Empty Or Not Empty?
> In this case, we can see that we have the class "*pointer*" variable `self.head` which has been initialised to `None`!
> 
> But if we were to change it to something like this:
> 
> ```python
> # above code stays the same
> 
> # change the "location" of the pointer to point to a node
> # node in this case contains the integer value of '1'
> self.head = Node(1)
> 
> # code below stays the same
> ```
> 
> > The code that I wrote above works! The `head` pointer points to the `Node` with value '1'!

---

# Function / Method Related To Linked List

> [!INFO]
> These *functions* / *methods* that you are going to find below are all found **inside** ( */ methods of* ) the `LinkedList` class!

## Data Insertion Methods

### Insert At The Start - Prepend Method

```python
# method that will add data to start of the linked list ==> add data at "head"
def prepend(self, data):
	# declare and initialise new node object with "proper" data to add
	new_node: Node = Node(data)

	# make the new node neighbour become the node found at the head
	new_node.next = self.head

	# therefore, return the "head" pointer to its original position
	# ==> by "original" position we mean pointing to the very first node
	self.head = new_node
```

> [!TIP]- Time Complexity = O(1)
> - As we **don't** need to *traverse* the linked list **at all**
> 	- The position of the data is going to be **always** at the `head` / start
> - **Best** Case: O(1)
> - **Worst** Case: O(1)
> 	- Therefore, even if we had a *million* nodes; the *worst* case is still going to be **O(1)**

#### Prepend Method Usage

```python
# add some integer data to the front of the linked list
my_llist.prepend(3)
my_llist.prepend(2)
my_llist.prepend(1)
```

### Insert At The End - Append Method

```python
# method that will add data to end of the linked list ==> add data at "tail"
def append(self, data):
	# check if the linked list has no nodes present ==> 'head' pointer is emtpy
	if self.head is None:
		# there we just need to append the new node
		self.head = Node(data)

	# if the linked list contains node(s)
	else:
		# initialise pointer that is going to point to the "current" node
		current_node_ptr = self.head

		# iterate through the linked list until the tail has been reached
		# tail reached ==> pointer will be pointing at `None`
		while current_node_ptr.next:
			# meaning that the current node's neighbour is NOT emtpy
			# therefore, change the position of the current pointer to neighbour
			current_node_ptr = current_node_ptr.next

		# after iterating through the entire linked list ==> tail reached
		# therefore, we simply need to add the data at the end!
		current_node_ptr.next = Node(data)
```

> [!TIP]- Time Complexity = O(n)
> - The **overall** *running* time complexity for this method is going to be O(n)
> - Best Case: O(1)
> - Worst Case: O(n)
> 	- In this case the *best case* is going to be **constant** time as we <span style="color: orange;"> don't</span> need to *iterate* through the whole linked list
> 		- We have the "*best*" case when we have **no** nodes present

#### Append Method Usage

```python
# add some integer data to the back of the linked list
my_llist.append(5)
my_llist.append(6)
```

### Insert At Any Position Using Index - Insert Method

```python
# method that will allow the user to enter data at "any" index ( within reason )
def insert(self, index, data):
	# check if the user wants to insert data at index '0' ==> at the 'head'
	if index == 0:
		# therefore call the `prepend` function instead of re-writing it
		self.prepend(data)

	# if the index entered is not '0' / at the head
	else:
		# check if linked list does not contain any values
		if self.head is None:
			# meaning that they are no data currently present in linked list
			# therefore, raise a little `IndexError`
			raise IndexError("\n\t<< Linked List Empty!!! > > \n")

		# if the linked list contains any node(s)
		else:
			# initialise pointer that is going to point to the "current" node
			current_node_ptr = self.head

			# iterate through the number of nodes required
			# ==> iterate 1 before that "real" index to be able to add the required data
			for i in range(index - 1):
				# if the index entered is not found inside the linked list
				if current_node_ptr.next is None:
					# similarly, raise a little `IndexError`
					raise IndexError("\n\t<< Index Not Found!!! > > \n")

				# if the current node's neighbour is not empty
				# ==> change the current pointer position ( to the neighbour )
				current_node_ptr = current_node_ptr.next

			# if we have reached here ==> we have reached the desired index
			# therefore, create the new node
			new_node = Node(data)

			# initialise the new node's neighbour
			new_node.next = current_node_ptr.next

			# then re-initialise the current node's neighbour
			current_node_ptr.next = new_node
```

> [!TIP]- Time Complexity = O(n)
> - The **overall** *running* time complexity for this method is going to be O(n)
> - Best Case: O(1)
> - Worst Case: O(n)
> 	- In this case the *best case* is going to be **constant** time as we <span style="color: orange;"> don't</span> need to *iterate* through the whole linked list
> 		- We have the "*best*" case when we are trying to insert at *index* / *position* '**0**'!

#### Insert Method Usage

```python
# method 1: using `insert` method "directly"
my_llist.insert(5, 69)

# method 2: using `insert` method inside a `try... except` block
# exception handling for insertion of data using the `insert` method
try:
	# insert the integer value '4' at index '0'
	my_llist.insert(0, 4)

# if index has not been found
except IndexError:
	# output appropriate message
	print("\n" + "-" * 50)
	print("\t   << Index Error!!! > > ")
	print("-" * 50)
```

### Insert In Orderly Manner - Insert Ordered Method

```python
# method that will allow data to be automatically ordered when inserted
def insert_ordered(self, data):
	# create the new node to be added to the linked list
	new_node: Node = Node(data)

	# check if the linked list has no nodes present ==> 'head' pointer is emtpy
	if self.head is None:
		# there we just need to append the new node
		self.head = new_node

	# check if the linked lists contains only 1 node
	# check if the data to add is smaller than that found at the 'head' pointer
	elif self.head.data > data:
		# as new data needs to be in front of current data found at 'head'
		# therefore call the `prepend` function instead of re-writing it
		self.prepend(data)

	# if linked list contains other node(s) and data is bigger than at "current" node
	else:
		# initialise pointer that is going to point to the "current" node
		current_node_ptr = self.head

		# initialise another pointer to keep track of previous node
		# pointer that will be 1 node behind the current pointer
		previous_node_ptr = None

		# iterate through the linked list
		# until the correct "data" position has been found
		while current_node_ptr is not None and current_node_ptr.data < data:
			# keep track of the "path" / current node's previous neighbour
			previous_node_ptr = current_node_ptr

			# change the current node pointer to the next neighbour
			current_node_ptr = current_node_ptr.next

		# after iterating through the linked list ==> "data" position found
		# therefore, we simply need to add the data at that position!

		# initialise the new node's neighbour
		new_node.next = current_node_ptr

		# then re-initialise the current node's neighbour
		# then initialise the new node's "previous" neighbour's "new" neighbour
		previous_node_ptr.next = new_node
```

> [!TIP]- Time Complexity = O(n)
> - The **overall** *running* time complexity for this method is going to be O(n)
> - Best Case: O(1)
> - Worst Case: O(n)
> 	- In this case the *best case* is going to be **constant** time as we <span style="color: orange;"> don't</span> need to *iterate* through the whole linked list
> 		- We have the "*best*" case when we are trying to insert at *index* / *position* '**0**'!

#### Insert Ordered Method Usage

```python
# insert data in an ordered manner
my_llist.insert_ordered(100)
my_llist.insert_ordered(8)
my_llist.insert_ordered(0)
my_llist.insert_ordered(-1)
```

## Data Removal Methods

### Delete At The Start - Delete Head Method

```python
# method that will remove data from start of the linked list ==> remove data from "head"
def delete_head(self):
	# check if the linked list has no nodes present ==> 'head' pointer is emtpy
	if self.head is None:
		# meaning that they are no data currently present in linked list
		# therefore, raise a little `IndexError`
		raise IndexError("\n\t<< Linked List Empty!!! > > \n")

	# if the linked list is not empty; remove the first node
	# by moving the 'head' pointer to point to the next node / second node
	self.head = self.head.next
```

> [!TIP]- Time Complexity = O(1)
> - As we **don't** need to *traverse* the linked list **at all**
> 	- The position of the data is going to be **always** at the `head` / start
> - **Best** Case: O(1)
> - **Worst** Case: O(1)
> 	- Therefore, even if we had a *million* nodes; the *worst* case is still going to be **O(1)**

#### Delete Head Method Usage

```python
# method 1: using `delete_head` method "directly"
my_llist.delete_head()

# method 2: using `delete_head` method inside a `try... except` block
# exception handling for removal of data using the `delete_head` method
try:
	my_llist.delete_head()

# if index has not been found
except IndexError:
	# output appropriate message
	print("\n\t" + "-" * 50)
	print("\t\t\t<< Index Error!!! > > ")
	print("\t" + "-" * 50)
```

### Delete At The End - Pop Method

```python
# method that will remove data from end of the linked list ==> remove data from "tail"
def pop(self):
	# check if the linked list has no nodes present ==> 'head' pointer is emtpy
	if self.head is None:
		# meaning that they are no data currently present in linked list
		# therefore, raise a little `IndexError`
		raise IndexError("\n\t<< Linked List Empty!!! > > \n")

	# if the linked list is not empty
	else:
		# if the linked list only contains 1 single little node
		# initialise pointer that is going to point to the "current" node
		current_node_ptr = self.head

		# check if the current node's ( i.e 'head' pointer ) node points to `None`
		if current_node_ptr.next is None:
			# get the data of the node to be removed
			popped_data = current_node_ptr.data

			# meaning that we can remove the only node present ==> head points to `None`
			self.head = None

			# return the popped value to the "main" function
			return popped_data

		# if linked list contains more than 1 nodes
		# ==> iterate through the whole linked list until "tail" is reached
		while current_node_ptr.next.next:
			# if the neighbour's neighbour contains data ==> not "tail"
			# change the position of the current node pointer by 1 ( "next" )
			current_node_ptr = current_node_ptr.next

		# if the "tail" has been reach ==> get the data that will be removed
		popped_data = current_node_ptr.next.data

		# remove / pop the last node from linked list
		current_node_ptr.next = None

		# return the popped value to the "main" function
		return popped_data
```

> [!TIP]- Time Complexity = O(n)
> - The **overall** *running* time complexity for this method is going to be O(n)
> - Best Case: O(1)
> - Worst Case: O(n)
> 	- In this case the *best case* is going to be **constant** time as we <span style="color: orange;"> don't</span> need to *iterate* through the whole linked list
> 		- We have the "*best*" case when we have **no** or **1** node is present

#### Pop Method Usage

```python
# method 1: using `pop` method "directly"
my_llist.pop()

# method 2: pop the data and display the data popped
print("\n\t" + "-" * 50)
print(f"\t\t   == Popped Node Data: {my_llist.pop()} ==")
print("\t" + "-" * 50)

# method 3: using `pop` method inside a `try... except` block
# exception handling for removal of data using the `pop` method
try:
	my_llist.pop()

# if index has not been found
except IndexError:
	# output appropriate message
	print("\n\t" + "-" * 50)
	print("\t\t\t<< Index Error!!! > > ")
	print("\t" + "-" * 50)
```

### Delete At Any Position Using Index - Delete Index Method

```python
# method that will allow the user to remove data at "any" index ( within reason )
def delete_index(self, index):
	# check if the linked list has no nodes present ==> 'head' pointer is emtpy
	if self.head is None:
		# meaning that they are no data currently present in linked list
		# therefore, raise a little `IndexError`
		raise IndexError("\n\t<< Linked List Empty!!! > > \n")

	# if the linked list is not empty
	else:
		# initialise pointer that is going to point to the "current" node
		current_node_ptr = self.head

		# check if the user wants to remove data at index '0' ==> at the 'head'
		if index == 0:
			# get the data of the node to be removed
			popped_data = current_node_ptr.data

			# simply make the head pointer points to the "head" node's neighbour
			self.head = current_node_ptr.next

			# return the popped value to the "main" function
			return popped_data

		# iterate through the number of nodes required
		# ==> iterate 1 before that "real" index to be able to remove the required data
		for i in range(index - 1):
			# if the index entered is not found inside the linked list
			if current_node_ptr.next is None:
				# similarly, raise a little `IndexError`
				raise IndexError("\n\t<< Index Error... Tail Reached!!! > > \n")

			# if the current node's neighbour is not empty
			# ==> change the current pointer position ( to the neighbour )
			current_node_ptr = current_node_ptr.next

		# check if the current node's ( being pointed at ) neighbour is empty
		if current_node_ptr.next is None:
			# similarly, raise a little `IndexError`
			raise IndexError("\n\t<< Index Error... Index Too Big!!! > > \n")

		# but if we found the proper "index" that we need to remove
		else:
			# remove the node from the linked list
			current_node_ptr.next = current_node_ptr.next.next
```

> [!TIP]- Time Complexity = O(n)
> - The **overall** *running* time complexity for this method is going to be O(n)
> - Best Case: O(1)
> - Worst Case: O(n)
> 	- In this case the *best case* is going to be **constant** time as we <span style="color: orange;"> don't</span> need to *iterate* through the whole linked list
> 		- We have the "*best*" case when we have **no** or *removing* **first** node

#### Delete Index Method Usage

```python
# method 1: using `delete_index` method "directly"
my_llist.delete_index(5)

# method 2: using `delete_index` method inside a `try... except` block
# exception handling for removal of data using the `delete_index` method
try:
	my_llist.delete_index(3)

# if index has not been found
except IndexError:
	# output appropriate message
	print("\n", "\t" + "-" * 50)
	print("\t\t\t<< Index Error!!! > > ")
	print("\t" + "-" * 50)
```

---

### Combining Both Pop Method and Delete Index Method - Updated Pop Method

> This is completely my idea!

> [!INFO]
> The `pop` function in Python, *with lists*, can remove the **last** element from the list. But if we pass in a *value* / **index** inside the `pop` function.
>
> We can see that the `pop` function will *remove* the value at *that* **index**!
>
> Now, given that Python does <strong> <span style="color: orange;"> not</span> </strong> '*method overloading*'. I am simply going to create **another** *method* called `update_pop`!

> [!WARNING]
> There are **no** such thing as '*Method Overloading*' in Python!
>
> Hence, if you really want to *overload* the `pop` method. Simply remove the "*original*" `pop` method that we created and change the name of the method found below from `updated_pop` to `pop`!

```python
# method that will actually emulate the actual `pop` function in Python for lists
def updated_pop(self, index=None):
	# check if the user passed in the `index` as parameters
	if index is None:
		# check if the linked list contains no nodes ==> 'head' points to nothing
		if self.head is None:
			# meaning that there is nothing to remove
			# therefore, we can raise a little `IndexError`
			raise IndexError("\n\t<< Linked List Empty > > \n")

		# if the linked list contains node(s)
		else:
			# initialise pointer that is going to point to the "current" node
			current_node_ptr = self.head

			# check if the linked list contains only 1 node
			if current_node_ptr.next is None:
				# get the data of the node to be removed
				popped_data = current_node_ptr.data

				# make the 'head' pointer points to `None`
				self.head = None

				# return the removed data of node to the "main" program
				return popped_data

			# if the linked list contains more than 1 nodes
			# therefore, interate through the linked list until "tail" is reached
			while current_node_ptr.next.next:
				# check if the current pointer's neighbour is the last node
				# change the position of the current pointer to the neighbour
				current_node_ptr = current_node_ptr.next

			# if the "tail" has been reached ==> remove last the node
			# get the data of the last node to be removed
			popped_data = current_node_ptr.next.data

			# actually remove / pop the last node from the list
			current_node_ptr.next = None

			# return the popped value to the "main" function
			return popped_data

	# if the user does pass an index to the function ==> implement the `delete_index` method
	else:
		# check if the linked list contains any actual nodes or not
		if self.head is None:
			# meaning that they are no data currently present in linked list
			# therefore, raise a little `IndexError`
			raise IndexError("\n\t<< Linked List Empty!!! > > \n")

		# if the linked list is not empty
		else:
			# initialise pointer that is going to point to the "current" node
			current_node_ptr = self.head

			# check if the user wants to delete the first node ==> node at 'head'
			if index == 0:
				# get the data at the 'head' that we are trying to remove
				popped_data = current_node_ptr.data

				# remove the required node by simply changing to where 'head' points
				self.head = current_node_ptr.next

				# return the popped value to the "main" program
				return popped_data

			# if the user wants to delete something found in the middle
			# ==> iterate through the linked list until the proper `index` is reached
			for i in range(index - 1):
				# check if the current nodes neighbour is empty ==> meaning index not found
				if current_node_ptr.next is None:
					# similarly, raise a little `IndexError`
					raise IndexError("\n\t<< Index Error... Tail Reached!!! > > \n")

				# if the neighbour's node was not empty ==> change the position of the caret
				current_node_ptr = current_node_ptr.next

			# check if current pointer's next node is empty ==> "tail" reached
			# meaning if the user entered index that is not found in linked list
			if current_node_ptr.next is None:
				# similarly, raise a little `IndexError`
				raise IndexError("\n\t<< Index Error... Index Too Big!!! > > \n")

			# if the proper "index" was found
			else:
				# get the data of the node to be removed
				popped_data = current_node_ptr.next.data

				# therefore, make current node point to the neighbour's neighbour
				current_node_ptr.next = current_node_ptr.next.next

				# return the removed / popped data to the "main" function
				return popped_data
```

> [!TIP]- Time Complexity = O(n)
> - The **overall** *running* time complexity for this method is going to be O(n)
> - Best Case: O(1)
> - Worst Case: O(n)
> 	- In this case the *best case* is going to be **constant** time as we <span style="color: orange;"> don't</span> need to *iterate* through the whole linked list
> 		- We have the "*best*" case when we have **no** or *removing* **first** node

> [!SUCCESS]
> We have basically combined the `pop` and `delete_index` methods!
>
> I mean you could also have make the `updated_pop` method simply **call** the `pop` and `delete_index` method...
>
> > "*But what's the fucking fun in that*!!!"
>

#### Updated Pop Method Usage

```python
# method 1: using `update_pop` method "directly"
my_llist.updated_pop(5)

# method 2: using `updated_pop` method inside a `try... except` block
# exception handling for removal of data using the `updated_pop` method
try:
	my_llist.updated_pop(3)

# if index has not been found
except IndexError:
	# output appropriate message
	print("\n", "\t" + "-" * 50)
	print("\t\t\t<< Index Error!!! > > ")
	print("\t" + "-" * 50)
```

---

### Delete At Any Position Using Data - Delete Data Method

```python
# method that will allow the user to remove data using the data itself
def delete_data(self, data):
	# check if the linked list has no nodes present ==> 'head' pointer is emtpy
	if self.head is None:
		# meaning that they are no data currently present in linked list
		# therefore, raise a little `IndexError`
		raise IndexError("\n\t<< Linked List Empty!!! > > \n")

	# if the linked list is not empty
	else:
		# initialise pointer that is going to point to the "current" node
		current_node_ptr = self.head

		# check if the data to be removed is found inside the 'head' node / pointer itself
		if current_node_ptr is not None:
			# meaning that the 'head' node does contain data
			# therefore check if the data to be removed is found inside the first node
			if current_node_ptr.data == data:
				# meaning that the data to be removed has been found ==> remove first node
				self.head = current_node_ptr.next

			# if the data is not found inside the head
			else:
				# ==> iterate through the whole linked list until "tail" is reached
				while current_node_ptr.next:
					# check if the data is found at the current node's neighbour
					if current_node_ptr.next.data == data:
						# meaning that the data if found
						# therefore make the current pointer point to the neighbour's neighbour
						current_node_ptr.next = current_node_ptr.next.next

						# as data is found ==> not need to keep iterating through linked list
						# therefore simply return to the "main" function
						return

					# if the data has not been found at the current node' neighbour
					# change the position of the current pointer to the neighbour
					current_node_ptr = current_node_ptr.next

				# if the data has not been found ==> data not present inside linked list
				raise ValueError(f"\n\t<< '{data}' Has NOT Been Found!!! > > \n")
```

> [!TIP]- Time Complexity = O(n)
> - The **overall** *running* time complexity for this method is going to be O(n)
> - Best Case: O(1)
> - Worst Case: O(n)
> 	- In this case the *best case* is going to be **constant** time as we <span style="color: orange;"> don't</span> need to *iterate* through the whole linked list
> 		- We have the "*best*" case when we have **no** or *removing* **first** node

#### Delete Data Method Usage

```python
# method 1: using `delete_data` method "directly"
my_llist.delete_data(5)

# method 2: using `delete_data` method inside a `try... except` block
# exception handling for removal of data using the `delete_data` method
try:
	my_llist.delete_data(1)
	my_llist.delete_data(5)
 	my_llist.delete_data(69)

# if the linked list is emtpy
except IndexError:
	# output appropriate message
	print("\n", "\t" + "-" * 50)
	print("\t\t\t<< Index Error... Emtpy Linked List!!! > > ")
	print("\t" + "-" * 50)

# if the linked list is emtpy
except ValueError:
	# output appropriate message
	print("\n", "\t" + "-" * 50)
	print("\t\t\t<< Data NOT Found!!! > > ")
	print("\t" + "-" * 50)
```

## Modification Methods

### Modify Data Using Index - Modify Index Method

```python
# method that will allow the user to modify a node located by its index
def modify_node_index(self, index, new_data):
	# check if the linked list has no nodes present ==> 'head' pointer is emtpy
	if self.head is None:
		# meaning that they are no data currently present in linked list
		# therefore, raise a little `IndexError`
		raise IndexError("\n\t<< Linked List Empty!!! > > \n")

	# if the linked list is not empty
	else:
		# initialise pointer that is going to point to the "current" node
		current_node_ptr = self.head

		# iterate through the linked list until the proper "index" is reached
		# NOTE: in this case, we just do `index` instead of `index - 1`
		# this is because we need to go to "that" node instead of one before it
		for i in range(index):
			# check if the current node's neighbour is empty
			if current_node_ptr.next is None:
				# meaning that they are no data currently present in linked list
				# therefore, raise a little `IndexError`
				raise IndexError("\n\t<< Index Not Found... Tail Reached!!! > > \n")

			# if the neighbour's node is not empty
			# ==> change the current pointer's position to that neighbour
			current_node_ptr = current_node_ptr.next

		# if the proper index as been found ==> change the value at that index
		current_node_ptr.data = new_data

		# return the the "main" program after modifying the correct data
		return
```

> [!TIP]- Time Complexity = O(n)
> - The **overall** *running* time complexity for this method is going to be O(n)
> - Best Case: O(1)
> - Worst Case: O(n)
> 	- In this case the *best case* is going to be **constant** time as we <span style="color: orange;"> don't</span> need to *iterate* through the whole linked list
> 		- We have the "*best*" case when we have **no** nodes to *modify*

#### Modify Data Using Index Method Usage

```python
# method 1: using `modify_node_index` method "directly"
my_llist.modify_node_index(5, 69)

# method 2: using `delete_data` method inside a `try... except` block
# exception handling for removal of data using the `modify_node_index` method
try:
	my_llist.modify_node_index(1, 2)
	my_llist.modify_node_index(2, 3)
	my_llist.modify_node_index(69, 69)

# if index has not been found
except IndexError:
	# output appropriate message
	print("\n", "\t" + "-" * 50)
	print("\t\t\t<< Index Error!!! > > ")
	print("\t" + "-" * 50)
```

### Modify Data Using Data - Modify Data Method

```python
# method that will allow the user to modify a node located by its old data
def modify_node_data(self, old_data, new_data):
	# check if the linked list has no nodes present ==> 'head' pointer is emtpy
	if self.head is None:
		# meaning that they are no data currently present in linked list
		# therefore, raise a little `IndexError`
		raise IndexError("\n\t<< Linked List Empty!!! > > \n")

	# if the linked list is not empty
	else:
		# initialise pointer that is going to point to the "current" node
		current_node_ptr = self.head

		# iterate through the linked to list to find the correct node
		while current_node_ptr is not None:
			# check if the current node's data matches the `old_data`
			if current_node_ptr.data == old_data:
				# meaning that we have found the "proper" node
				# therefore, modify the data found inside the node
				current_node_ptr.data = new_data

				# as data has already been modify ==> simply return to the "main" program
				return

			# else if the "proper" / required node has not been found
			# ==> change the position of the current pointer to the next node
			current_node_ptr = current_node_ptr.next

		# if the node containing the old data has not been found
		# therefore raise a little `ValueError`
		raise ValueError(
			f"\n\t<< Node Containing '{old_data}' Has NOT Been Found!!! > > \n"
		)
```

> [!TIP]- Time Complexity = O(n)
> - The **overall** *running* time complexity for this method is going to be O(n)
> - Best Case: O(1)
> - Worst Case: O(n)
> 	- In this case the *best case* is going to be **constant** time as we <span style="color: orange;"> don't</span> need to *iterate* through the whole linked list
> 		- We have the "*best*" case when we have **no** nodes to *modify*

#### Modify Data Using Data Method Usage

```python
# method 1: using `modify_node_data` method "directly"
my_llist.modify_node_data(5)

# method 2: using `modify_node` method inside a `try... except` block
# exception handling for removal of data using the `modify_node_data` method
try:
	my_llist.modify_node_data(3, 1)
	my_llist.modify_node_data(1, 3)
	my_llist.modify_node_data(69, 69)

# if index has not been found
except IndexError:
	# output appropriate message
	print("\n\t" + "-"  *50)
	print("\t\t\t<< List Empty!!! > > ")
	print("\t" + "-" * 50)
	
# if value has not been found
except ValueError:
	# output appropriate message
	print("\n\t" + "-" * 50)
	print("\t\t\t<< Old Data NOT Found!!! > > ")
	print("\t" + "-" * 50)
```

## Miscellaneous Methods

### Display The Whole Linked List - Print Method

```python
# method to be able to display the whole linked list ==> implement using dunder method
def __repr__(self):
	# before displaying the whole linked list; check if nodes are actually present
	if self.head is None:
		# meaning that there is nothing inside the linked list
		# ==> show "EMTPY" linked list
		return "\n\tHead --> Tail ( None )\n"


	# if there are node(s) present inside the linked list
	else:
		# initialise pointer that is going to point to the "current" node
		current_node_ptr = self.head

		# declare and initialised the "returned" string that we are going to display
		linked_list_repr = f"Head --> {current_node_ptr.data}"

		# iterate through the linked list until the tail has been reached
		# tail reached ==> pointer will be pointing at `None`
		while current_node_ptr.next:
			# change the position of the pointer to the next node
			current_node_ptr = current_node_ptr.next

			# "append" the data of this "next" node to the "returned" string
			linked_list_repr += f" --> {current_node_ptr.data}"

		# after iterating through the entire linked list ==> tail reached
		linked_list_repr += " --> Tail ( None )"

	# return the string created to the "main" function
	return linked_list_repr
```

> [!TIP]- Time Complexity = O(n)
> - As we need to **traverse** through the *whole* linked list
> 	- The `while` loop needs to run `n` times.
> - **Best** Case: O(1)
> - **Worst** Case: O(n)

#### Print / Representation Method Usage

```python
# display / represent the whole linked list to the user
print("\n Linked List Representation ( Before Insertion Of Data ):\n")
print(f"\t\t{my_llist}")
```

> The `__repr__` and `__str__` method allows us to simply pass the **object** inside the `print` function!

### Check If Linked List Empty Or Not - Check Empty Method

```python
# method to check if a linked list is empty or not
def check_emtpy(self):
	# if the 'head' pointer points to nothing ==> no nodes present
	return self.head is None
```

> [!NOTE] The `None` Keyword in Python
> In the lecturer's code, she was doing something like this:
>
> ```python
> return self.head == None
> ```
>
> Well, as I use Neovim; I see that [Ruff](https://github.com/astral-sh/ruff) *linter*, starts to scream at me saying that:
>
> > "*Comparison to `None` should be `cond is None`*"!
>

#### Check Empty Method Usage

- This is how we are going to use the `check_empty` method:

```python
# check whether the linked list is emtpy or not
print(f"\nLinked List Empty? {my_llist.check_emtpy()}\n")
```

### Length Of Whole Linked List - Length Method

There are 2 main ways to find the *total* **length** of a Linked List. These *ways* includes:

- Using `self.size` **class variable** to keep track of number of nodes
- Using `len()` **function**... Well to find the length

> [!TIP] What Is Better? **It Depends**!!!
> If you are accessing the length of the linked list "*all the time*". Therefore its recommended that you go for the first approach as `self.size`, if you look at it. Its just a **variable** being *accessed*!
>
> But if you are *occasionally* required to find the length of said linked list; just implement the [dunder method](https://www.youtube.com/watch?v=bGGXE0D41Nw) `__len__` so that we can call the `len()` function on the linked list!
>
> > I **prefer** the *second* method!
>

#### Find The Length Using Class Variable

- Therefore **modify** our `LinkedList` *class* and add the new class variable `self.size`:

```python
# our linked list class ==> to be able to link our nodes together
class LinkedList:
    # the constructor for the linked list class
    def __init__(self):
        # INFO: at the start of an EMPTY linked list
        # the head points to nothing! ( Yes... "pointer" to the first node )
        self.head = None
        
        # initialise the size class variable to '0'
        # as the linked list does not contains any nodes
        self.size = 0
```

> [!WARNING] **Increment** / **Decrement**!!!
> If you are using this *method* to find the **length** of the linked list. You **must** either *increment* or *decrement* the `self.size` method each time in the specific methods.
>
> For example, in the `.append()` method you are going to **increment** *while* in the `.pop()` method, you are going to **decrement**!

#### Find The Length Using Function

- This is my *preferred* method to find the length of a linked list:

```python
# method to find the length "whole" linked list ==> implement using dunder method
def __len__(self):
	# initialise pointer that is going to point to the "current" node
	current_node_ptr = self.head

	# declare and initialise variable to keep track of number of nodes
	node_count = 0

	# iterate through the linked list until the tail has been reached
	# tail reached ==> pointer will be pointing at `None`
	while current_node_ptr is not None:
		# meaning that a node has been found
		node_count += 1

		# change the position of pointer to the next node
		current_node_ptr = current_node_ptr.next

	# finally when there are no nodes to iterate
	# ==> tail reached; return number of nodes
	return node_count
```

> [!TIP]- Time Complexity = O(n)
> - As we need to **traverse** through the *whole* linked list
> 	- The `while` loop needs to run `n` times.
> - **Best** Case: O(n)
> - **Worst** Case: O(n)
> 	- In this case, *best case* and *worst case* are going be the **same** as we <span style="color: orange;"> don't</span> know if we have only 1 node or `n` nodes!

##### Length Method Usage

```python
# find the length of the linked list
print(f"\nLength Of Linked List = {len(my_llist)}\n")
```

---

# Creation Of Linked List and Usage

## Actual Code

```python
# our linked list nodes
class Node:
    # our constructor method
    def __init__(self, data) -> None:
        # the actual node data / element inside node
        # INFO: in this case, head cannot start without any data
        self.data = data
        # class variable to "point" to the next node
        self.next = None


# our linked list class ==> to be able to link our nodes together
class LinkedList:
    # the constructor for the linked list class
    def __init__(self):
        # INFO: at the start of an EMPTY linked list
        # the head points to nothing! ( Yes... "pointer" to the first node )
        self.head = None

    # method that will add data to start of the linked list ==> add data at "head"
    def prepend(self, data):
        # declare and initialise new node object with "proper" data to add
        new_node: Node = Node(data)

        # make the new node neighbour become the node found at the head
        new_node.next = self.head

        # therefore, return the "head" pointer to its original position
        # ==> by "original" position we mean pointing to the very first node
        self.head = new_node

    # method that will add data to end of the linked list ==> add data at "tail"
    def append(self, data):
        # check if the linked list has no nodes present ==> 'head' pointer is emtpy
        if self.head is None:
            # there we just need to append the new node
            self.head = Node(data)

        # if the linked list contains node(s)
        else:
            # initialise pointer that is going to point to the "current" node
            current_node_ptr = self.head

            # iterate through the linked list until the tail has been reached
            # tail reached ==> pointer will be pointing at `None`
            while current_node_ptr.next:
                # meaning that the current node's neighbour is NOT emtpy
                # therefore, change the position of the current pointer to neighbour
                current_node_ptr = current_node_ptr.next

            # after iterating through the entire linked list ==> tail reached
            # therefore, we simply need to add the data at the end!
            current_node_ptr.next = Node(data)

    # method that will allow the user to enter data at "any" index ( within reason )
    def insert(self, index, data):
        # check if the user wants to insert data at index '0' ==> at the 'head'
        if index == 0:
            # therefore call the `prepend` function instead of re-writing it
            self.prepend(data)

        # if the index entered is not '0' / at the head
        else:
            # check if linked list does not contain any values
            if self.head is None:
                # meaning that they are no data currently present in linked list
                # therefore, raise a little `IndexError`
                raise IndexError("\n\t<< Linked List Empty!!! > > \n")

            # if the linked list contains any node(s)
            else:
                # initialise pointer that is going to point to the "current" node
                current_node_ptr = self.head

                # iterate through the number of nodes required
                # ==> iterate 1 before that "real" index to be able to add the required data
                for i in range(index - 1):
                    # if the index entered is not found inside the linked list
                    if current_node_ptr.next is None:
                        # similarly, raise a little `IndexError`
                        raise IndexError("\n\t<< Linked List Empty!!! > > \n")

                    # if the current node's neighbour is not empty
                    # ==> change the current pointer position ( to the neighbour )
                    current_node_ptr = current_node_ptr.next

                # if we have reached here ==> we have reached the desired index
                # therefore, create the new node
                new_node = Node(data)

                # initialise the new node's neighbour
                new_node.next = current_node_ptr.next

                # then re-initialise the current node's neighbour
                current_node_ptr.next = new_node

    # method that will allow data to be automatically ordered when inserted
    def insert_ordered(self, data):
        # create the new node to be added to the linked list
        new_node: Node = Node(data)

        # check if the linked list has no nodes present ==> 'head' pointer is emtpy
        if self.head is None:
            # there we just need to append the new node
            self.head = Node(data)

        # check if the linked lists contains only 1 node
        # check if the data to add is smaller than that found at the 'head' pointer
        elif self.head.data > data:
            # as new data needs to be in front of current data found at 'head'
            # therefore call the `prepend` function instead of re-writing it
            self.prepend(data)

        # if linked list contains other node(s) and data is bigger than at "current" node
        else:
            # initialise pointer that is going to point to the "current" node
            current_node_ptr = self.head

            # initialise another pointer to keep track of previous node
            # pointer that will be 1 node behind the current pointer
            previous_node_ptr = None

            # iterate through the linked list
            # until the correct "data" position has been found
            while current_node_ptr is not None and current_node_ptr.data < data:
                # keep track of the "path" / current node's previous neighbour
                previous_node_ptr = current_node_ptr

                # change the current node pointer to the next neighbour
                current_node_ptr = current_node_ptr.next

            # after iterating through the linked list ==> "data" position found
            # therefore, we simply need to add the data at that position!

            # initialise the new node's neighbour
            new_node.next = current_node_ptr

            # then re-initialise the current node's neighbour
            # then initialise the new node's "previous" neighbour's "new" neighbour
            previous_node_ptr.next = new_node

    # method that will remove data from start of the linked list ==> remove data from "head"
    def delete_head(self):
        # check if the linked list has no nodes present ==> 'head' pointer is emtpy
        if self.head is None:
            # meaning that they are no data currently present in linked list
            # therefore, raise a little `IndexError`
            raise IndexError("\n\t<< Linked List Empty!!! > > \n")

        # if the linked list is not empty; remove the first node
        # by moving the 'head' pointer to point to the next node / second node
        self.head = self.head.next

    # method that will remove data from end of the linked list ==> remove data from "tail"
    def pop(self):
        # check if the linked list has no nodes present ==> 'head' pointer is emtpy
        if self.head is None:
            # meaning that they are no data currently present in linked list
            # therefore, raise a little `IndexError`
            raise IndexError("\n\t<< Linked List Empty!!! > > \n")

        # if the linked list is not empty
        else:
            # if the linked list only contains 1 single little node
            # initialise pointer that is going to point to the "current" node
            current_node_ptr = self.head

            # check if the current node's ( i.e 'head' pointer ) node points to `None`
            if current_node_ptr.next is None:
                # get the data of the node to be removed
                popped_data = current_node_ptr.data

                # meaning that we can remove the only node present ==> head points to `None`
                self.head = None

                # return the popped value to the "main" function
                return popped_data

            # if linked list contains more than 1 nodes
            # ==> iterate through the whole linked list until "tail" is reached
            while current_node_ptr.next.next:
                # if the neighbour's neighbour contains data ==> not "tail"
                # change the position of the current node pointer by 1 ( "next" )
                current_node_ptr = current_node_ptr.next

            # if the "tail" has been reach ==> get the data that will be removed
            popped_data = current_node_ptr.next.data

            # remove / pop the last node from linked list
            current_node_ptr.next = None

            # return the popped value to the "main" function
            return popped_data

    # method that will allow the user to remove data at "any" index ( within reason )
    def delete_index(self, index):
        # check if the linked list has no nodes present ==> 'head' pointer is emtpy
        if self.head is None:
            # meaning that they are no data currently present in linked list
            # therefore, raise a little `IndexError`
            raise IndexError("\n\t<< Linked List Empty!!! > > \n")

        # if the linked list is not empty
        else:
            # initialise pointer that is going to point to the "current" node
            current_node_ptr = self.head

            # check if the user wants to remove data at index '0' ==> at the 'head'
            if index == 0:
                # get the data of the node to be removed
                popped_data = current_node_ptr.data

                # simply make the head pointer points to the "head" node's neighbour
                self.head = current_node_ptr.next

                # return the popped value to the "main" function
                return popped_data

            # iterate through the number of nodes required
            # ==> iterate 1 before that "real" index to be able to remove the required data
            for i in range(index - 1):
                # if the index entered is not found inside the linked list
                if current_node_ptr.next is None:
                    # similarly, raise a little `IndexError`
                    raise IndexError("\n\t<< Index Error... Tail Reached!!! > > \n")

                # if the current node's neighbour is not empty
                # ==> change the current pointer position ( to the neighbour )
                current_node_ptr = current_node_ptr.next

            # check if the current node's ( being pointed at ) neighbour is empty
            if current_node_ptr.next is None:
                # similarly, raise a little `IndexError`
                raise IndexError("\n\t<< Index Error... Index Too Big!!! > > \n")

            # but if we found the proper "index" that we need to remove
            else:
                # remove the node from the linked list
                current_node_ptr.next = current_node_ptr.next.next

    # method that will actually emulate the actual `pop` function in Python for lists
    def updated_pop(self, index=None):
        # check if the user passed in the `index` as parameters
        if index is None:
            # check if the linked list contains no nodes ==> 'head' points to nothing
            if self.head is None:
                # meaning that there is nothing to remove
                # therefore, we can raise a little `IndexError`
                raise IndexError("\n\t<< Linked List Empty > > \n")

            # if the linked list contains node(s)
            else:
                # initialise pointer that is going to point to the "current" node
                current_node_ptr = self.head

                # check if the linked list contains only 1 node
                if current_node_ptr.next is None:
                    # get the data of the node to be removed
                    popped_data = current_node_ptr.data

                    # make the 'head' pointer points to `None`
                    self.head = None

                    # return the removed data of node to the "main" program
                    return popped_data

                # if the linked list contains more than 1 nodes
                # therefore, interate through the linked list until "tail" is reached
                while current_node_ptr.next.next:
                    # check if the current pointer's neighbour is the last node
                    # change the position of the current pointer to the neighbour
                    current_node_ptr = current_node_ptr.next

                # if the "tail" has been reached ==> remove last the node
                # get the data of the last node to be removed
                popped_data = current_node_ptr.next.data

                # actually remove / pop the last node from the list
                current_node_ptr.next = None

                # return the popped value to the "main" function
                return popped_data

        # if the user does pass an index to the function ==> implement the `delete_index` method
        else:
            # check if the linked list contains any actual nodes or not
            if self.head is None:
                # meaning that they are no data currently present in linked list
                # therefore, raise a little `IndexError`
                raise IndexError("\n\t<< Linked List Empty!!! > > \n")

            # if the linked list is not empty
            else:
                # initialise pointer that is going to point to the "current" node
                current_node_ptr = self.head

                # check if the user wants to delete the first node ==> node at 'head'
                if index == 0:
                    # get the data at the 'head' that we are trying to remove
                    popped_data = current_node_ptr.data

                    # remove the required node by simply changing to where 'head' points
                    self.head = current_node_ptr.next

                    # return the popped value to the "main" program
                    return popped_data

                # if the user wants to delete something found in the middle
                # ==> iterate through the linked list until the proper `index` is reached
                for i in range(index - 1):
                    # check if the current nodes neighbour is empty ==> meaning index not found
                    if current_node_ptr.next is None:
                        # similarly, raise a little `IndexError`
                        raise IndexError("\n\t<< Index Error... Tail Reached!!! > > \n")

                    # if the neighbour's node was not empty ==> change the position of the caret
                    current_node_ptr = current_node_ptr.next

                # check if current pointer's next node is empty ==> "tail" reached
                # meaning if the user entered index that is not found in linked list
                if current_node_ptr.next is None:
                    # similarly, raise a little `IndexError`
                    raise IndexError("\n\t<< Index Error... Index Too Big!!! > > \n")

                # if the proper "index" was found
                else:
                    # get the data of the node to be removed
                    popped_data = current_node_ptr.next.data

                    # therefore, make current node point to the neighbour's neighbour
                    current_node_ptr.next = current_node_ptr.next.next

                    # return the removed / popped data to the "main" function
                    return popped_data

    # method that will allow the user to remove data using the data itself
    def delete_data(self, data):
        # check if the linked list has no nodes present ==> 'head' pointer is emtpy
        if self.head is None:
            # meaning that they are no data currently present in linked list
            # therefore, raise a little `IndexError`
            raise IndexError("\n\t<< Linked List Empty!!! > > \n")

        # if the linked list is not empty
        else:
            # initialise pointer that is going to point to the "current" node
            current_node_ptr = self.head

            # check if the data to be removed is found inside the 'head' node / pointer itself
            if current_node_ptr is not None:
                # meaning that the 'head' node does contain data
                # therefore check if the data to be removed is found inside the first node
                if current_node_ptr.data == data:
                    # meaning that the data to be removed has been found ==> remove first node
                    self.head = current_node_ptr.next

                # if the data is not found inside the head
                else:
                    # ==> iterate through the whole linked list until "tail" is reached
                    while current_node_ptr.next:
                        # check if the data is found at the current node's neighbour
                        if current_node_ptr.next.data == data:
                            # meaning that the data if found
                            # therefore make the current pointer point to the neighbour's neighbour
                            current_node_ptr.next = current_node_ptr.next.next

                            # as data is found ==> not need to keep iterating through linked list
                            # therefore simply return to the "main" function
                            return

                        # if the data has not been found at the current node' neighbour
                        # change the position of the current pointer to the neighbour
                        current_node_ptr = current_node_ptr.next

                    # if the data has not been found ==> data not present inside linked list
                    raise ValueError(f"\n\t<< '{data}' Has NOT Been Found!!! > > \n")

    # method that will allow the user to modify a node located by its index
    def modify_node_index(self, index, new_data):
        # check if the linked list has no nodes present ==> 'head' pointer is emtpy
        if self.head is None:
            # meaning that they are no data currently present in linked list
            # therefore, raise a little `IndexError`
            raise IndexError("\n\t<< Linked List Empty!!! > > \n")

        # if the linked list is not empty
        else:
            # initialise pointer that is going to point to the "current" node
            current_node_ptr = self.head

            # iterate through the linked list until the proper "index" is reached
            # NOTE: in this case, we just do `index` instead of `index - 1`
            # this is because we need to go to "that" node instead of one before it
            for i in range(index):
                # check if the current node's neighbour is empty
                if current_node_ptr.next is None:
                    # meaning that they are no data currently present in linked list
                    # therefore, raise a little `IndexError`
                    raise IndexError("\n\t<< Index Not Found... Tail Reached!!! > > \n")

                # if the neighbour's node is not empty
                # ==> change the current pointer's position to that neighbour
                current_node_ptr = current_node_ptr.next

            # if the proper index as been found ==> change the value at that index
            current_node_ptr.data = new_data

            # return the the "main" program after modifying the correct data
            return

    # method that will allow the user to modify a node located by its old data
    def modify_node_data(self, old_data, new_data):
        # check if the linked list has no nodes present ==> 'head' pointer is emtpy
        if self.head is None:
            # meaning that they are no data currently present in linked list
            # therefore, raise a little `IndexError`
            raise IndexError("\n\t<< Linked List Empty!!! > > \n")

        # if the linked list is not empty
        else:
            # initialise pointer that is going to point to the "current" node
            current_node_ptr = self.head

            # iterate through the linked to list to find the correct node
            while current_node_ptr is not None:
                # check if the current node's data matches the `old_data`
                if current_node_ptr.data == old_data:
                    # meaning that we have found the "proper" node
                    # therefore, modify the data found inside the node
                    current_node_ptr.data = new_data

                    # as data has already been modify ==> simply return to the "main" program
                    return

                # else if the "proper" / required node has not been found
                # ==> change the position of the current pointer to the next node
                current_node_ptr = current_node_ptr.next

            # if the node containing the old data has not been found
            # therefore raise a little `ValueError`
            raise ValueError(
                f"\n\t<< Node Containing '{old_data}' Has NOT Been Found!!! > > \n"
            )

    # method to be able to display the whole linked list ==> implement using dunder method
    def __repr__(self):
        # before displaying the whole linked list; check if nodes are actually present
        if self.head is None:
            # meaning that there is nothing inside the linked list
            # ==> show "EMTPY" linked list
            return "\n\tHead --> Tail ( None )\n"

        # if there are node(s) present inside the linked list
        else:
            # initialise pointer that is going to point to the "current" node
            current_node_ptr = self.head

            # declare and initialised the "returned" string that we are going to display
            linked_list_repr = f"\n\tHead --> {current_node_ptr.data}"

            # iterate through the linked list until the tail has been reached
            # tail reached ==> pointer will be pointing at `None`
            while current_node_ptr.next:
                # change the position of the pointer to the next node
                current_node_ptr = current_node_ptr.next

                # "append" the data of this "next" node to the "returned" string
                linked_list_repr += f" --> {current_node_ptr.data}"

            # after iterating through the entire linked list ==> tail reached
            linked_list_repr += " --> Tail ( None )\n"

        # return the string created to the "main" function
        return linked_list_repr

    # method to check if a linked list is empty or not
    def check_emtpy(self):
        # if the 'head' pointer points to nothing ==> no nodes present
        return self.head is None

    # method to find the length "whole" linked list ==> implement using dunder method
    def __len__(self):
        # initialise pointer that is going to point to the "current" node
        current_node_ptr = self.head

        # declare and initialise variable to keep track of number of nodes
        node_count = 0

        # iterate through the linked list until the tail has been reached
        # tail reached ==> pointer will be pointing at `None`
        while current_node_ptr is not None:
            # meaning that a node has been found
            node_count += 1

            # change the position of pointer to the next node
            current_node_ptr = current_node_ptr.next

        # finally when there are no nodes to iterate
        # ==> tail reached; return number of nodes
        return node_count


def main():
    my_llist: LinkedList = LinkedList()

    print(f"Linked List Emtpy? {my_llist.check_emtpy()}")
    print(f"Linked List Length? {len(my_llist)}")

    # add some integer data to the front of the linked list
    my_llist.prepend(3)
    my_llist.prepend(2)
    my_llist.prepend(1)

    print(my_llist)

    my_llist.append(5)
    my_llist.append(6)

    print(my_llist)

    my_llist.insert(3, 4)
    my_llist.insert(6, 100)

    try:
        my_llist.insert(100, 100)

    except IndexError:
        print("\t\t" + "-" * 50)
        print("\t\t\t   << Index '100' Error!!! > > ")
        print("\t\t" + "-" * 50)

    print(my_llist)

    my_llist.insert_ordered(99)
    my_llist.insert_ordered(7)
    my_llist.insert_ordered(0)
    my_llist.insert_ordered(-1)

    print(my_llist)

    try:
        my_llist.delete_head()
        my_llist.delete_head()

    except IndexError:
        print("\t\t" + "-" * 50)
        print("\t\t\t   << Index '100' Error!!! > > ")
        print("\t\t" + "-" * 50)

    print(my_llist)

    my_llist.delete_index(7)

    try:
        my_llist.delete_index(len(my_llist))

    except IndexError:
        print("\t\t" + "-" * 50)
        print(f"\t\t\t    << Index '{len(my_llist)}' Error!!! > > ")
        print("\t\t" + "-" * 50)

    print(my_llist)

    my_llist.updated_pop()

    try:
        my_llist.updated_pop(len(my_llist))

    except IndexError:
        print("\t\t" + "-" * 50)
        print(f"\t\t\t    << Index '{len(my_llist)}' Error!!! > > ")
        print("\t\t" + "-" * 50)

    print(my_llist)

    my_llist.delete_data(4)

    try:
        my_llist.delete_data(100)

    except ValueError:
        print("\t\t" + "-" * 50)
        print("\t\t\t    << Value '100' Error!!! > > ")
        print("\t\t" + "-" * 50)

    print(my_llist)

    my_llist.modify_node_index(len(my_llist) - 1, 100)

    try:
        my_llist.modify_node_index(len(my_llist), 69)

    except IndexError:
        print("\t\t" + "-" * 50)
        print(f"\t\t\t    << Index '{len(my_llist)}' Error!!! > > ")
        print("\t\t" + "-" * 50)

    print(my_llist)

    my_llist.modify_node_data(100, 7)

    try:
        my_llist.modify_node_data(69, 69)

    except IndexError:
        print("\t\t" + "-" * 50)
        print("\t\t\t    << Index Error!!! > > ")
        print("\t\t" + "-" * 50)

    except ValueError:
        print("\t\t" + "-" * 50)
        print("\t\t\t    << Value '69' Error!!! > > ")
        print("\t\t" + "-" * 50)

    print(my_llist)

    print(f"Linked List Emtpy? {my_llist.check_emtpy()}")
    print(f"Linked List Length? {len(my_llist)}")


if __name__ == "__main__":
    main()
```

## The Output

```console
Linked List Emtpy? True
Linked List Length? 0

        Head --> 1 --> 2 --> 3 --> Tail ( None )


        Head --> 1 --> 2 --> 3 --> 5 --> 6 --> Tail ( None )

                --------------------------------------------------
                           << Index '100' Error!!! > >
                --------------------------------------------------

        Head --> 1 --> 2 --> 3 --> 4 --> 5 --> 6 --> 100 --> Tail ( None )


        Head --> -1 --> 0 --> 1 --> 2 --> 3 --> 4 --> 5 --> 6 --> 7 --> 99 --> 100 --> Tail ( None )


        Head --> 1 --> 2 --> 3 --> 4 --> 5 --> 6 --> 7 --> 99 --> 100 --> Tail ( None )

                --------------------------------------------------
                            << Index '8' Error!!! > >
                --------------------------------------------------

        Head --> 1 --> 2 --> 3 --> 4 --> 5 --> 6 --> 7 --> 100 --> Tail ( None )

                --------------------------------------------------
                            << Index '7' Error!!! > >
                --------------------------------------------------

        Head --> 1 --> 2 --> 3 --> 4 --> 5 --> 6 --> 7 --> Tail ( None )

                --------------------------------------------------
                            << Value '100' Error!!! > >
                --------------------------------------------------

        Head --> 1 --> 2 --> 3 --> 5 --> 6 --> 7 --> Tail ( None )

                --------------------------------------------------
                            << Index '6' Error!!! > >
                --------------------------------------------------

        Head --> 1 --> 2 --> 3 --> 5 --> 6 --> 100 --> Tail ( None )

                --------------------------------------------------
                            << Value '69' Error!!! > >
                --------------------------------------------------

        Head --> 1 --> 2 --> 3 --> 5 --> 6 --> 7 --> Tail ( None )

Linked List Emtpy? False
Linked List Length? 6
```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!