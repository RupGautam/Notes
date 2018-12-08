## Linked List:
Linked can provide alternative to an array-based structure, linked list is in its simpliest form of nodes that is collectively form a linear sequence. 

#### Singly Linked List:
Singly linked list is a concrete data structure consisting of a sequence of nodes (elements) starting from head pointer. 

```java 
public class SinglyLinkedList<E> {
	private static class Node<E> {
	private E element;
	private Node<E> next;
	public Node(E e, Node<E> n) {
	element = e;
	next = n;
	}
	public E getElement() { return element; }
	public Node<E> getNext() { return next; }
	public void setNext(Node<E> n) { next = n; }
	}
}
```

##### Inserting element at the head:

```java
Algorithm addFirst(e)	
	newest = Node(e)
    #create new node instance storing reference to element e 
    newest.next = head
    #set new node's next to reference the old head node 
    head = newest 
    #set variable head to reference the new node 
    size ++ 
    #increase the node count 
```

##### Inserting element at the tail:

```java
Algorithm addLast(e)
    newest = Node(e)
    #create new node instance storing reference to element e 
    newest.next = null
    #set new node's next ref to null for garbage collector 
    tail.next = newest
    #make old tail node to point to new node
    tail = newest 
    #set variable tail to ref the new node
    size ++
    #increase the node count 
```

##### Removing element:
Removing an element at tail of singly linked list is not easy, because it is time consuming to remove any node other than the head. To remove tail we would have to go through every element is the list to get to the tail 
```java
Algorithm removeFirst(e)
	if head == null then 
	#if head is null then list must be empty, no nothing 
	the list is empty
	head == head.next
	#point current head to next node
	size --; 
	#decrease the node count
```

#### Doubly Linked List:

Special Doubly linked list can traversed forward and backward, node stores *element, previous node and next node.* 

Header node is the head of the list, and tailer node is tail of the list. 

```java
public class DoublyLinkedList<E> {
    private static class Node<E> {
    private E element;
    private Node<E> prev;
    private Node<E> next;
    public Node(E e, Node<E> p, Node<E> n) {
    element = e;
    prev = p;
    next = n;
}
    public E getElement() { return element; }
    public Node<E> getPrev() { return prev; }
    public Node<E> getNext() { return next; }
    public Node<E> setPrev(Node<E> p) { prev = p; } 
    public void setNext(Node<E> n) { next = n; }
    }
}
```

##### DoublyLinked List must have:

```java
# This are the method, that we must have 
size() # return size of list 
isEmpty() # test if list is empty 
first() # return the first element of the list 
last() # return the last element of the list 
addFirst() # add element at first position 
addLast() # add element at last position
removeFirst() # remove the first element
removeLast() # remove the last element
addBetween() # add element in between 
remove() # removes the node and returns 
```
