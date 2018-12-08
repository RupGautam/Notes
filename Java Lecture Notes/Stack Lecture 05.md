## Stacks 

**Stack**:  Stack are collections of an object that interested and removed according to last-in first-out LIFO principle.

#### The Stack ADT 

A stack is a LIFO sequence. Adding and remove takes place only at one end, called at top. 

![stack.gif](https://i.stack.imgur.com/fUtR1.png)

[Source](https://stackoverflow.com/questions/10974922/what-is-the-basic-difference-between-stack-and-queue)

**Main stacks operations are:**

​	`push(e)`: inserts and element 

​	`pop()`: removes and return the last inserted element

**Auxiliary stack operations are:**

​	`top()`: returns the last inserted element without removing it

​	`int size()`: return the number of elements stored

​	`isEmpty()`: indicates whether no element is stored

**The built-in Java Stack Interface**

This is the example of `java.util.Stack` 
```java
public interface Stack<E>{
    int size();
    boolean isEmpty();
    void push(E e);
    E pop();
    E top();
}
```
The difference between*built-in*  VS * own Stack* is that; If stack is empty in built-in class it  throws exception error, whereas, our own Stack ADT will return null. Our own ADT defines what the data type holds (int, string or custom values etc.). 

#### Implementing a stack with Array 

```java
public class ArrayStack<E> implements Stack<E>{
    public static final int CAPS = 100; //maxs space 
    private E[] STACK; //stack to hold the elements
    private int top = -1; //top must element 
    private int size = 0; //size of a array
	//constructors
    public ArrayStack(){ this(CAPS);}
    public ArrayStack(int caps){
        STACK = (E[]) new Object(caps);
    }
    public int size(){ return top + 1;}
    public boolean isEmpty(){ return size == 0;}
    public void push(E e){
        if(size == STACK.length) throw new StackOverflowError("StackOverflowError");
        STACK[top] = top + 1;
        size ++;
        STACK[top] = e;
    }
    public E pop(){
    	if(isEmpty()) return null;
    	E popped = STACK[top];
    	STACK[top] = null;
    	size --;
    	return popped; 
    }
}
```

#### Analyzing array-based stack 

All of the above implementation runs in constant time 

`size()`: $\mathcal{O}(1)$

`isEmpty()`: $\mathcal{O}(1)$

`top()`: $\mathcal{O}(1)$

`push()`: $\mathcal{O}(1)$

`pop()`: $\mathcal{O}(1)$

#### What are the drawback of array-based stack?

One disadvantage of using an array to implement a stack if the wasted space -- most of the time most of the array is unused. You must assume a fixed upper bound capacity on the ultimate size of the stack. 

#### Implementing a stack with a singly linked list

The advantage of using singly linked list is that the linked-list approach has a memory usage that is always proportional to the number of actual elements currently in stack, this make efficient use of memory. Unlike array-based implementation, the linked-list approach has memory usage that is always proportional to the number of actual elements in the current stack without arbitrary capacity limit. 

#### The adapter pattern 

It allow us to effectively want to modify an existing class so that its methods match those of a related, but different, class of interface

-  Define a new class that contains an instance of the existing class as a hidden field, then implement each method of the new class using methods of this hidden instance variable
- Creates a new class that performs some of the same functions as an existing class, but repackaged in a more convenient way


| Stack methods        | SLL methods           |
| ------------- |:-------------:|
| `size()`      | `list.size()` |
| `isEmpty()`      | `list.isEmpty()`      |
| `push(e)` | `list.addFirst(e)`      |
|  `pop(e)`	  | `list.removeFirst(e)`				|
|  `top(e)`			|  `list.first()`			|

**Implementing a stack with a singly linked list**

```java
public class LinkedStack<E> implements Stack<E>{
    private SinglyLinkedList<E> list = new SinglyLinkedList<>();
    public LinkedStack(){} //empty constructor 
	public int size() { return list.size();} 
	public boolean isEmpty() { return list.isEmpty() == 0;}
	public E pop(){ return list.removeFirst();}
	public E top() { return list.first();}
}
```

**Reversing and array with Stack**

Create an empty Stack `buffer`for storage, push all of the array elements onto the stack, and then `pop()` those element off of original Stack `arr` while overwritting the cells of the array from beginning to end 

$arr[ a ,  b ,  c,  d] --> buffer[ a ,  b ,  c , d] --> arr[ d ,  c ,  b , a]$

```java
public static<E> void reverse(E[] arr){
    Stack<E> buffer = new ArrayStack<>(arr.length) 
    for(int i =0; i < arr.length; i++)
    	buffer.push(arr[i]);
    for(int i =0; i < arr.length; i++)
    	arr[i] = buffer.pop();
}
```



