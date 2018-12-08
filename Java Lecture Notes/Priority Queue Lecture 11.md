## Priority Queue 

We use the Entry type in the formal interface for priority queue, which allows us to return both a key and value as a single object from methods such as `min()` and `removeMin()`

```java
public interface Priority Queue {
    int size();
    boolean is isEmpty();
    Entry<K, V> insert(K key, V value)throw IllegalArgumentException;
    Entry<K,V> min();
    Entry<K,V> removeMin();
}
```

### Comparing Keys

#### Compareable interface

A class that is also known as the *natural ordering* of its instances by formally implementing the `java.lang.Comparable` interface, which includes single method call `compareTo`. Comparable is an interface defining a strategy of 
comparing an object with other objects of the same type. This is called the class’s “natural ordering”.

#### Comparator interface

Other than doing *natural ordering*, comparator will allow to compare objects according to some notion, for example comparing two strings which is the shortest. A comparator is an object that is external to the class of the keys it compares  

```java
public class StringLengthComparator implements Comparator<String> {
    /** Compares two string according to their lengths */
    public int compare(String a, String b){
        if(a.length() < b.length()) return -1;
        else if(a.length() == b.length()) return 0;
        else return 1;
    }
}
```

Using a comparator using above implementation 

```java
StringLengthComparator comp = new StringLengthComparator();
String a, b;
...
int i = comp.compare(a,b);

#using java collections sort 
ArrayList list = new ArrayList();
...
Collections.sort(list, comp);    
```

### Comparator Priority Queue ADT



























## Heaps

#### Heap properties

A heap is a binary tree T that stores entries at its positions, and that satisfies two additional properties: 

**Heap-Order Property:** In a heap T, $\mathcal{O}(n\log{}n)$ 

**Complete Binary Tree Property:** 



