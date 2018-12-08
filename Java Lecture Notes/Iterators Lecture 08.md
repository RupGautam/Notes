## Iterators

#### Iterators 

An *Iterators*is a software design pattern that abstracts the process of scanning through a sequence of element, one element at a time.

Follow are the methods `java.util.Iterator` provides:

`hasNext()`: Returns true if there is at least one additional element in the sequence; return false otherwise

`next()`: Returns the next element in the sequence

##### Iterator interface

This is the `java.util.Iterator`interface 

```java
public interface Iterator<E>{
    boolean hasNext();
    E next();
    void remove(){ 
    	//
    }
    //
}
```

#### The Iterable interface 
A single iterator instance supports only one pass through a collection; there is no way to *reset*the iterator back to begining of the sequence. However, a data structure that wishies to allow repeated iterations can support a method that returns a new iterator, each time it is called 

#### Implementing Iterators
Generally there are two style to implement iterators:
##### Snapshot iterator
Maintains it own private copy or *snapshot* of the sequence of elements, which is constructed at the time the iterator object is created. 
*Advantage*: Simple and easy to implement, since it requires a simple traversal of the primary structure
*Disadvantage*: It requires $\mathcal O (n)$ run time and $\mathcal{ O (n)}$ auxiliary space, upon construction, to copy and store a collection of $n$ elements

##### Lazy iterator
Does not make an upfront copy, instead performing a traversal of primary structure only when `next()`method is called to request another element
*Advantage*: Is that is can typically be implemented so the iterator require only $\mathcal{O(1)}$ space and $\mathcal{O(1)}$ construction time
*Disadvantage*: Behaviour is affected if the primary structure is modified before the iteration completes

#### ArrayList iterator 

Add an `iterator()` method to that class defination, which return an instance of an object that implments the `Iterator<E>` interface

```java
ArrayList<String> names = new ArrayList<String>();
names.add("Steve");
names.add("John");
names.add("Jedi");

Iterator<Stirng> it = names.iterator();

while(it.hasNext()){
    String value = it.next();
    System.out.println(value);
}
#output should be ["steve", "John", "Jedi"]
```

```java
#nested ArrayIterator class 
private class ArrayIterator implements Iterator<E>{
    private int j =0;
    private boolean removable = false;
    public boolean hasNext(){ return j < size; }
    public E next()throws NoSuchElementException {
        if(j == size) throws NoSuchElementException("No next element");
        removable = true;
        return data[j++];
    }
    public void remove() throw IllegalStateException {
        if(!removeable) throw new IllegalStateException("Nothing to remove");
        ArrayList.this.remove( j - 1);
        j --;
        removable = false;
    }
}
 //returns an iterator of elements stored in the list
public Iterator<E> iterator(){
    return new ArrayIterator();
}
```



#### **LinkedPositionalList iterator**





#### HashMap iterator

```java
HashMap<Integer, String> maps = new HashMap<Integer, String>();
    maps.put(10, "John");
    maps.put(11,"Steve");
    maps.put(12,"Jedi");
    Iterator<Map.Entry<Integer, String>> iterator = maps.entrySet().iterator();
      while(iterator.hasNext()){
        Map.Entry it = iterator.next();
        System.out.print("[key: "+it.getKey() + "value: "+it.getValue()+" ]\n");
      }
#output: [key:11 value:Steve]
		 [key:10 value:Steve]
		 [key:12 value:John]
```

#### 
