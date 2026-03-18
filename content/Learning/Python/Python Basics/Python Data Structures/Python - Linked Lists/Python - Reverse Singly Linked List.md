---
id: Python - Reverse Singly Linked List
aliases: Reversing A Singly Linked List ( LeetCode )
tags:
  - python
  - data-structures
  - lists
  - oop
author: S.Sunhaloo
date: 2025-10-06
status: Completed
---

## List of Contents

- [[#Reversing A Singly Linked List ( In-Place )]]
	- [[#Iterative Method ( In-Place )]]
	- [[#Recursive Method ( In-Place )]]
		- [[#NeetCode's Version]]
		- [[#Commenter's Version]]
- [[#Reversing A Singly Linked List ( Not In-Place )]]
	- [[#The Other Methods Required]]
	- [[#The Actual Method]]

---

> [!INFO] Resource(s)
> - NeetCode: https://www.youtube.com/watch?v=G0_I-ZF0S38
> - LeetCode 'Doocs': https://leetcode.doocs.org/en/lc/206
>
> > Original Singly Linked List Note: '[[Python - Singly Linked Lists]]'

> [!NOTE]
> I will be only adding the *method* for **reversing** the linked list itself. I am <span style="color: orange;"> not</span> going to try write everything from scratch again here.
>
> Similar to how I drew the *position* and *movement* of the **nodes** and "*arrows*" / *links*... I am **not** going to be drawing anything here also.
>
> This is because before even watching the video I did understand that we had to use **2 pointers** as we need to keep track of the *previous* node!
>
> > [!INFO]
> > > "*If I still have it*"
> >
> > Please refer to my Samsung Notes for the drawing or simply re-watch the video
>

# Reversing A Singly Linked List ( In-Place )

> [!WARNING]
> Again, I am only going to be showing the method `reverse` found **inside** the `LinkedList` class!
>
> What I am trying to say its that you **need** to *implement* the class of `Node` and `LinkedList` respectively.

## Iterative Method ( In-Place )

```python
# method that will reverse the linked list ==> ( head --> tail | tail --> head )
def reverse(self):
	# check if the linked list does not contain any values
	if self.head is None:
		# meaning that there are not data present in linked list
		# therefore, raise a little 'IndexError'
		raise IndexError("\n\t<< Linked List Empty!!! > > \n")

	# if the linked list contains any node
	else:
		# intialise pointer that is going to point to the "current" node
		current_node_ptr = self.head
		# intialise pointer that is going to point to the previous node ( of 'current' )
		previous_node_ptr = None

		# iterate through the number of nodes required
		while current_node_ptr:
			# WARNING: need to keep track of current pointer's neighbour
			current_node_ptr_next = current_node_ptr.next

			# make the current node point to the previous node
			# INFO: in the case for the first ( head ) node ==> points to 'None'
			current_node_ptr.next = previous_node_ptr

			# need to move the 'previous' node pointer to the next node first
			previous_node_ptr = current_node_ptr

			# therefore move the current node to the previous "current node" neighbour
			current_node_ptr = current_node_ptr_next

		# finally make the head point to the last ( now first ) node
		self.head = previous_node_ptr
```

> [!TIP]- Time Complexity = O(n)
> - The **overall** *running* time complexity for this method is going to be O(n)
> - Best Case: O(1)
> - Worst Case: O(n)
> 	- In this case the *best case* is going to be **constant** time as we <span style="color: orange;"> don't</span> need to *iterate* through the whole linked list
> 		- We have the "*best*" case when we have **one** node present

### Reverse ( Iterative ) Method ( In-Place ) Usage

```python
# method 1: using `reverse` method "directly"
my_llist.reverse()

# method 2: using `reverse` method inside a `try... except` block
# exception handling for reversing of linked list using the `reverse` method
try:
	# reverse the linked list
	my_llist.reverse()

# if index has not been found
except IndexError:
	# output appropriate message
	print("\n" + "-" * 50)
	print("\t   << Index Error!!! > > ")
	print("-" * 50)
```

## Recursive Method ( In-Place )

### NeetCode's Version

```python
# recursive method that will reverse the linked list ==> ( head --> tail | tail --> head )
# NOTE: in this case, we need to pass the node found at head of linked list
def recursion_reverse(self, head_node):
	# check if the linked list does not contain any values
	if head_node is None:
		# meaning that there are not data present in linked list
		# therefore, raise a little 'IndexError'
		raise IndexError("\n\t<< Linked List Empty!!! > > \n")

	# if we have exactly one node present inside the linked list
	if head_node.next is None:
		# therefore, we simply need to return the current node itself
		return head_node

	# intialise pointer to point to the new head
	new_head = head_node

	# check if the head has a neighbour
	if self.head.next:
		# call the function again on the sub-linked list
		new_head = self.recursion_reverse(head_node.next)

		# move the head the next head
		head_node.next.next = head_node

	# make the "last" head point to `None`
	head_node.next = None

	# return the new head
	return new_head
```

#### Reverse ( NeetCode - Recursive ) Method ( In-Place ) Usage

```python
# method 1: using `recursion_reverse` method "directly"
my_llist.recursion_reverse()

# method 2: using `recursion_reverse` method inside a `try... except` block
# exception handling for reversing of linked list using the `recursion_reverse` method
try:
	# reverse the linked list using recursion
	my_llist.recursion_reverse()

# if index has not been found
except IndexError:
	# output appropriate message
	print("\n" + "-" * 50)
	print("\t   << Index Error!!! > > ")
	print("-" * 50)
```

### Commenter's Version

```python
# recursive method that will reverse the linked list ==> ( head --> tail | tail --> head )
# NOTE: in this case, we need to pass the node found at head of linked list and `None`
def recursion_reverse_commenter(self):
	# check if the linked list does not contain any values
	if self.head is None:
		# meaning that there are not data present in linked list
		# therefore, raise a little 'IndexError'
		raise IndexError("\n\t<< Linked List Empty!!! > > \n")

	# INFO: helper function / method to perform the actual movement of data
	def reverse(current_node_ptr, previous_node_ptr):
		# check if the current pointer is 'None' ==> base case
		if current_node_ptr is None:
			# return the previous pointer ==> previous node's neighbour
			return previous_node_ptr

		# if the current pointer does not points to the "tail"

		# WARNING: need to keep track of the current pointer's neighbour
		current_node_ptr_next = current_node_ptr.next

		# make the current node point to the previous node
		# INFO: in the case for the first ( head ) node ==> points to 'None'
		current_node_ptr.next = previous_node_ptr

		# call the function again to repeat the process for other nodes
		return reverse(current_node_ptr_next, current_node_ptr)

	# therefore, actually call the helper function on the main linked list
	self.head = reverse(self.head, None)
```

##### Reverse ( Commenter - Recursive ) Method ( In-Place ) Usage

```python
# method 1: using `recursion_reverse_commenter` method "directly"
my_llist.recursion_reverse_commenter()

# method 2: using `recursion_reverse_commenter` method inside a `try... except` block
# exception handling for reversing of linked list using the `recursion_reverse_commenter` method
try:
	# reverse the linked list using recursion
	my_llist.recursion_reverse_commenter()

# if index has not been found
except IndexError:
	# output appropriate message
	print("\n" + "-" * 50)
	print("\t   << Index Error!!! > > ")
	print("-" * 50)
```

# Reversing A Singly Linked List ( Not In-Place )

> [!TIP] Mr Sathan's Method
> > He is the GOAT!
>
> I was having trouble with **iterative** version whereby instead of returning `self.head = previous_node_ptr`... I was just returning `previous_node_ptr` which simply <span style="color: red;"> breaks</span> the links between the nodes.
>
> > If you **don't** do what I just said above... In the output it will only show the "*first*" node!
>
> But he told me to do something **extremely** simple! "*Just create another Linked List*!"
>
> Yes, he was suggesting that instead of reversing the linked list "*in-place*", we just create a **new** Linked List and `return` that **new** Linked List!
>
> This is due to the fact that we already have our `pop`, `append` and `__len__` ( dunder ) methods!

> In the code block below, I am going to also add the code for the `pop`, `append` and `__len__` methods.

## The Other Methods Required

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

## The Actual Method

```python
# method that will reverse the linked list ==> ( head --> tail | tail --> head )
def new_list_reverse(self):
	# check if the linked list does not contain any values
	if self.head is None:
		# meaning that there are not data present in linked list
		# therefore, raise a little 'IndexError'
		raise IndexError("\n\t<< Linked List Empty!!! > > \n")

	# if the linked list is not empty ==> perform `pop` and `append` operations

	# declare new linked list that will hold the reverse
	new_linked_list: LinkedList = LinkedList()

	# intialise pointer that is going to point to the "current" node
	current_node_ptr = self.head

	# check if the linked list has only one node present inside
	if current_node_ptr.next is None:
		# meaning that we do only have one node inside ==> simply `append` to new linked list
		new_linked_list.append(current_node_ptr.data)
		
		# finally return the new list to the "main" program
		return new_linked_list

	# else if the linked list has more than 1 nodes
	else:
		# iterate through the linked list until no nodes are present
		while len(self) != 0:
			# therefore remove the last node using the `pop` method
			popped_data = self.pop()

			# add the new data to the new linked list using the `append` method
			new_linked_list.append(popped_data)

		# finally, return the new linked list when the original linked list empty
		return new_linked_list
```

### Reverse ( Iterative ) Method ( Not In-Place ) Usage

```python
# method 1: using `new_list_reverse` method "directly"
my_llist.new_list_reverse()

# method 2: using `new_list_reverse` method inside a `try... except` block
# exception handling for reversing of linked list using the `new_list_reverse` method
try:
	# reverse the linked list
	my_llist.new_list_reverse()

# if index has not been found
except IndexError:
	# output appropriate message
	print("\n" + "-" * 50)
	print("\t   << Index Error!!! > > ")
	print("-" * 50)
```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!