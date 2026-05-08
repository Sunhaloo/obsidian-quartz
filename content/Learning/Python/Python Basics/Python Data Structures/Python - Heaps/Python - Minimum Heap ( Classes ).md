---
id: Python - Minimum Heap ( Classes )
aliases: Min-Heap ( Priority Queue - Abstract Data Type  ) implemented using Python Classes
tags:
  - arrays
  - bifo
  - binary-tree
  - data-structures
  - heap
  - lists
  - oop
  - python
  - queue
author: S.Sunhaloo
date: 2026-03-25
status: Completed
---

## List of Contents

- [[#Creation Of Minimum Heap Class]]
- [[#Function / Method Related To Minimum Heap]]
	- [[#Data Insertion Methods]]
		- [[#Sift Up Private Method]]
		- [[#Insert Method]]
		- [[#Meld Method]]
	- [[#Data Removal Methods]]
		- [[#Sift Down Private Method]]
		- [[#Extract Minimum Method]]
	- [[#Miscellaneous Methods]]
		- [[#Length Of Heap]]
		- [[#Display / Print Heap]]
		- [[#Peek The Minimum Value / Root]]
		- [[#Private Parent Method]]
		- [[#Private Left Child Method]]
		- [[#Private Right Child Method]]
		- [[#Heapify Method]]
- [[#Creation Of Minimum Heap and Usage]]

---

> [!NOTE]
> This is note is only going to show about the implementation of the **Minimum Heap** *data structure* using Python classes.
> 
> Please refer to online resources or even use Large Language Models to learn more about 'Heaps' in general.

> [!WARNING]
> As you know by now, in Python there are **no strict** ways to enforce '*private*' methods like in other programming languages such as [[Java Data View | Java]].
> 
> Therefore, how can we *have* **private methods** in this codebase?
> 
> Therefore, we do a little **gentleman's agreement** whereby, if we write a function / method that starts with and `_` character. For example, `_some_method` or `_helper_function`...
> 
> We as **programmers**, are going to agree that we **won't** use this method *outside* the **current** `class`. Therefore, this is the reason as to why we "*can*" have **_"private"_ methods** in Python!
> 
> > [!BUG]
> > As of today the 27/04/2026 @ 19:46; I found out that the using a **single** underscore `_` actually **conveys** the *meaning* of a **`protected`** *variable*, *function* / *method* in Python.
> > 
> > To **convey** the *meaning* of a **`private`**; we need to use **double** underscored `__`!
> > 
> > > Therefore, keep this in mind when you are reading through the content!

---

> [!INFO] Resource(s)
> 
> - Neural Nine: https://www.youtube.com/watch?v=wOouknH8RsY
> - [anbnyc](https://gist.github.com/anbnyc): https://gist.github.com/anbnyc/c8a8f91c64e1d7bd3e263124d25b4bd5
> - Medium Article: https://medium.com/@kyleanthonyhay/leetcode-min-heap-construction-61bea4ef9883

---

# Creation Of Minimum Heap Class

```python
# our min-heap class
class MinHeap:
    # our constructor method
    def __init__(self):
        # initialise our "heap"
        # INFO: you could also say that its an "array" / list implementation of heap
        self.heap = []
```

- Therefore to create some Heaps, we can simply create our objects of class `MinHeap`:

```python
# our main function
def main():
    # create our first min-heap
    heap: MinHeap = MinHeap()

    # create our second min-heap
    second_heap: MinHeap = MinHeap()


if __name__ == "__main__":
    main()
```

> Need I Say More?

---

> [!BUG]
> From our notes on '[[Python - Stacks ( Linked List )]]', we talked about; if you are accessing the **length** of the stack *frequently*.
> 
> Therefore, it makes complete sense that you create the `self.size` attribute when we are implementing the `Stack` class.
> 
> Therefore, I said to myself, let's try doing the **same** thing here!
> 
> Hence, I updated the `MinHeap` class definition by adding the following `size` attribute:
> 
> ```python
> # attribute to keep track of the length of the "array" / heap
> self.size = len(self.heap)
> ```
> 
> Therefore, I tried doing something like this:
> 
> > Remember in our `MinHeap` class, the `list` for `self.heap` is initially **empty**!
>
> ```python
> # create our first min-heap
> heap: MinHeap = MinHeap()
> 
> # update the heap / list
> heap.heap = [1, 2, 3, 4, 5]
> 
> # display the heap together with the size
> print(heap.heap, heap.size)
> ``` 
> 
> Therefore, we expect when to see `[1, 2, 3, 4, 5] 5` when we run the program right?
> 
> ```console
> [1, 2, 3, 4, 5] 0
> ```
> 
> > Yep! We get '0' for the length / value of `self.size` of the array!
> 
> > [!INFO]
> > This is simply because when we initially did "*declare and initialise*" the `self.size` inside the `MinHeap` class.
> > 
> > The `self.size = len(self.heap)` is only going to be *evaluated* **once** and given that initially, `self.heap = []`...
> > 
> > This means that we are **always** going to `return` '0' even if we do enter something in our heap after modifying the `heap` in our `main` function!
> 
> > *[The More You Know](https://www.youtube.com/watch?v=GD6qtc2_AQA)... Fuck Me... Stupid and Silly Mistakes*!
> 
> > [!TIP]
> > Additionally, its not like we are losing performance using the `__len__` *dunder* method here!
> > 
> > Compared to a **linked list** whereby iterating through is going to have a time complexity of $O(n)$ because of our pesky `while` loop...
> > 
> > We have **nothing** to *worry* about here as we are dealing with Python `list`s and therefore the `len` function is already optimised and hence $O(1)$ running time complexity

---

# Function / Method Related To Minimum Heap

> [!WARNING]
> You are going to see `key` a lot! Don't worry about it for now.
> 
> Just know that the `key` can only be `int`, `float` or `str`. This is because our data ( *for this "learning session"* ) is going to look like this: `(key, actual_data )`.
> 
> > Yes a [[Python - Tuples | tuple]] containing 2 values!
> 
> We need `key` to *form part* of these 3 data types above because we are going to be using the `key` for **comparison**!

## Data Insertion Methods

### Sift Up Private Method

In this case, 'sift-up' means moving a node **up** the heap while its *key* is **smaller** than its *parent*, until the min-heap *property* is **restored**.

```python
# ( "private" ) method to sift-up data into correct position
def _sift_up(self, index):
	# call the "private" `_parent` method to find the parent of the `index`
	parent_idx = self._parent(index)

	# iterate through binary tree until min-heap quality is achieved
	# NOTE: here are some conditions that we are going to have to follow
	# 1. continue to iterate if the `parent_idx` is not `None`
	# 2. continue while the current node's key is smaller than its parent's key

	# WARNING: we need to do `[parent_idx][0]` as our data are in a tuple
	# and that tuple is in the form of `(key, value)` --> see `insert` method
	while parent_idx is not None and self.heap[parent_idx][0] > self.heap[index][0]:
		# simply swap the position of the 2 "nodes"
		self.heap[index], self.heap[parent_idx] = (
			self.heap[parent_idx],
			self.heap[index],
		)

		# given that the position of the "nodes" have changed
		# we need to re-initialise the index of the parent
		index = parent_idx

		# finally call the "private" `_parent` method again to find new parent `index`
		parent_idx = self._parent(index)
```

> [!TIP]- Time Complexity = O(log n)
> - The **overall** *running* time complexity for this method is going to be O(log n)
> - Best Case: O(1)
> 	- Occurs when the *initial position* of the newly added node is **correct**
> - Worst Case: O(log n)
> 	- Occurs when the new node has *highest* priority and therefore has to *travel* / swap all the way to the **root** node

> [!TIP] The Swapping Part
> Normally, in a language like C or Java, you would do something like this:
> 
> > I am writing this in a way so that you can 'copy-paste' into the above code and run!
> 
> ```python
> 	# swap the current node with the parent node
> 	
> 	# store the current node temporarily
> 	temp = self.heap[index]
> 	# overwrite current node with the parent node
> 	self.heap[index] = self.heap[parent_idx]
> 	# place the parent node in "current" node's position
> 	self.heap[parent_idx] = temp
> ```
> But because we use Python and we are *snakes*, we can just **rattle** and **slither** our way and do the **same** thing like so:
> 
> ```python
> 	# swap the nodes using Python's tuple thingy
> 	self.heap[index], self.heap[parent_idx] = self.heap[parent_idx], self.heap[index]
> ```

### Insert Method

```python
# method to insert data at the end and then sift-up to correct position
def insert(self, key, value):
	# insert the "node" / key-value pair ( tuple ) to the heap
	self.heap.append((key, value))

	# call the "private" `_sift_up` method
	# INFO: as "node" might not necessarily be in the correct position
	# call `_sift_up` method to move that "node" into the "correct" position
	# ======================================================================
	# additionally, given that the last "node" added will always last...
	# we simply need to pass the index of the last "node"
	self._sift_up(len(self.heap) - 1)
```

> [!TIP]- Time Complexity = O(log n)
> - The **overall** *running* time complexity for this method is going to be O(log n)
> - Best Case: O(1)
> 	- Occurs when the *initial position* of the newly added node is **correct**
> - Worst Case: O(log n)
> 	- Occurs when the new node has *highest* priority and therefore has to *travel* / swap all the way to the **root** node

### Meld Method

```python
# method to combine another heap's list with the "current" heap
def meld_min_heap(self, other_min_heap):
	# combine the "original" heap with the new heap
	combined_heap = self.heap + other_min_heap.heap

	# call the `heapify_min` method to ensure min-heap property is satisfied
	self.heapify_min(combined_heap)

	# INFO: following Neural Nine's...
	# "really absorb the elements of the other heap"
	other_min_heap.heap = []
```

> [!TIP]- Time Complexity = O(n + m)
> - The **overall** *running* time complexity for this method is going to be O(n + m)
> - Best Case: O(n + m)
> 	- Runs through **all** *parent* nodes even if heap **already** satisfies heap *property*
> - Worst Case: O(n + m)
> 	- Occurs when *many* nodes needs to be **moved**

## Data Removal Methods

### Sift Down Private Method

In this case, 'sift-down' means moving a node **down** the heap while its *key* is **larger** than **one** or **both** of its *children*, swapping with the **smaller** *child* each time, until the min-heap *property* is **restored**.

```python
# ( "private" ) method to sift-down data into correct position
def _sift_down(self, index):
	# iterate through binary tree until min-heap quality is achieved
	while True:
		# initialise the smallest index
		smallest_idx = index

		# try to get the left or right child or both
		left_child_idx = self._left_child(index)
		right_child_idx = self._right_child(index)

		# NOTE: here are some conditions that we are going to have to follow
		# for both when we are checking for the right / left child
		# 1. right / left child does contain data
		# 2. data inside the right / left child is smaller than that of "parent" node
		# again, as we are dealing with tuples... We have to access like so.

		if (
			left_child_idx is not None
			and self.heap[left_child_idx][0] < self.heap[smallest_idx][0]
		):
			# if so ==> swap the indices with each other
			smallest_idx = left_child_idx

		if (
			right_child_idx is not None
			and self.heap[right_child_idx][0] < self.heap[smallest_idx][0]
		):
			# if so ==> swap the indices with each other
			smallest_idx = right_child_idx

		# condition to stop ==> min-heap property has been reached
		if smallest_idx == index:
			break

		# actually swap the nodes with each other at comparison until "found"
		self.heap[index], self.heap[smallest_idx] = (
			self.heap[smallest_idx],
			self.heap[index],
		)

		# finally, change the `index` to the `smallest_idx`
		# so that we get the updated index for next iteration
		index = smallest_idx
```

> [!TIP]- Time Complexity = O(log n)
> - The **overall** *running* time complexity for this method is going to be O(log n)
> - Best Case: O(1)
> 	- Occurs when the *initial position* of the newly added node is **correct**
> - Worst Case: O(log n)
> 	- Occurs when the new node has *lowest* priority and therefore has to *travel* / swap all the way *from* the **root** node *to* the **leaf** node

### Extract Minimum Method

```python
# method to extract / remove the minimum "node" from the heap
def extract_min_root(self):
	# check if the heap / "array" contains any data
	if not self.heap:
		raise IndexError("\n\t<< Empty Heap!!! >>\n")

	# find the minimum element which is always at the front ( index: 0 )
	minimum_element = self.heap[0]

	# get the last element from the heap / "array"
	last_element = self.heap.pop()

	# check if we have remaining data in the heap
	if self.heap:
		# therefore place the last element as the "root" node
		self.heap[0] = last_element

		# call the "private" `_sift_down` method
		# INFO: as "node" might not necessarily be in the correct position
		# call `_sift_down` method to move that "node" into the "correct" position
		self._sift_down(0)

	# finally, return the minimum ( "previous" root ) element
	return minimum_element
```

> [!TIP]- Time Complexity = O(log n)
> - The **overall** *running* time complexity for this method is going to be O(log n)
> - Best Case: O(1)
> 	- Occurs when the heap has **only** *one* element or *new root* is already **smaller** than both of its *children*
> - Worst Case: O(log n)
> 	- Occurs when the new node has *highest* priority and therefore has to *travel* / swap all the way *from* the **root** node *to* the **leaf** node

## Miscellaneous Methods

### Length Of Heap

> This function is also going to work with *Max-Heaps*!

```python
# ( dunder ) method to find the length of the heap using Python's `len` function
def __len__(self) -> int:
	return len(self.heap)
```

> [!TIP]- Time Complexity = O(1)
> - The **overall** *running* time complexity for this method is going to be O(1)
> - Best Case: O(1)
> - Worst Case: O(1)
> 
> > Simply because of the Python's `len` function implementation!

### Display / Print Heap

> This function is also going to work with *Max-Heaps*!

```python
# ( dunder ) method to display / print the heap / "array"
def __repr__(self) -> str:
	return str(self.heap)
```

> [!TIP]- Time Complexity = O(n)
> - The **overall** *running* time complexity for this method is going to be O(n)
> - Best Case: O(1)
> 	- Occurs when we **only** have *one* item in the heap / `list`
> - Worst Case: O(n)
> 	- Occurs when multiple items in the heap / `list`

### Peek The Minimum Value / Root

> This function is also going to work with *Max-Heaps*... Just need to change the `minimum` **comment**!

```python
# method to peek / see the minimum element / "root node"
def peek_min_root(self):
	# check if the heap / "array" contains any data
	if not self.heap:
		raise IndexError("\n\t<< Empty Heap!!! >>\n")

	# return / see the first element as the first is always minimum
	return self.heap[0]
```

> [!TIP]- Time Complexity = O(1)
> - The **overall** *running* time complexity for this method is going to be O(1)
> - Best Case: O(1)
> - Worst Case: O(1)
> 
> > I think you get the point as to why this is actually $O(1)$ even for the *worst* cast right?

---

> The `TIP` [callout](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#alerts) was *re-written* by [ChatGPT](https://chatgpt.com) after extensive chatting and re-writing of about 30 minutes... *Fuck My Life*!

> [!TIP]
> Let's say that we have a **minimum _heap_** ( *or `list`* ) that looks like this: `[5, 16, 33, 44, 55]`.
>
> We can use the above `list` to determine an *element's* **parent**, as well as its *left* and / or *right* **child(ren)**.
>
> Refer to the following *formulae*:
>
> - Parent: `(index - 1) // 2` whereby `index` should be **greater than `0`**
> - Left: `(2 * index) + 1`
> - Right: `(2 * index) + 2`
>
> If you are trying to find the *parent*, you **cannot** use index `0`.
>
> > This means you **must** use an index **greater than or equal to `1`**, since the *root node* has **no parent**.
>
> Similarly, if you are trying to find the *child* (left or right), you *can* start at the **last** index, but you **won't** get any children.
>
> This is because there is no more data, and the computed indices will fall outside the heap (or `list`).
>
> > In the above example, trying to find *children* at index `2` will yield **no valid indices**.
> 
> - Here is a little diagram for you to understand how to "*see*" the **parent** and the **children**.
> 
> ![[Minimum Heap - Relationship Representation.png | 300]]

### Private Parent Method

> This function is also going to work with *Max-Heaps*!

```python
# ( "private" ) method to find the parent of a "node"
def _parent(self, index) -> int | None:
	# find the parent of a "node" while the index is greater than '0'
	return ((index - 1) // 2) if index > 0 else None
```

> [!TIP]- Time Complexity = O(1)
> - The **overall** *running* time complexity for this method is going to be O(1)
> - Best Case: O(1)
> - Worst Case: O(1)
> 
> > Again, I think you get the point as to why this is actually $O(1)$ even for the *worst* cast right?

> [!WARNING]
> Neural Nine did **not** use `index > 0`... Instead he implemented the above "*private*" method like so:
> 
> ```python
> # ( "private" ) method to find the parent of a "node" ( Neural Nine )
> def _parent(self, index):
> 	# find the parent of a "node" while the index is not equal to '0'
> 	return ((index - 1) // 2) if index != 0 else None
> ```
> 
> But this might cause us some issues if we **negative** indices, which Python does support...
> 
> Therefore, in my eyes; it makes much *more sense* to use `> 0` **instead** of `!= 0`

### Private Left Method

> This function is also going to work with *Max-Heaps*!

```python
# ( "private" ) method to find the left child of a "node"
def _left_child(self, index) -> int | None:
	# calculate the index of the left child
	left_child_idx = (2 * index) + 1

	# return the correct index ==> depending of `index` provided
	return left_child_idx if left_child_idx < len(self.heap) else None
```

> [!TIP]- Time Complexity = O(1)
> - The **overall** *running* time complexity for this method is going to be O(1)
> - Best Case: O(1)
> - Worst Case: O(1)

### Private Right Method

> This function is also going to work with *Max-Heaps*!

```python
# ( "private" ) method to find the right child of a "node"
def _right_child(self, index) -> int | None:
	# calculate the index of the right child
	right_child_idx = (2 * index) + 2

	# return the correct index ==> depending of `index` provided
	return right_child_idx if right_child_idx < len(self.heap) else None
```

> [!TIP]- Time Complexity = O(1)
> - The **overall** *running* time complexity for this method is going to be O(1)
> - Best Case: O(1)
> - Worst Case: O(1)

### Heapify Method

> This function is also going to work with *Max-Heaps*!

```python
# method to convert an array / list of elements ( the tuples ) into a min-heap
def heapify_min(self, elements):
	# convert the elements into the heap
	# WARNING: this replaces the current heap with a copy of the input elements
	self.heap = list(elements)

	# iterate through all parent nodes ( from last parent to first )
	# call "private" `_sift_down` on each to ensure the min-heap property is satisfied
	for i in reversed(range(self._parent(len(self.heap) - 1) + 1)):
		self._sift_down(i)
```

> [!TIP]- Time Complexity = O(n)
> - The **overall** *running* time complexity for this method is going to be O(n)
> - Best Case: O(n)
> 	- Runs through **all** *parent* nodes even if heap **already** satisfies heap *property*
> - Worst Case: O(n)
> 	- Occurs when *many* nodes needs to be **moved**

---

# Creation Of Minimum Heap and Usage

Here is simple, example of what we get when we combine all of these functions above.

> [!INFO]
> I hard-coded the input and deletion; but you can easily use a `for` loop to create another *simple* function if you want to allow for user input!

> [!WARNING]
> This 'Minimum Heap' implementation will work with **all** data types!
> 
> I just chose to use '`str`ings' for the **actual** `value` and the `key` to be `int`eger numbers!

```python
# our min-heap class
class MinHeap:
    # our constructor method
    def __init__(self):
        # initialise our "heap"
        # INFO: you could also say that its an "array" / list implementation of heap
        self.heap = []

    # ( dunder ) method to find the length of the heap using Python's `len` function
    def __len__(self) -> int:
        return len(self.heap)

    # ( dunder ) method to display / print the heap / "array"
    def __repr__(self) -> str:
        return str(self.heap)

    # method to peek / see the minimum element / "root node"
    def peek_min_root(self):
        # check if the heap / "array" contains any data
        if not self.heap:
            raise IndexError("\n\t<< Empty Heap!!! >>\n")

        # return / see the first element as the first is always minimum
        return self.heap[0]

    # ( "private" ) method to find the parent of a "node"
    def _parent(self, index) -> int | None:
        # find the parent of a "node" while the index is greater than '0'
        return ((index - 1) // 2) if index > 0 else None

    # ( "private" ) method to find the left child of a "node"
    def _left_child(self, index) -> int | None:
        # calculate the index of the left child
        left_child_idx = (2 * index) + 1

        # return the correct index ==> depending of `index` provided
        return left_child_idx if left_child_idx < len(self.heap) else None

    # ( "private" ) method to find the right child of a "node"
    def _right_child(self, index) -> int | None:
        # calculate the index of the right child
        right_child_idx = (2 * index) + 2

        # return the correct index ==> depending of `index` provided
        return right_child_idx if right_child_idx < len(self.heap) else None

    # ( "private" ) method to sift-up data into correct position
    def _sift_up(self, index):
        # call the "private" `_parent` method to find the parent of the `index`
        parent_idx = self._parent(index)

        # iterate through binary tree until min-heap quality is achieved
        # NOTE: here are some conditions that we are going to have to follow
        # 1. continue to iterate if the `parent_idx` is not `None`
        # 2. continue while the current node's key is smaller than its parent's key

        # WARNING: we need to do `[parent_idx][0]` as our data are in a tuple
        # and that tuple is in the form of `(key, value)` --> see `insert` method
        while parent_idx is not None and self.heap[parent_idx][0] > self.heap[index][0]:
            # simply swap the position of the 2 "nodes"
            self.heap[index], self.heap[parent_idx] = (
                self.heap[parent_idx],
                self.heap[index],
            )

            # given that the position of the "nodes" have changed
            # we need to re-initialise the index of the parent
            index = parent_idx

            # finally call the "private" `_parent` method again to find new parent `index`
            parent_idx = self._parent(index)

    # ( "private" ) method to sift-down data into correct position
    def _sift_down(self, index):
        # iterate through binary tree until min-heap quality is achieved
        while True:
            # initialise the smallest index
            smallest_idx = index

            # try to get the left or right child or both
            left_child_idx = self._left_child(index)
            right_child_idx = self._right_child(index)

            # NOTE: here are some conditions that we are going to have to follow
            # for both when we are checking for the right / left child
            # 1. right / left child does contain data
            # 2. data inside the right / left child is smaller than that of "parent" node
            # again, as we are dealing with tuples... We have to access like so.

            if (
                left_child_idx is not None
                and self.heap[left_child_idx][0] < self.heap[smallest_idx][0]
            ):
                # if so ==> swap the indices with each other
                smallest_idx = left_child_idx

            if (
                right_child_idx is not None
                and self.heap[right_child_idx][0] < self.heap[smallest_idx][0]
            ):
                # if so ==> swap the indices with each other
                smallest_idx = right_child_idx

            # condition to stop ==> min-heap property has been reached
            if smallest_idx == index:
                break

            # actually swap the nodes with each other at comparison until "found"
            self.heap[index], self.heap[smallest_idx] = (
                self.heap[smallest_idx],
                self.heap[index],
            )

            # finally, change the `index` to the `smallest_idx`
            # so that we get the updated index for next iteration
            index = smallest_idx

    # method to insert data at the end and then sift-up to correct position
    def insert(self, key, value):
        # insert the "node" / key-value pair ( tuple ) to the heap
        self.heap.append((key, value))

        # call the "private" `_sift_up` method
        # INFO: as "node" might not necessarily be in the correct position
        # call `_sift_up` method to move that "node" into the "correct" position
        # ======================================================================
        # additionally, given that the last "node" added will always last...
        # we simply need to pass the index of the last "node"
        self._sift_up(len(self.heap) - 1)

    # method to extract / remove the minimum "node" from the heap
    def extract_min_root(self):
        # check if the heap / "array" contains any data
        if not self.heap:
            raise IndexError("\n\t<< Empty Heap!!! >>\n")

        # find the minimum element which is always at the front ( index: 0 )
        minimum_element = self.heap[0]

        # get the last element from the heap / "array"
        last_element = self.heap.pop()

        # check if we have remaining data in the heap
        if self.heap:
            # therefore place the last element as the "root" node
            self.heap[0] = last_element

            # call the "private" `_sift_down` method
            # INFO: as "node" might not necessarily be in the correct position
            # call `_sift_down` method to move that "node" into the "correct" position
            self._sift_down(0)

        # finally, return the minimum ( "previous" root ) element
        return minimum_element

    # method to convert an array / list of elements ( the tuples ) into a min-heap
    def heapify_min(self, elements):
        # convert the elements into the heap
		# WARNING: this replaces the current heap with a copy of the input elements
        self.heap = list(elements)

        # iterate through all parent nodes ( from last parent to first )
        # call "private" `_sift_down` on each to ensure the min-heap property is satisfied
        for i in reversed(range(self._parent(len(self.heap) - 1) + 1)):
            self._sift_down(i)

    # method to combine another heap's list with the "current" heap
    def meld_min_heap(self, other_min_heap):
        # combine the "original" heap with the new heap
        combined_heap = self.heap + other_min_heap.heap

        # call the `heapify_min` method to ensure min-heap property is satisfied
        self.heapify_min(combined_heap)

        # INFO: following Neural Nine's...
        # "really absorb the elements of the other heap"
        other_min_heap.heap = []


# our main function
def main():
    # create our min-heap
    drivers_heap: MinHeap = MinHeap()

    # insert data using the `insert` method into the min-heap
    drivers_heap.insert(44, "Lewis Hamilton")
    drivers_heap.insert(1, "Max Verstappen")
    drivers_heap.insert(33, "Max Verstappen")
    drivers_heap.insert(3, "Daniel Ricciardo")
    drivers_heap.insert(4, "Lando Norris")
    drivers_heap.insert(14, "Fernando Alonso")

    print("\n\t -- After Insertion --\n")

    # display the min-heap using the `__repr__` dunder method
    print(drivers_heap.heap)

    print("\n\t -- Find Length Of Racing Driver Heap --\n")

    # find the length of the min-heap using the `__len__` dunder method
    print(f"Length of Racing Drivers Heap: {len(drivers_heap)}")

    # extract the minimum root using the `extract_min_root` method
    extracted = drivers_heap.extract_min_root()

    print("\n\t -- Extracting Minimum Node ==> Root Node --\n")

    print(f"Extracted Minimum Root: {extracted}")

    print("\n\t -- After Extraction --\n")

    # display the min-heap after extraction
    print(drivers_heap.heap)

    print("\n\t -- Parent and Children --\n")

    # find the parent of index 1 using the `_parent` method
    print(f"Parent of index 1: {drivers_heap._parent(1)}")

    # find the left child of index 1 using the `_left_child` method
    print(f"Left child of index 1: {drivers_heap._left_child(1)}")

    # find the right child of index 1 using the `_right_child` method
    print(f"Right child of index 1: {drivers_heap._right_child(1)}")

    # create our riders min-heap using the heapify method
    riders_heap: MinHeap = MinHeap()

    # convert array / list of elements into a min-heap using the `heapify_min` method
    riders_heap.heapify_min(
        [
            (46, "Valentino Rossi"),
            (93, "Marc Marquez"),
            (27, "Dani Pedrosa"),
            (99, "Jorge Lorenzo"),
            (21, "Franco Morbidelli"),
            (20, "Maverick Vinales"),
        ]
    )

    print("\n\t -- Riders Heap (via heapify) --\n")

    # display the riders heap
    print(riders_heap.heap)

    # find the length of the riders heap
    print(len(riders_heap))

    # create our combined min-heap
    goated_racers_min_heap: MinHeap = MinHeap()

    # convert drivers heap into min-heap
    goated_racers_min_heap.heapify_min(drivers_heap.heap)

    # combine the riders heap with the drivers heap using the `meld_min_heap` method
    goated_racers_min_heap.meld_min_heap(riders_heap)

    print("\n\t -- Goated Racers (combined) --\n")

    # display the combined heap
    print(goated_racers_min_heap.heap)

    print("\n\t -- Find Length Of Racing Riders Heap --\n")

    # find the length of the combined heap
    print(f"Length of Racing Riders Heap: {len(goated_racers_min_heap)}")


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