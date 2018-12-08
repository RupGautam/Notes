## Queues

### Queues

A Queue is FIFO sequence. It is close "cousin" of Stack but adding takes place only at `tail` and removal take place only at the `head`. 

This is the example of representation of Queue 

![queues.png](https://i.stack.imgur.com/CqutZ.png)

[source](https://stackoverflow.com/questions/10974922/what-is-the-basic-difference-between-stack-and-queue)

**The basic operations are: **
​	`enqueue(e)`: Inserts elements at the end of the queue
​	`dequeue()`: Removes and returns the elements from the front of the queue
​	`first()`: Returns the element from the front without removing it 
​	`size()`: Returns the number of elements stored
​	`isEmpty()`: Indicates whether no elements are sto

This is the example of Queue interface`java.util.Queue`

```java
public interface Queue<E>{
    int size();
    boolean isEmpty();
    void enqueue(E e);
    E first();
    E dequeue();
}
```

From the above built-in class, `first()`and `dequeue()` will return `null` if the stack is empty.

### The Queues ADT

#### Implementing a queue with a Array-based 

If we were to store elements on array $array = {\{a , b, c, d, . . . n-1\}}$ such that first element is at index `0`  and second at `1` and so on.

In Queue cases we need to dequeue element to Queue another element, which mean we need to remove the element that is at `0`. To accomplish this we can remove the element at index `0`but then, we would have to shift all other element one cell to the left. This will result in $\mathcal{O}(n)$ runtime 

TODO: ask about page #259 and slide #35

This implementation of Queue ADT using fixed-length array

```java
public class ArrayQueue<E> implements Queue<E>{
    private E[] data; //store
    private int f = 0; //front index element 
    private int size = 0; // current number of element
    public ArrayQueue(){ this(CAPACITY);}
    public ArrayQueue(int caps){data = (E[]) new Object[caps];}
    public int size() { return size;}
    public boolean isEmpty() {return size == 0;}
    public void enqueue(E e) throw IllegalStateException {
        if(size == data.length); // throw Queue is full 
        int available = (f + size) % data.length;
        // f = (f + size) % n 
        data[available] = e; 
        size ++;
    }
    public E first(){ 
        if(isEmpty()) return null; 
     	return data[f];}
    public E dequeue(){
        if(isEmpty()) return null;
        E popped = data[f];
        data[f] = null;
        f = (f + 1) % data.length;
        size --;
        return popped;
    }
}
```

**Analysis**
Looping through the `N` number of element results in $\mathcal{O(1)}$. Limited by array size and queue method executes a constant number of statements. Hence, all of the method `isEmpty()`, `first()`, `enqueue()`, `dequeue()` results in $\mathcal{O(1)}$ 

#### Implementing a queue with a Singly linked list

```java
public class LinkedQueue<E> implements Queue<E>{
    private SinglyLinkedList<E> list = new SinglyLinkedList<>();
    public LinkedQueue(){}
    public int size(){ return list.size();}
    public boolean isEmpty(){ return list.isEmpty();}
    public void enqueue(E e){ list.addLast(e);}
    public E first() { return list.first();}
    public E dequeue() {return list.removeFirst();}
}
```

**Analysis**

Singly linked list implementation runs on $\mathcal{O(1)}$ runtime. We also avoid the need to specify a capacity of queue size compare to array-based queue.Because eacho nodes stores a next reference, in addition to the element reference, a linked list uses more space per element than a properly sized array of references.

 It sound very effective but both implemenation involves large number of primitive operations per call. 

For example at array-base queue consists primarily of calculating an index with modular arithmetic, storing the element in the array cell, and incrementing the size counter. 

${\mathcal f = (f + size)  \%  n }$  

Another example at linked list, an insertion includes the instantiation and initialization of a new node, relinking an existing node to the new node, and incrementing the size counter.  

Deletions at the tail of a singly linked list cannot be done in constant time. 





## DEQUES

### DEQUES: Double-ended queues

A deque, also known as double-ended queues, is an ordered collection of items similar to the queue. It has two ends, a front and a rear, and the items remain positioned in the collections. It supports removing and adding element from both front and a rear end. 

![A deque of Python data objects](https://bradfieldcs.com/algos/deques/introduction/figures/basic-deque.png)

[*Content credit*](https://bradfieldcs.com/algos/deques/introduction/)

**Main queue operations:**

`addFirst()`: inserts elements at front of the deque

`addLast()`: inserts elements at the end of the deque

`removeFirst()`: removes and returns the first element of the deque

`removeLast()`: removes and returns the last element of the deque

**Auxiliary deque operations:**

`first()`: returns the first element without removing it

`last()`: returns the last element without removing it

`size()`: returns the number of elements stored

`isEmpty()`: indicates whether no elements are stored

This is the Deque interface from `java.util.deque`

```java
public interface Deque<E>{
    int size();
    boolean isEmpty();
    E first(); 
    E last();
    void addFirst(E e);
    void addLast(E e);
    E removeFirst();
    E removeLast();
}
```

To implement a deque, it requires insertion and removal at both ends of a list, using a singly linked list to implement a deque would be inefficient. So, implementing a deque using doubly linked list would be efficient and removing and adding element at either end of a doubly would be $\mathcal{O(1)}$ runtime.