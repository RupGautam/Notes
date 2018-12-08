## Maps

#### Map

A Map is an abstract data type designed to efficiently store and retrieve values based upon a uniquely identifying search key for each. 

A Map stores *key-value*pairs `(K, V)`which we call entries, where *K*is the *Key*and *V*is it's corresponding *Value*

Keys are required to be unique, so that the association of keys to values defines a mapping. Maps are also known as associative arrays, because the entry's key acts like an index into the map, that assists the map to locate the element efficently.

##### Example of real world maps applications:

- A University's info system maps a student ID to the student's record
- DNS maps a host name to an IP address 
- A customer's account maps customer's stored data 

#### The Map ADT

Following the method that Map ADT should implement 

`size()`: Returns the number of entries in *M*

`isEmpty()`: Returns a boolean indicating whether *M*is empty

`get(k)`: Returns the value *V*associated with *key* *K,*if such an entry exist; otherwise returns null

`put(k, v)`: If *M*does not have an entry with *key*equal to *K,*then adds entry *(K, V)*to *M*and returns *null;*else, replace with *V*the existing value of the entry with key equal to *K* and return the old value

`remove(k)`: Removes from *M*the entry with key equal to *K,*and returns its value; if *M*has no such entry, then returns null

`keySet()`: Returns an iterable collection containing all the keys stored in *M*

`values()`: Returns an iterable collection containing all the values of entries stored in *M*(with repetition if multiple keys map to the same value)

`entrySet()`: Returns an iterable collection containing all the key-value entries in *M*

##### The Map interface

```java
public interface Map<K, V>{
    int size();
    boolean isEmpty();
    V get(K key);
    v put(K key, V value);
    Iterable<K> keySet();
    Iterable<V> values();
    Iterable<Entry<K, V>> entrySet();
}
```

#### AbstractMap

The AbstractMap base class provides functionality that is shared by all of our map implementations. 