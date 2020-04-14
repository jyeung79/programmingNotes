# Data Structures

Going through the books Competitive Programmer's Handbook, Elements of Programming Interviews in Java & Cracking the Coding Interview.
    - Competitive Programmer's is the most concise and clear out of them all
    - Elements of Programming Interview as from what majority people agrees > Cracking the Coding Interview
Going through the Coursera course from Princeton University: Algorithms I & Algorithms II

The most commonly used Data Structures are:
| Data Structures     	| Summary                                                                                                                                                                                                                                                                         	|
|---------------------	|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
| Primitives          	| <ul><li>These are the int, char, double</li><li>In Javascript, these are Number, String, Boolean, Undefined, Null</li></ul>                                                                                                                                                                         	|
| Arrays              	| <ul><li>Fast access for element at an index</li><li>Slow lookups and insertion; unless sorted - Know iteration, resizing, partitioning, merging (resizing & partitioning is relevant for C++ or Java not Javascript)</li></ul>                                                                        	|
| Strings             	| <ul><li>Understand basic operators such as comparison, copy, matching, joining, splitting</li></ul>                                                                                                                                                                                             	|
| Lists               	| <ul><li>Tradeoffs vs Arrays</li><li>Iteration, insertion, deletions in a singly-linked and doubly-linked list</li><li>Dynamic allocation of a lists and with arrays</li></ul>                                                                                                                               	|
| Stacks & Queues     	| <ul><li>LIFO (stacks) vs FIFO (queues)</li><li>Stacking plates to be washed and lining up for the newest iphone</li><li>Array and Linked-list implementation</ul>                                                                                                                                       	|
| Binary Trees        	| <ul><li>Used to represent hierachical data</li><li>Depth, height, leaves, search path, traversal sequences, successor/predecessor operation</li></ul>                                                                                                                                                 	|
| Heaps               	| <ul><li>Key benefit: O(1) lookup find-max</li><li>O(logn) insertion; O(logn) deletion of max</li><li>Node and array implementation</li><li>Min-heap variant</li></ul>                                                                                                                                           	|
| Hash Tables         	| <ul><li>Key benefit: O(1) insertions, deletions and lookups</li><li>Key Disadvantage: Not suitable for order-related quieries; need for resizing; poor worst-case performances</li><li>Array of buckets & collision chains implementation</li><li>Know hash functions for integers, strings and objects</li></ul> 	|
| Binary Search Trees 	| <ul><li>Key benefit: O(log n) insertions, deletions, lookups, find-min, find-max, successor, predessor when tree is height-balanced</li><li>Understand node fields, pointer implementation(not needed for JS)</li><li>Be familiar with the notion of balance, and operations maintaining balance</li></ul>  	|

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

### Algorithm Patterns
Algorithm Design Patterns beneficial to solving interview problems can be split into two catgories
    1. Analysis Patterns
        1. Concrete Examples
        2. Case Analysis
        3. Iterative Refinement
        4. Reduction
        5. Graph Modeling
    2. Algorithm Design Patterns
        1. Sorting
        2. Recursion
        3. Divide-and-Conquer
        4. Dynamic Programming
        5. Greedy Algorithms
        6. Invariants

## Analysis Patterns
### 1. Concrete Examples
Problems that seem too difficult can be become more tractable when you examine concrete examples.
    i. Small Inputs such as BST with 5-7 inputs
    ii. Extreme/Specialized INputs ie. binary values, nonoverlapping intervals, sorted arrays, connected graphs

Problems: Smallest Non Constructible Value Problem
The smallest non constructible value is where the added number u > V + 1 where V is the maximum constructible number (sum of all values). V+1 becomes the largest value that we cannot produce. Loop over a sorted array and stop when the condition of u > V + 1 is met.

ie) <1,2,4> -> 1,2,3,4,5,6,7 -> V = 8 and if u = 10 is added then V + 1= 9 is the largest non constructible value 

### 2. Case Analysis
Problems can be split into a number of separate cases. Examine all possible cases. They do not have to be mutally exclusive but must be exhaustive to cover all possibilities.

### 3. Iterative Refinement
Oftentime most algorithms can be solved in a brute-force, exhaustive search and generate-and-test method.

### 4. Reduction
Trying to make harder, more complex problems and reduce it into a easier problem. Sometimes, you need to reduce a problem known to be difficult to the given problem, justifying heuristics and approximate solutions.

Problem: Determine if one string is a rotation of the other one
ie) "car" and "arc" are rotations of each other. Brute-force rotate every char in first string to match results in O(n^2). However reduce it into a string search problem. Concat the second string to itself and them search 1st string in the 2nd string. Find a match and they are rotations of each other. O(n^2) becomes O(n) problem.

### 5. Graph Modeling
Drawing pictures are a great way to brainstorm for a potential solution. If the relationship can be represented by a graph, then quite often it can be reduced to a well-known graph problem.

