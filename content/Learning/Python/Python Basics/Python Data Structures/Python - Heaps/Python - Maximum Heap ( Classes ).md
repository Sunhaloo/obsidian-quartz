---
id: Python - Maximum Heap ( Classes )
aliases: Max-Heap ( Priority Queue - Abstract Data Type  ) implemented using Python Classes
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

- [[#Creation Of Maximum Heap Class]]
- [[#Function / Method Related To Maximum Heap]]
  - [[#Data Insertion Methods]]
		- [[#Sift Up Private Method]]
		- [[#Insert Method]]
		- [[#Meld Method]]
	- [[#Data Removal Methods]]
		- [[#Sift Down Private Method]]
		- [[#Extract Maximum Method]]
	- [[#Miscellaneous Methods]]
		- [[#Length Of Heap]]
		- [[#Display / Print Heap]]
		- [[#Peek The Maximum Value / Root]]
		- [[#Private Parent Method]]
		- [[#Private Left Child Method]]
		- [[#Private Right Child Method]]
		- [[#Heapify Method]]
- [[#Creation Of Maximum Heap and Usage]]

---

> [!NOTE]
> This is note is only going to show about the implementation of the **Maximum Heap** *data structure* using Python classes.
> 
> Please refer to online resources or even use Large Language Models to learn more about 'Heaps' in general.

---

> [!INFO] Resource(s)
> 
> - [[Python - Minimum Heap ( Classes )]]

> [!INFO]
> Yes, I did **use** the implementation of the `MinHeap` to make this note right here!
> 
> Therefore, if you want to; take a look at the above note whereby *I* implemented the `MinHeap`...

---

# Creation Of Maximum Heap Class

```python
# our max-heap class
class MaxHeap:
    # our constructor method
    def __init__(self):
        # initialise our "heap"
        # INFO: you could also say that its an "array" / list implementation of heap
        self.heap = []
```

- Therefore to create some Heaps, we can simply create our objects of class `MaxHeap`:

```python
# our main function
def main():
    # create our first max-heap
    heap: MaxHeap = MaxHeap()

    # create our second max-heap
    second_heap: MaxHeap = MaxHeap()


if __name__ == "__main__":
    main()
```

---

> [!WARNING]
> As you know by now, in Python there are **no strict** ways to enforce '*private*' methods like in other programming languages such as [[Java Data View | Java]].
> 
> Therefore, how can we *have* **private methods** in this codebase?
> 
> Therefore, we do a little **gentleman's agreement** whereby, if we write a function / method that starts with and `_` character. For example, `_some_method` or `_helper_function`...
> 
> We as **programmers**, are going to agree that we **won't** use this method *outside* the **current** `class`. Therefore, this is the reason as to why we "*can*" have **_"private"_ methods** in Python!

---

# Function / Method Related To Maximum Heap

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

In this case, 'sift-up' means moving a node **up** the heap while its *key* is **larger** than its *parent*, until the max-heap *property* is **restored**.

```python
# ( "private" ) method to sift-up data into correct position
def _sift_up(self, index):
	# call the "private" `_parent` method to find the parent of the `index`
	parent_idx = self._parent(index)

	# iterate through binary tree until max-heap quality is achieved
	# NOTE: here are some conditions that we are going to have to follow
	# 1. continue to iterate if the `parent_idx` is not `None`
	# 2. continue while the current node's key is larger than its parent's key

	# WARNING: we need to do `[parent_idx][0]` as our data are in a tuple
	# and that tuple is in the form of `(key, value)` --> see `insert` method
	while parent_idx is not None and self.heap[parent_idx][0] < self.heap[index][0]:
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
def meld_max_heap(self, other_max_heap):
	# combine the "original" heap with the new heap
	combined_heap = self.heap + other_max_heap.heap

	# call the `heapify_max` method to ensure max-heap property is satisfied
	self.heapify_max(combined_heap)

	# INFO: following Neural Nine's...
	# "really absorb the elements of the other heap"
	other_max_heap.heap = []
```

> [!TIP]- Time Complexity = O(n + m)
> - The **overall** *running* time complexity for this method is going to be O(n + m)
> - Best Case: O(n + m)
> 	- Runs through **all** *parent* nodes even if heap **already** satisfies heap *property*
> - Worst Case: O(n + m)
> 	- Occurs when *many* nodes needs to be **moved**

## Data Removal Methods

### Sift Down Private Method

In this case, 'sift-down' means moving a node **down** the heap while its *key* is **smaller** than **one** or **both** of its *children*, swapping with the **larger** *child* each time, until the max-heap *property* is **restored**.

```python
# ( "private" ) method to sift-down data into correct position
def _sift_down(self, index):
	# iterate through binary tree until max-heap quality is achieved
	while True:
		# initialise the largest index
		largest_idx = index

		# try to get the left or right child or both
		left_child_idx = self._left_child(index)
		right_child_idx = self._right_child(index)

		# NOTE: here are some conditions that we are going to have to follow
		# for both when we are checking for the right / left child
		# 1. right / left child does contain data
		# 2. data inside the right / left child is larger than that of "parent" node
		# again, as we are dealing with tuples... We have to access like so.

		if (
			left_child_idx is not None
			and self.heap[left_child_idx][0] > self.heap[largest_idx][0]
		):
			# if so ==> swap the indices with each other
			largest_idx = left_child_idx

		if (
			right_child_idx is not None
			and self.heap[right_child_idx][0] > self.heap[largest_idx][0]
		):
			# if so ==> swap the indices with each other
			largest_idx = right_child_idx

		# condition to stop ==> max-heap property has been reached
		if largest_idx == index:
			break

		# actually swap the nodes with each other at comparison until "found"
		self.heap[index], self.heap[largest_idx] = (
			self.heap[largest_idx],
			self.heap[index],
		)

		# finally, change the `index` to the `largest_idx`
		# so that we get the updated index for next iteration
		index = largest_idx
```

> [!TIP]- Time Complexity = O(log n)
> - The **overall** *running* time complexity for this method is going to be O(log n)
> - Best Case: O(1)
> 	- Occurs when the *initial position* of the newly added node is **correct**
> - Worst Case: O(log n)
> 	- Occurs when the new node has *lowest* priority and therefore has to *travel* / swap all the way *from* the **root** node *to* the **leaf** node

### Extract Maximum Method

```python
# method to extract / remove the maximum "node" from the heap
def extract_max_root(self):
	# check if the heap / "array" contains any data
	if not self.heap:
		raise IndexError("\n\t<< Empty Heap!!! >>\n")

	# find the maximum element which is always at the front ( index: 0 )
	maximum_element = self.heap[0]

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

	# finally, return the maximum ( "previous" root ) element
	return maximum_element
```

> [!TIP]- Time Complexity = O(log n)
> - The **overall** *running* time complexity for this method is going to be O(log n)
> - Best Case: O(1)
> 	- Occurs when the heap has **only** *one* element or *new root* is already **larger** than both of its *children*
> - Worst Case: O(log n)
> 	- Occurs when the new node has *lowest* priority and therefore has to *travel* / swap all the way *from* the **root** node *to* the **leaf** node

## Miscellaneous Methods

### Length Of Heap

> This function is also going to work with *Min-Heaps*!

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

> This function is also going to work with *Min-Heaps*!

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

### Peek The Maximum Value / Root

> This function is also going to work with *Min-Heaps*... Just need to change the `maximum` **comment**!

```python
# method to peek / see the maximum element / "root node"
def peek_max_root(self):
	# check if the heap / "array" contains any data
	if not self.heap:
		raise IndexError("\n\t<< Empty Heap!!! >>\n")

	# return / see the first element as the first is always maximum
	return self.heap[0]
```

> [!TIP]- Time Complexity = O(1)
> - The **overall** *running* time complexity for this method is going to be O(1)
> - Best Case: O(1)
> - Worst Case: O(1)
> 
> > I think you get the point as to why this is actually $O(1)$ even for the *worst* cast right?

---

> [!TIP]
> Let's say that we have a **maximum _heap_** ( *or `list`* ) that looks like this: `[55, 44, 33, 16, 5]`.
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

> This function is also going to work with *Min-Heaps*!

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
> # ( "private" ) method to find the "parent" of a "node" ( Neural Nine )
> def _parent(self, index):
> 	# find the parent of a "node" while the index is not equal to '0'
> 	return ((index - 1) // 2) if index != 0 else None
> ```
> 
> But this might cause us some issues if we **negative** indices, which Python does support...
> 
> Therefore, in my eyes; it makes much *more sense* to use `> 0` **instead** of `!= 0`

### Private Left Child Method

> This function is also going to work with *Min-Heaps*!

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

### Private Right Child Method

> This function is also going to work with *Min-Heaps*!

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

> This function is also going to work with *Min-Heaps*!

```python
# method to convert an array / list of elements ( the tuples ) into a max-heap
def heapify_max(self, elements):
	# convert the elements into the heap
	# WARNING: this is going to remove the original data ( "the tuples" )
	# that you originally inserted into the heap!
	self.heap = list(elements)

	# iterate through all parent nodes ( from last parent to first )
	# call "private" `_sift_down` on each to ensure the max-heap property is satisfied
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

# Creation Of Maximum Heap and Usage

Here is simple, example of what we get when we combine all of these functions above.

> [!INFO]
> I hard-coded the input and deletion; but you can easily use a `for` loop to create another *simple* function if you want to allow for user input!

> [!WARNING]
> This 'Maximum Heap' implementation will work with **all** data types!
> 
> I just chose to use '`str`ings' for the **actual** `value` and the `key` to be `int`eger numbers!

```python
# our max-heap class
class MaxHeap:
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

    # method to peek / see the maximum element / "root node"
    def peek_max_root(self):
        # check if the heap / "array" contains any data
        if not self.heap:
            raise IndexError("\n\t<< Empty Heap!!! >>\n")

        # return / see the first element as the first is always maximum
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

        # iterate through binary tree until max-heap quality is achieved
        # NOTE: here are some conditions that we are going to have to follow
        # 1. continue to iterate if the `parent_idx` is not `None`
        # 2. continue while the current node's key is larger than its parent's key

        # WARNING: we need to do `[parent_idx][0]` as our data are in a tuple
        # and that tuple is in the form of `(key, value)` --> see `insert` method
        while parent_idx is not None and self.heap[parent_idx][0] < self.heap[index][0]:
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
        # iterate through binary tree until max-heap quality is achieved
        while True:
            # initialise the largest index
            largest_idx = index

            # try to get the left or right child or both
            left_child_idx = self._left_child(index)
            right_child_idx = self._right_child(index)

            # NOTE: here are some conditions that we are going to have to follow
            # for both when we are checking for the right / left child
            # 1. right / left child does contain data
            # 2. data inside the right / left child is larger than that of "parent" node
            # again, as we are dealing with tuples... We have to access like so.

            if (
                left_child_idx is not None
                and self.heap[left_child_idx][0] > self.heap[largest_idx][0]
            ):
                # if so ==> swap the indices with each other
                largest_idx = left_child_idx

            if (
                right_child_idx is not None
                and self.heap[right_child_idx][0] > self.heap[largest_idx][0]
            ):
                # if so ==> swap the indices with each other
                largest_idx = right_child_idx

            # condition to stop ==> max-heap property has been reached
            if largest_idx == index:
                break

            # actually swap the nodes with each other at comparison until "found"
            self.heap[index], self.heap[largest_idx] = (
                self.heap[largest_idx],
                self.heap[index],
            )

            # finally, change the `index` to the `largest_idx`
            # so that we get the updated index for next iteration
            index = largest_idx

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

    # method to extract / remove the maximum "node" from the heap
    def extract_max_root(self):
        # check if the heap / "array" contains any data
        if not self.heap:
            raise IndexError("\n\t<< Empty Heap!!! >>\n")

        # find the maximum element which is always at the front ( index: 0 )
        maximum_element = self.heap[0]

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

        # finally, return the maximum ( "previous" root ) element
        return maximum_element

    # method to convert an array / list of elements ( the tuples ) into a max-heap
    def heapify_max(self, elements):
        # convert the elements into the heap
        # WARNING: this is going to remove the original data ( "the tuples" )
        # that you originally inserted into the heap!
        self.heap = list(elements)

        # iterate through all parent nodes ( from last parent to first )
        # call "private" `_sift_down` on each to ensure the max-heap property is satisfied
        for i in reversed(range(self._parent(len(self.heap) - 1) + 1)):
            self._sift_down(i)

    # method to combine another heap's list with the "current" heap
    def meld_max_heap(self, other_max_heap):
        # combine the "original" heap with the new heap
        combined_heap = self.heap + other_max_heap.heap

        # call the `heapify_max` method to ensure max-heap property is satisfied
        self.heapify_max(combined_heap)

        # INFO: following Neural Nine's...
        # "really absorb the elements of the other heap"
        other_max_heap.heap = []


# our main function
def main():
    # create our max-heap
    drivers_heap: MaxHeap = MaxHeap()

    # insert data using the `insert` method into the max-heap
    drivers_heap.insert(44, "Lewis Hamilton")
    drivers_heap.insert(1, "Max Verstappen")
    drivers_heap.insert(33, "Max Verstappen")
    drivers_heap.insert(3, "Daniel Ricciardo")
    drivers_heap.insert(4, "Lando Norris")
    drivers_heap.insert(14, "Fernando Alonso")

    print("\n\t -- After Insertion --\n")

    # display the max-heap using the `__repr__` dunder method
    print(drivers_heap.heap)

    print("\n\t -- Find Length Of Racing Driver Heap --\n")

    # find the length of the max-heap using the `__len__` dunder method
    print(f"Length of Racing Drivers Heap: {len(drivers_heap)}")

    # extract the maximum root using the `extract_max_root` method
    extracted = drivers_heap.extract_max_root()

    print("\n\t -- Extracting Maximum Node ==> Root Node --\n")

    print(f"Extracted Maximum Root: {extracted}")

    print("\n\t -- After Extraction --\n")

    # display the max-heap after extraction
    print(drivers_heap.heap)

    print("\n\t -- Parent and Children --\n")

    # find the parent of index 1 using the `_parent` method
    print(f"Parent of index 1: {drivers_heap._parent(1)}")

    # find the left child of index 1 using the `_left_child` method
    print(f"Left child of index 1: {drivers_heap._left_child(1)}")

    # find the right child of index 1 using the `_right_child` method
    print(f"Right child of index 1: {drivers_heap._right_child(1)}")

    # create our riders max-heap using the heapify method
    riders_heap: MaxHeap = MaxHeap()

    # convert array / list of elements into a max-heap using the `heapify_max` method
    riders_heap.heapify_max(
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

    # create our combined max-heap
    goated_racers_max_heap: MaxHeap = MaxHeap()

    # convert drivers heap into max-heap
    goated_racers_max_heap.heapify_max(drivers_heap.heap)

    # combine the riders heap with the drivers heap using the `meld_max_heap` method
    goated_racers_max_heap.meld_max_heap(riders_heap)

    print("\n\t -- Goated Racers (combined) --\n")

    # display the combined heap
    print(goated_racers_max_heap.heap)

    print("\n\t -- Find Length Of Racing Riders Heap --\n")

    # find the length of the combined heap
    print(f"Length of Racing Riders Heap: {len(goated_racers_max_heap)}")


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