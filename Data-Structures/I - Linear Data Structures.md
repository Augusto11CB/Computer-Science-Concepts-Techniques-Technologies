
# Overview of Data Structures | Linear Data Structures - I
A data structure is a particular way of organizing data in a computer so that it can be used effectively. The idea is to reduce the space and time complexities of different tasks.

## Sumary
1. Array
2. Linked List
3. Stack
4. Queue

## Array
Array is a data structure for storing more than one data item of the same type. The items of an array are allocated at  adjacent memory locations which are called **elements**.

-   **Element**  − Each item stored in an array is called an element.
    
-   **Index**  − Each location of an element in an array has a numerical index, which is used to identify the element.

### Array Time Complexity
- Accessing Time: 
	- O(1) [his is because any element can be instantly read using indexes]   
- Search Time:   
	- O(n) for Sequential Search: 
	- O(log n) for Binary Search [If Array is sorted]
- Insertion Time: 
	- O(n) [The worst case occurs when insertion at the Beginning of an array and shifting all of the elements]
- Deletion Time: 
	- O(n) [The worst case occurs when deletion happens at the Beginning of an array and shifting all of the elements]

### Array - Advantages and Disadvantages 
**Disadvantages** 
1. While using array, we must need to make the decision of the size of the array in the beginning, so if we are not aware how many elements we are going to store in array, it would make the task difficult.

2. The size of the array is fixed so if at later point, if we need to store more elements in it then it can’t be done. On the other hand, if we store less number of elements than the declared size, the remaining allocated memory is wasted.


### Example of Queue Usages

### Code Snippets

## Linked List
The linked list is comprising of two items - the data and a reference to the next node.

Types of Linked List:
1. Single Linked List
**Characteristic**: In this type of linked list, every node stores address or reference of next node in list and the last node has next address or reference as NULL

2. Doubly Linked List
**Characteristics**: each node has two references, one of the references points to the next node and the other to the previous node. **Advantage** of this type is that it is possible to traverse in both directions and for deletions, there is no need to have explicit access to the previous node.

3. Circular Linked List
**Characteristics**: In this type, the end of the list points to the first element of the list. This structure can be single or doubly-linked. **Advantages** are that any node can be made as starting node. 

### Linked List  Time Complexity
- Acessing time of an element: O(n)
- Searching time of an element: O(n)
- Insertion of an element: O(1) [If it is in the position where the insertion have to be made]
- Deletion of an element: O(1) [If it is known the address of the previous node of the node to be deleted]
- 
### Array - Advantages and Disadvantages 
**Disadvantages**
One drawback of linked list is, random access is not allowed. With arrays, we can access i’th element in O(1) time.

### Example of Queue Usages

### Code Snippets
```java
public class SinglyLinkedList {

      public void addLast(SinglyLinkedListNode newNode) {

            if (newNode == null)

                  return;
            else {

                  newNode.next = null;

                  if (head == null) {

                        head = newNode;
                        tail = newNode;
                  } else {

                        tail.next = newNode;
                        tail = newNode;
                  }
            }
      } 

      public void addFirst(SinglyLinkedListNode newNode) {

            if (newNode == null)

                  return;
            else {

                  if (head == null) {

                        newNode.next = null;
                        head = newNode;
                        tail = newNode;
                  } else {

                        newNode.next = head; 
                        head = newNode;

                  }
            }
      } 

      public void insertAfter(SinglyLinkedListNode previous,

                  SinglyLinkedListNode newNode) {

            if (newNode == null)

                  return;

            else {

                  if (previous == null)

                        addFirst(newNode);

                  else if (previous == tail)

                        addLast(newNode);

                  else {

                        SinglyLinkedListNode next = previous.next;
                        previous.next = newNode;
                        newNode.next = next;

                  }
            }
      }
}
``` 

## Stack 
Stack works with the concept of "last in, first out". This structure serves as a collection of elements. The main operation to work with stacks are **push**(add elements) and **pop**(remove the last element inserted) 

### Stack List  Time Complexity
- Insertion : O(1)
- Deletion :  O(1)
- Access Time : O(n) [Worst Case]
- Insertion and Deletion are allowed on one end.

### Array - Advantages and Disadvantages 

### Example Stack Usages
Stacks are used for maintaining function calls (the last called function must finish execution first), we can always remove recursion with the help of stacks. Stacks are also used in cases where we have to reverse a word, check for balanced parenthesis and in editors where the word you typed the last is the first to be removed when you use undo operation. Similarly, to implement back functionality in web browsers.

### Code Snippets

## Queue
Queue ~ FIFO ~ "first in, first out" works as a collection of elements which principal operations are: **enqueue** (process of add elements to the collection), and dequeue (process of removing the first element added)

### Stack List  Time Complexity
- Insertion : O(1)
- Deletion  : O(1)
- Access Time : O(n) [Worst Case]

### Array - Advantages and Disadvantages 

### Example of Queue Usages
Any situation where resources are shared among multiple users and served on first come first server basis. Examples include CPU scheduling, Disk Scheduling. Another **application of queue is when data is transferred asynchronously** (data not necessarily received at same rate as sent) between two processes. Examples include IO Buffers, pipes, file IO, etc.

### Code Snippets

## References
[https://www.geeksforgeeks.org/overview-of-data-structures-set-1-linear-data-structures/](https://www.geeksforgeeks.org/overview-of-data-structures-set-1-linear-data-structures/)
[https://www.tutorialspoint.com/data_structures_algorithms/array_data_structure.htm](https://www.tutorialspoint.com/data_structures_algorithms/array_data_structure.htm)
[https://beginnersbook.com/2018/10/data-structure-array/](https://beginnersbook.com/2018/10/data-structure-array/)