Problem: Want to determine if an arbitrage exists with a given set of currencies. Basically, you want to make the most money converting money around.
ie) 1 USD -> 1 x 0.8123 = 0.8123 EUR -> 0.8123 x 1.2010 = CHF ... = 1.00385 USD

This is a graph problem where G = (V, E)
    - V is the set of vertices; represents the currencies
    - E is the set of edges; represents exchanges
    - Edge Weight represents the log(exchange rate)

Use Bellman-Ford algorithm

## Algorithm Design Patterns
### 1. Sorting
Sorting can make certain problems easier to understand and solve when the input is sorted. However, it may not be clear at first what should be sorted. 

Sorting is not appropriate when <= O(n) algorithm is possible. Sometimes sorting can obsfuscate the problem.

### 2. Recursion
Recursive function consists of base cases and calls to the same functino with different arguements
Appropriate scenarios may include:
    - Searching
    - Enumeration
    - Divide-And-Conquer
    - Decomposing a complex problem into a set of similar smaller instances

### 3. Divide-And-Conquer
Decomposes a problem into 2 or more smaller independent subproblems until it gets to instances where they are simple enough to be solved directly. Afterwards the results are then combined all together.

Q: How is this different from recursion?
Divide-and-conquer is usually implemented with recursion however, recursion is more general and subproblems do not have to be the same form

ie) 21 Triomino in a 8 x 8 Mboard with a top-left square piece gone. Subproblem with the top left square missing is different from others with a smaller n x n board.

### 4. Dynamic Programming
Dynamic Programming can be used when the problem has "optimal substructure: Possible to reconstruct a solution to the given instance from solutions to subinstances of smaller problems
A key aspect of DP is maintaining a cache of solutions to subinstances. Can be done recursively(stored in hash table or BST) or iteratively (one or multi-dimensional array). Typically DP
problems are implemented by recursion but most of the time, iteration may be more efficient.

ie) Fibonacci numbers can be solved typically 3 ways
    i) Brute Force O(2^n) 
    ii) Recursion O(n)
    iii) Bottom Up O(n) but does not overflow callback stack

### 5. Greedy Algorithms
Where you make decisions that are locally optimal but you never change them. This does not always result in the most optimal solution. Also there may be multiple greedy algorithms for a 
given problem but only some of them are optimal.

### 6. Invariants
Invariants is a condition that is true during execution. A variable or control logic may be set true in order to rule out potential solution that are suboptimal.

Invariants can also be used to analyze a given algorithm, prove correctness or analyze time complexity.



### Data Structure Operations Complexity*

| Data Structure          | Access    | Search    | Insertion | Deletion  | Comments  |
| ----------------------- | :-------: | :-------: | :-------: | :-------: | :-------- |
| **Array**               | 1         | n         | n         | n         |           |
| **Stack**               | n         | n         | 1         | 1         |           |
| **Queue**               | n         | n         | 1         | 1         |           |
| **Linked List**         | n         | n         | 1         | n         |           |
| **Hash Table**          | -         | n         | n         | n         | In case of perfect hash function costs would be O(1) |
| **Binary Search Tree**  | n         | n         | n         | n         | In case of balanced tree costs would be O(log(n)) |
| **B-Tree**              | log(n)    | log(n)    | log(n)    | log(n)    |           |
| **Red-Black Tree**      | log(n)    | log(n)    | log(n)    | log(n)    |           |
| **AVL Tree**            | log(n)    | log(n)    | log(n)    | log(n)    |           |
| **Bloom Filter**        | -         | 1         | 1         | -         | False positives are possible while searching |

### Array Sorting Algorithms Complexity*

| Name                  | Best            | Average             | Worst               | Memory    | Stable    | Comments  |
| --------------------- | :-------------: | :-----------------: | :-----------------: | :-------: | :-------: | :-------- |
| **Bubble sort**       | n               | n<sup>2</sup>       | n<sup>2</sup>       | 1         | Yes       |           |
| **Insertion sort**    | n               | n<sup>2</sup>       | n<sup>2</sup>       | 1         | Yes       |           |
| **Selection sort**    | n<sup>2</sup>   | n<sup>2</sup>       | n<sup>2</sup>       | 1         | No        |           |
| **Heap sort**         | n&nbsp;log(n)   | n&nbsp;log(n)       | n&nbsp;log(n)       | 1         | No        |           |
| **Merge sort**        | n&nbsp;log(n)   | n&nbsp;log(n)       | n&nbsp;log(n)       | n         | Yes       |           |
| **Quick sort**        | n&nbsp;log(n)   | n&nbsp;log(n)       | n<sup>2</sup>       | log(n)    | No        | Quicksort is usually done in-place with O(log(n)) stack space |
| **Shell sort**        | n&nbsp;log(n)   | depends on gap sequence   | n&nbsp;(log(n))<sup>2</sup>  | 1         | No         |           |
| **Counting sort**     | n + r           | n + r               | n + r               | n + r     | Yes       | r - biggest number in array |
| **Radix sort**        | n * k           | n * k               | n * k               | n + k     | Yes       | k - length of longest key |

