## Hash Tables

### Hash Table

A hash table is a collection of items which are stored in such a way as to make it easy to find them later. Each position of the hash table, often called a slot, can hold an item and is named by an integer value starting at 0. 

![Hash table with 11 empty slots](https://bradfieldcs.com/algos/searching/hashing/figures/hash-table.png)

Ideally, keys will be distributed in the range from 0 to $N -1$ by a *hash function,*but in practice there may be two or more distinct key that get mapped to the same index. 

As a result, we will conceptualize our table as a *bucket*array, in which each bucket may manage a collection of entires that are sent to a specific index by the *hash function*

## 

### Hash Function

The mapping between an item and the slot where that item belongs in the hash table is called the *hash function*. The goal of a *hash function, h,*is to map each key *K*to an integer in the range $[0, N - 1],$ where *N*is the capacity of the bucket array for a *hash table*

With such a *hash function, h,*we use the hash function value, *h(K),* as an index into our bucket array, *A*, instead of the key *K*. That is we store the *entry (K, V)*in the bucket *$A[h (k)]$* 

***In this figure:*** 

key is *K*which computes an integer that is called the *hash code*for *K*. This integer do not need to be in the range of $[0, N - 1]$, and may even be negative.

![hashing.png](https://datastructures.maximal.io/img/hash-tables/hashing.png)

## 

#### Collision 

If there are two or more keys with the same hash value, then two different entries will be mapped to the same bucket in *A*.  In this case, we say that a collision has occurred. We say that a hash function is *good*if it maps the keys in our map so as to sufficiently minimize collisions. 

## 

### Hash codes in Java

The object class, which servers as an ancestor of all object types, includes a default `hashCode()`method that returns a 32-bit integer of type *int*, which servers as an object's hash code. It is derived from the object's memory address.

## 

#### Compression functions

The hash code for a key *K*will typically not be suitable for immediate use with a bucket array, because the integer hash code may be negative or may exceed the capacity of bucket array. The **Compression function**is the second action performed as part of an overall hash function.

##### The division method

A simple compression function is the **divison method**, which maps an integer *i*to $i \ mod\  N$, where *N*, the size of the bucket array, is a fixed positive integer. If we take *N*to be a prime number, then this compression function helps "spread out" the distribution of hashed values.

##### The MAD method

A more sophisticated compression function, which helps eliminate repeated patterns in a set of integer keys, is the *Multiply-Add-and-Divide (or "MAD")*method.

This method maps an integer *i*to 

$\mathcal{[ (ai + b)\  mod\ p ]\ mod\ N }$ 

Where *N *is the size of the bucket array, *P *is a prime number larger than *N, *and *a and b* are integers chosen at random from the interval $[0, p - 1], $ with $a\ >\ 0$ . This function is chosen in order to eliminate repeated patterns in the set of hash codes and get us closer to having a "good" hash function

## 

### Collision and Collision handling

#### Collision 

If there are two or more keys with the same hash value, then two different entries will be mapped to the same bucket in *A*.  In this case, we say that a collision has occurred. We say that a hash function is *good*if it maps the keys in our map so as to sufficiently minimize collisions. 

#### Collision handling 

The main idea of a hash table is to take a bucket array, A, and a hash function, *h*and use them to implement a map by storing each `entry(K, V)`in the *bucket* `A[ h (k)]`

However, we have problem when we have two distinct keys, *k1*and *k2*,  such that `h( k1 ) == h( k2)`. This collisions prevents us from simply inserting a new `entry(K, V)` directly into the bucket `A[h (k)]`

## 

### Separate chaining 

A simple and efficent way for dealing with collisions is to have each bucket *A[j]*store its own secondary container, holding all `entry(K, V)`such that `h(k) = j`

If we insert DTW, SFO, LHR, YYZ, LAX and SYD into a hash table and use seperate chaining as the collision resolution schema, this is what hash table will look

![chaining.png](https://datastructures.maximal.io/img/hash-tables/chaining.png)

#### Linear probing

A simple method for collision handling with open addressign is *linear probing*. If we try to insert an `entry(K, V)`into a bucket `A[j]`that is already occupied,
where `j = h(k)`, then we try next `A[j + 1] mod N`, if this slot is also already occupied, then we try `A[(j + 2) mod N]`, and so on, until we find an empty bucket that can accept the new entry 

Let’s insert DTW, SFO, LHR, YYZ, LAX and SYD into a hash table using 
linear probing as the collision resolution schema. We might end up with a
hash table that looks like this:

![linear probing.png](https://datastructures.maximal.io/img/hash-tables/linear_probing.png)

### Efficiency of hash tables

If hash function is good, then we expect the entries to be uniformly distributed in the *N*cells of the bucket array.

To store *n*entries, the expected number of keys in a bucket would be $\ulcorner n/\ N \urcorner$ , which is $O(1)$ if $n$ is $O(N)$. 

| Method                         | Unsorted List | Hash Table<br />  Expected vs Worst |
| :----------------------------- | :------------- | :----------        |
| `get`                          | $O(n)$        | $O(1)$ vs $O(n)$ |
| `put`                          | $O(n)$        | $O(1)$ vs $O(n)$ |
| `remove`                       | $O(n)$        | $O(1)$ vs $O(n)$   |
| `size`, `isEmpty`              | $O(1)$        | $O(1)$ vs $O(1)$   |
| `entrySet`, `KeySet`, `values` | $O(n)$        | $O(n)$ vs $O(n)$   |


