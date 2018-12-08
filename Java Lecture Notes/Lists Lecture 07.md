## Lists

### The Lists ADT

List abstract data type are consider a list to be a collection of items where each item holds a relative position with respect to the others. elements of lists are refered to as *nodes*. When each nodes holds reference to the next node in the list, we call this a singly linked list. When each nodes hold reference to next and previous nodes in the list, we call this a doubly linked list. 

**The main operation are:**

`size()`: Returns the number of elements in the list

`isEmpty`: Returns a boolean whether the list is empty

`get( i )`: Returns the element of the list having index *i*

`set( i, e )`: Replaces the elements at index *i* with *e*, returns the old element that it replaced

`add(i, e)`: Inserts a new element *e* into the list so that it has index *i*, moving all the subsequent elements one index later in the list, error if not in range

`remove( i )`: Removes and returns the element at index *i*, moving all the subsequent elements one index earlier in the list, error if not in range 

**The built-in java interface for Lists**

```java
public interface List<E>{
    int size();
    boolean isEmpty();
    E get(int i) throws IndexOutOfBoundsExceptions;
    E set(int i, E e) throws IndexOutOfBoundsExceptions;
    void add(int i, E e) throws IndexOutOfBoundsExceptions;
    E remove(int i) throws IndexOutOfBoundsExceptions;
}
```

#### Implementing a Lists with ArrayList

```java
public class ArrayList<E> implements List<E>{
    public static final int CAPACITY = 16;
    private E[] data;
    private int size = 0;
    //constructors 
    public ArrayList(){ this(CAPCITY);}
    public ArrayList(int capacity){
        data = (E[]) new Object[capacity];
    }
    //public methods
    public int size(){ return size; }
    public boolean isEmpty(){ return size == 0; }
    public E get(int i) throw IndexOutOfBoundsException {
        checkIndex(i, size);
        return data[i];
    }
    public E set(int i, E e) throw IndexOutOfBoundsException {
        checkIndex(i, size);
        E temp = data[i];
        data[i] = e;
        return temp;
    }
    public void add(int i, E e)throw IndexOutOfBoundsException {
        checkIndex(i, size + 1);
        if(size == data.length) throw new IllegalStateException("Array is Full");
        for(int k=size-1;k>=i;k--)
            data[k+1] = data[k];
        data[i] = e;
        size++;
    }
    public E remove(int i)throw IndexOutOfBoundsException {
        checkIndex(i, size);
        E temp = data[i];
        for(int k=i; k < size -1; k++)
            data[k] = data[k+1];
        data[size -1] = null;
        size --;
        return temp;
    }
    protected void checkIndex(int i, int n)throw IndexOutOfBoundsException{
        if(i < 0 || i >= n) throw new IndexOutOfBoundsException("Illegal index: "+i)
    }
}
```

| Methods  | Runtime          |
| -------- | ---------------- |
| `size()` | $\mathcal{O(1)}$ |
| `isEmpty()`| $\mathcal{O(1)}$|
| `get(i)`| $\mathcal{O(1)}$   |
| `set(i, e)` | $\mathcal{O(1)}$ |
| `add(i,e)`   | $\mathcal{O(n)}$ //because we need to shift the elements forward |
| `remove(i)` | $\mathcal{O(n)}$ //because we need to shift the elements backward |

**Analysis for ArrayList implementation**

Requires a fixed maxium capacity to be declared. Throws an exception if attempted to add an element once the array is full. Inefficient waste if memory if too large of an array is requested or a fatal error if exhausting the capacity of a array that was requested too small. 

#### Implementing a Dynamic Array

```java
protected void resize(int capacity){
    E[] temp = (E[]) new Object[capacity];
    for(int k=0; k<size; k++)
        temp[k] = data[k];
    data = temp;
}
//add method that resizes if the size == data.length
public void add(int i, E e) throw IndexOutOfBoundsException {
    checkIndex(i, size + 1);
    if(size == data.length)
        resize(2*data.length);
    for(int k=size-1; k>=i;k--)
        data[k+1] = data[k];
    data[i] = e;
    size ++;
}
```

