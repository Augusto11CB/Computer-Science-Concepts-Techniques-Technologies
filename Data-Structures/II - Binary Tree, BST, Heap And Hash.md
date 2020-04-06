# Overview of Data Structures | Binary Tree, BST, Heap And Hash - II 

## Sumary
1. Binary Tree
2. Binary Search Tree
3. Binary Heap
4. Hashing

### Array Time Complexity

### Array - Advantages and Disadvantages 

### Example of Queue Usages

### Code Snippets

## Binary Tree
Differently from Arrays, queues, stacks that are linear data structures, **trees** are **hierarchical data structures**.

A specifically for binary tree case, **each one of its nodes has at most two children**.

### Binary Tree Structure
A tree is represented by a pointer to the topmost node in the tree (root).
- Data
- Pointer to left child
- Pointer to right child

### Ways to Traversed Binary Tree
- Depth First Traversal
	- Inorder (Left-Root-Right) 
	- Preorder (Root-Left-Right) 
	- Postorder (Left-Right-Root)
- Breadth First Traversal

### Properties
- The maximum number of nodes at level ‘l’ = 2l-1.
- least number of nodes  =2h+1
- Maximum number of nodes = 2^(h + 1) – 1.
Here h is height of a tree. Height is considered 
as the maximum number of edges on a path from root to leaf.

### Time Complexity
- Time Complexity of Tree Traversal: O(n)

### Advantages and Disadvantages 

### Example of Usages
One reason to use binary tree or tree in general is for the things that form a hierarchy. They are useful in File structures where each file is located in a particular directory and there is a specific hierarchy associated with files and directories. Another example where Trees are useful is storing heirarchical objects like JavaScript Document Object Model considers HTML page as a tree with nesting of tags as parent child relations.

### Code Snippets

## Binary Search Tree
A Binary Search Tree is a Binary Tree with following additional properties:
1. The left subtree of a node contains only nodes with **keys less than the node’s key.**  
2. The right subtree of a node contains only nodes with k**eys greater than the node’s key.**  
3. The left and right subtree each must also be a binary search tree.

### Properties
If Binary Search Tree is Height Balanced, then **h = O(Log n)**

### Time Complexity
- Search :  O(h)
- Insertion : O(h)
- Deletion : O(h)
- Extra Space : O(n) for pointers
**h** is the height of the tree
**n** Number of nodes


### Advantages and Disadvantages 
- BST provide moderate access/search (quicker than Linked List and slower than arrays).  
- BST provide moderate insertion/deletion (quicker than Arrays and slower than Linked Lists).

### Example of Usages
Its main use is in search application where data is constantly entering/leaving and data needs to printed in sorted order. For example in implementation in E- commerce websites where a new product is added or product goes out of stock and all products are lised in sorted order.

### Code Snippets

## Binary Heap
Binary heap is defined as a binary tree with two additional constraints

- Shape property: a binary heap is a complete binary tree; that is, all levels of the tree, except possibly the last one (deepest) are fully filled, and, if the last level of the tree is not complete, the nodes of that level are filled from left to right.
- the key stored in each node is either greater than or equal to (≥) or less than or equal to (≤) the keys in the node's children, according to some total order.

## Type of Binary Heaps
Heaps where the **parent key is greater than or equal to (≥) the child keys** are called _max-heaps_; those where it is **less than or equal to (≤)** are called _min-heaps_.

### Time Complexity
et Minimum in Min Heap: O(1) [Or Get Max in Max Heap]
Extract Minimum Min Heap: O(Log n) [Or Extract Max in Max Heap]
Decrease Key in Min Heap: O(Log n)  [Or Decrease Key in Max Heap]
Insert: O(Log n) 
Delete: O(Log n)

### Example of Usages
Used in implementing efficient priority-queues, which in turn are used for scheduling processes in operating systems. Priority Queues are also used in Dijstra’s and Prim’s graph algorithms.  
The Heap data structure can be used to efficiently find the k smallest (or largest) elements in an array, merging k sorted arrays, median of a stream, etc.  
Heap is a special data structure and it cannot be used for searching of a particular element.

### Code Snippets

## Hashing

### Hash Function 
A function that converts a given big input key to a small practical integer value.

A good hash function satisfies two basic properties: 
1) it should be very fast to compute 
2) it should minimize duplication of output values (collisions).

### Hash Tables
Hash functions are used in conjunction with Hash table to store and retrieve data items or data records.

The hash function translates the key associated with each record into a hash code which is used to index the hash table.

When an item is to be added to the table, the hash code may index an empty slot (also called a bucket), in which case the item is added to the table there. However, if the hash code indexes a full slot there are some approaches to deal with collison.
Following are the ways to handle collisions:
- _chained hashing_, each slot is the head of a linked list or chain, and items that collide at the slot are added to the chain. Chains may be kept in random order and searched linearly, or in serial order, or as a self-ordering list by frequency to speed up access.
- In open address hashing, the table is probed starting from the occupied slot in a specified manner, usually by linear probing, quadratic probing, or double hashing until an open slot is located or the entire table is probed (overflow). Searching for the item follows the same procedure until the item is located, an open slot is found or the entire table has been searched (item not in table).

### Time Complexity
- Space : O(n)
- Search    : O(1) [Average]    O(n) [Worst case]
- Insertion : O(1) [Average]    O(n) [Worst Case]
- Deletion  : O(1) [Average]    O(n) [Worst Case]

### Advantages and Disadvantages 
Hashing seems better than BST for all the operations. But in hashing, elements are unordered and in BST elements are stored in an ordered manner. Also BST is easy to implement but hash functions can sometimes be very complex to generate. In BST, we can also efficiently find floor and ceil of values.

### Example of Usages
Hashing can be used to remove duplicates from a set of elements. Can also be used find frequency of all items. For example, in web browsers, we can check visited urls using hashing. In firewalls, we can use hashing to detect spam. We need to hash IP addresses. Hashing can be used in any situation where want search() insert() and delete() in O(1) time.


## References
Wikipedia
[https://www.geeksforgeeks.org/overview-of-data-structures-set-2-binary-tree-bst-heap-and-hash/#code6](https://www.geeksforgeeks.org/overview-of-data-structures-set-2-binary-tree-bst-heap-and-hash/#code6)
