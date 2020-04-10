# Data Structures

Going through the books Competitive Programmer's Handbook, Elements of Programming Interviews in Java & Cracking the Coding Interview.
    - Competitive Programmer's is the most concise and clear out of them all
    - Elements of Programming Interview as from what majority people agrees > Cracking the Coding Interview
Going through the Coursera course from Princeton University: Algorithms I & Algorithms II

The most commonly used Data Structures are:
| Data Structures     	| Summary                                                                                                                                                                                                                                                                         	|
|---------------------	|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
| Primitives          	| - These are the int, char, double - In Javascript, these are Number, String, Boolean, Undefined, Null                                                                                                                                                                           	|
| Arrays              	| - Fast access for element at an index - Slow lookups and insertion; unless sorted - Know iteration, resizing, partitioning, merging (resizing & partitioning is relevant for C++ or Java not Javascript)                                                                        	|
| Strings             	| - Understand basic operators such as comparison, copy, matching, joining, splitting                                                                                                                                                                                             	|
| Lists               	| - Tradeoffs vs Arrays - Iteration, insertion, deletions in a singly-linked and doubly-linked list - Dynamic allocation of a lists and with arrays                                                                                                                               	|
| Stacks & Queues     	| - LIFO (stacks) vs FIFO (queues); Stacking plates to be washed and lining up for the newest iphone - Array and Linked-list implementation                                                                                                                                       	|
| Binary Trees        	| - Used to represent hierachical data - Depth, height, leaves, search path, traversal sequences, successor/predecessor operation                                                                                                                                                 	|
| Heaps               	| - Key benefit: O(1) lookup find-max; O(logn) insertion; O(logn) deletion of max; - Node and array implementation; Min-heap variant                                                                                                                                              	|
| Hash Tables         	| - Key benefit: O(1) insertions, deletions and lookups - Key Disadvantage: Not suitable for order-related quieries; need for resizing; poor worst-case performances - Array of buckets & collision chains implementation - Know hash functions for integers, strings and objects 	|
| Binary Search Trees 	| - Key benefit: O(log n) insertions, deletions, lookups, find-min, find-max, successor, predessor when tree is height-balanced - Understand node fields, pointer implementation(not needed for JS) - Be familiar with the notion of balance, and operations maintaining balance  	|

### Basic Types
Computing the number of bits set to 1 in an integer-valued variable x
    - y = x & ~(x - 1) ```// & is the bit-wise AND operator and ~ is the bit-wise NOT operator
    - y is 1 at the lowest bit of x that is 1; all the rest is 0

Note: Problems involved with bit-level data are often asked in interviews. It's easy to introduce errors in bit level operation. (Is this true for Javascript where you don't necessarily operate at the bit-level?)

Famous Words: When you play with bits, expect to be bitten.

### Arrays
Arrays maps any primitive or data type in a range from [0, n-1]; n being the number of elements in an array. 

Problems may result when traversing beyond the array's range such as optimizing quicksort.

### Strings
Strings have indices as well but they are seperate because common operations such as comparison, joining, splitting, searching for substrings, replacing and parsing do not apply to arrays.

### Lists
Lists implements an ordered collection of values which may include repititions. Here we view lists as a collection of nodes that link to the next node, ie) singly-linked list vs ie) doubly-linked list with two links pointing to the next and prev node.

Similar to arrays because objects are in linear order. However, key differences are inserting and deleting elements are O(1) time complexity & obtaining kth element is O(n). List are usually the building blocks for more complex data structures.

### Stacks & Queues
Stacks(LIFO) and Queues(FIFO) are commonly implemented using arrays or linked lists. They are common building blocks for more complicated data structures.

### Binary Tree
Binary tree is a DS that represents hierarchical relationships. Commonly occur in the context of binary search trees, wherein keys are stored in a sorted fashion.
ie) A node may be locked iff nonde of its descendants and ancestors are locked

### Heaps
Heap, priority queue, is implemented with a binary tree. A heap is a queue with priority associated with each elemtn and deletion removes the element with the highest priority.

### Hash Tables
Hash tables is a data structure used to store keys and optionally values corresponding to the key.
Inserts, deletes and lookups run in O(1) on average. One caveat is that these operations require a good hash function, mapping all possible keys to integers. If the nubmer of keys that is stored is not known in advance, the hash table need to be periodically resized.

### Binary Search Trees
Stores objects that are comparable. The main focus is to organize the objects in an organized fashion where the nodes follow the BST property:
    - Left child is smaller than root & Right child is larger than root.
AVL & red-black trees are BST implementations that support this form of insertion and deletion.

BSTs are a workhorse of DS can be used to solve almost every DS problem reasonably efficiently. It is common to augment the BST to make ti possible to manipulate more complicated data i.e) intervals.

## 0. Time & Space Complexity


## 1. Primitves


## 2. Arrays


## 3. Strings


## 4. Linked Lists


## 5. Stacks & Queues


## 6. Binary Trees


## 7. Heaps


## 8. Searching


## 9. Hash Tables


## 10. Sorting


## 11. Binary Search Trees


## 12. Recursion


### Covered less often in Programming Interviews

## 13. Dynamic Programming


## 14. Greedy Algorithms & Invariants


## 15. Graphs


## 16. Parallel Computing