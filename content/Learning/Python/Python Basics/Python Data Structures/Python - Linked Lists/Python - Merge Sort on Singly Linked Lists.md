---
id: Python - Merge Sort on Singly Linked Lists
aliases: Implementation of Merge Sort on Singly Linked Lists in Python
tags:
  - python
  - algos
  - sorting
  - lists
  - oop
author: S.Sunhaloo
date: 2025-10-12
status: Completed
---

## List of Contents

- [[#Find Middle Node Of Linked List]]
- [[#Merge Sort Algorithm Implementation On Singly Linked List]]

---

> [!INFO]
> For more information on the **implementation** of Linked Lists in Python. Please refer to the file / note '[[Python - Singly Linked Lists]]'
>
> > [!INFO] Online Resource(s)
> > - https://leetcode.doocs.org/en/lc/148
> > - https://www.youtube.com/watch?v=TGveA1oFhrc
> > - https://www.youtube.com/watch?v=pNTc1bM1z-4
>

# Find Middle Node Of Linked List

To get the **middle** *node* of a Linked List, we are going to have to keep **two** pointers that will be initialised at the `self.head`!

We keep a `slow` pointer that moves by **one** ( *next* ) node each time and a `fast` pointer that moves by **two** ( *next* ) node each time!

> [!TIP]
> > This is actually so genius!
>
> As the fast node arrived at the **end** of the linked list... Logically speaking, the `slow` node will be pointing to the <strong> <span style="color: orange;"> middle</span> </strong> node!

```python
# method to find the middle node of a linked list of "any" size
def get_middle(self):
	# initialise our `slow` and `fast` pointers at the head of linked list
	slow_ptr = fast_ptr = self.head

	# check if the there is data at `fast` and its neighbour also has data
	while fast_ptr and fast_ptr.next:
		# change to the current pointer's neighbour
		slow_ptr = slow_ptr.next
		# change the to current pointer's neighbour's neighbour
		fast_ptr = fast_ptr.next.next

	# finally return the middle node itself
	return slow_ptr
```

# Merge Sort Algorithm Implementation On Singly Linked List

> [!NOTE]
> The *method* that is found below is the version that NeetCode showed in the above *linked* video.
>
> But his method is basically the **same** thing as the code found on 'leetcode.docs.org'!
>
> > He simply just created other *helper* function instead of writing everything inside the same function!
>
> But as I am creating my **own** Linked List `class`... I am going to implement these *helper* functions **outside** the `merge_sort` function!
>
> > Below you are going to find the code for the *helper* methods and the `merge_sort` method itself!
>

> [!WARNING]
> Given that LeetCode implementation of Linked List is a bit **different** from my implementation... There are somethings that are going to be **changed**!
>
> For example, the above `get_middle` function is going to work but we are going to have to modify it for it to actually work on our `LinkedList` *class*!

```python
# method to find the middle node of a linked list of "any" size ( given the head )
def get_middle(self, head):
	# check if the head itself is empty
	if head is None:
		# return the head itself
		return head

	# initialise our `slow` pointer at the head of linked list
	slow_ptr = head
	# initialise our `slow` pointer at the head's neighbour
	fast_ptr = head.next

	# check if the there is data at `fast` and its neighbour also has data
	while fast_ptr and fast_ptr.next:
		# change to the current pointer's neighbour
		slow_ptr = slow_ptr.next
		# change the to current pointer's neighbour's neighbour
		fast_ptr = fast_ptr.next.next

	# finally return the middle node of the linked list
	return slow_ptr

# "conquer" method to merge the individual nodes / data in orderly manner
def merge(self, left_part, right_part):
	# NOTE: create dummy / temporary `Node` so we don't have to check for edge cases
	tail_ptr = dummy_ptr = Node(0)

	# iterate through until we don't have data in our left and right part
	# INFO: the "merge" code below is literally the same as for arrays
	while left_part and right_part:
		# if the left part of the linked list value is smaller than right
		if left_part.data < right_part.data:
			# if so ==> swap the data
			tail_ptr.next = left_part
			left_part = left_part.next

		# if the right part of the linked list value is smaller than left
		else:
			tail_ptr.next = right_part
			right_part = right_part.next

		# change the current position of `tail_ptr` to the next node
		tail_ptr = tail_ptr.next

	# similarly... if there are any data left present inside left part
	if left_part:
		# add the remaining sorted data items into the linked list
		tail_ptr.next = left_part

	# similarly... if there are any data left present inside right part
	if right_part:
		# add the remaining sorted data items into the linked list
		tail_ptr.next = right_part

	# finally return "that" sorted linked list
	return dummy_ptr.next

# "divide" method that is going to recursively divide the linked list into halves
def merge_sort(self):
	# helper function so that we can go away without creating new linked list
	def merge_sort_helper(head):
		# check for the base case ==> if current head and neighbour is empty
		if (not head) or (not head.next):
			# return the head itself
			return head

		# split the linked list into halves until only one data is left

		# therefore, get the middle of the linked list ==> end of left ( part ) linked list
		mid_node = self.get_middle(head)
		# hence, get the start of the right ( part ) linked list
		right_part_head = mid_node.next

		# thus break the linkage to have two seperate linked list
		mid_node.next = None

		# call the function on the smaller linked list created
		left_part_llist = merge_sort_helper(head)
		right_part_llist = merge_sort_helper(right_part_head)

		# call the `merge` function to merge the data in order
		return self.merge(left_part_llist, right_part_llist)

	# finally return the sorted ( in-place ) linked list
	self.head = merge_sort_helper(self.head)
```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!