*Taken from [Javacript Algorithms and Data Structures](https://github.com/trekhleb/javascript-algorithms)

## 0. Time & Space Complexity
Time complexity is denoted by a O(...) where the ... refers to the function; n denotes the input size.

### Loops
If there are k nested loops, the time complexity becomes O(n<sup>k</sup>).

### Order of Magnitude
Time complexity does not tell us the exact number of times the code is ran but it gives us a general idea of the order of magnitude of the computation.

### Phases
If an algorithm contains multiple phases, subcomponents of algorithms, then the total time complexity becomes the largest time complexity of a single phase. This is because
the slowest phase is usually the bottleneck of the code.

As shown below, out of the three time complexities O(n), O(n^2) and O(n), O(n^2) is the slowest thus the total time complexity is O(n^2).
```javascript
for (int i = 1; i <= n; i++) {
// O(n)
}
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n; j++) {
    // O(n^2)
    }
}
for (int i = 1; i <= n; i++) {
// O(n)
}
```

### Several Variables
If the time complexity contains multiple variables then include them in the time complexity.

```javascript
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= m; j++) {
    // O(n x m) time complexity
    }
}
```

### Recursion
The time complexity of a recursive function depends on
    - number of times the function is called
    - the time complexity of a single call.

```javascript
const f( n) {
    if (n == 1) return;
    f(n-1);
}
```
Here, the single call is only O(1) and since there are n number of function calls, the time complexity becomes O(n).

However, if you have a higher time complexity of a call then the total time complexity drastically increases.

```javascript
const g(n) {
    if (n == 1) return;
    g(n-1); // Have 2 call to a recursive functio
    g(n-1);
}
```
Each function call generates two other calls except for n = 1. Thus there is a exponentially increasing amount of call 2<sup>n</sup>.

|function call| num of calls  |
|---|---|
| g(n)  |  1 |
| g(n-1)  | 2  |
| g(n-2)  | 4  |
| ...  | ...  |
| g(1)  |  2<sup>n</sup> - 1 |

This means that the time complexity becomes O(2<sup>n</sup>).

### Commplexity classes
The following list contains the common time complexities


#### O(log(n)) - Constant Time
The running-time of the algorithm does not depend on the input size. A typical constant-time algorithm directly calculates an answer.

#### O(n&nbsp;log(n)) - Logarithmic Time
Logarithmic algorithm often halves the input size at each step. Running time is logarithmic because log<sub>2</sub>n represetns the number of times
n must be divided by 2 to get 1.

#### O($\sqrt{n}$) - Square Root
Slower than logarithmic algorithms but faster than O(n). A special property of square roots is that $\sqrt{n}$) = n/$\sqrt{n}$), so square root $\sqrt{n}$) lies
somewhere in the middle of the input.  

#### O(n) - Linear Time
Given a n input size, the running time is O(n) because the algorithm has to access each input element at least once before reporting the answer.
Usually the best possible time complexity.

#### O(n&nbsp;logn) - n&nbsp;log(n) Time
Either the algorithm has to sort the input because efficient sorting algorithms take O(n&nbsp;log(n)) time complexity or
the data structure's operations take O(log(n)) time.

#### O(n<sup>2</sup>)
Often contains 2 nested loops.

#### O(2<sup>n</sup>)
This algorithm iterates all subsets of the input element. For example the subsets of {1, 2, 3} are 
null, {1}, {2}, {3}, {1,2}, {1,3}, {2,3} and {1,2,3}.

#### O(n!)
This algorithm iterates through all permutations of the input element. For example, the permutations of
{1,2,3} are (1,2,3), (1,3,2), (2,1,3), (2,3,1), (3,1,2) and (3,2,1}.


An algorithm is polynomial if its time complexity is at most O(n<sup>k</sup>) where k = constant. (O(2<sup>n</sup> and O(n!) are not)
Usually k is small so polynomial time complexity roughly means the algorithm is efficient.


### Estimating Efficiency
Before implementing an algorithm, we can figure out if its efficient enough for the problem by calculating the time complexity.

Given the input size, we can try to guess the required time complexity of the algorithm that solves the problem. The table below contains
some userful estimates assuming time limit of one second.

|input size     | required time complexity  |
|:--------------|--------------------------|
|n ≤ 10     | O(n!)  |
|n ≤ 20     | O(2<su>n</sup>)  |
|n ≤ 500    | O(n<sup>3</sup>)    |
|n ≤ 5000   | O(n<sup>2</sup>)   |
|n ≤ 106    | O(n&nbsp;logn) or O(n)  |
|n is large | O(1) or O(logn)  |

This helps to design algorithms because it eliminates approaches with worst time complexity.
* Note: Time complexity is an approximation because it hides away the constant factor. In real applications, there are differing effects on computation speeds because
of the constant factor.