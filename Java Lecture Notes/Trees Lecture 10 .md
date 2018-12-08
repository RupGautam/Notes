## Trees

### What is a Tree?

A Tree is a non-linear data structure where data objects are organized in terms of hierarchical relationship. Unlike *array* and *linked list*, data in a tree is not organized linearly. Each data element is stored in a structure called a *node*. 

a Tree is an abstract data type that stores elements hierarchically. With exception of the top element, each element in a tree has a *parent* element and zero or more *children*elements. 

#### Tree Definition

A tree T as set of nodes storing elements such that the nodes have a parent-child relationship that satisfies the following rules:

 -  If *T* is nonempty, it has a special node, called the *root of T*, that has no parent.

 -  Each node *v of T* different from the root has a unique *parent* node *w*; every node with parent *w* is a child of *w* 

**Other Node Relationships**

Two nodes that are *children* of the same parent are *siblings*. A node *V* is external
if *V* has no children. A node *V* is internal if it has one or more children. *External*
nodes are also known as *leaves*.

#### Important Terms

- **Root**: node without a parent (top most node)
- **Child**: The node below a given node connected by its edge
- **Depth**: Depth of a node (count of number of  ancestors)
- **Height**: Height of a tree: maxium depth of any node
- **Siblings**: Two nodes that are children of the same parent
- **External**:  A node *V* is external if *V*has no children, also known as *leaves* 
- **Internal**: A node *V* is internal if it has one or more children
- **Ancestor**: A node *U* is an ancestor of a node *V* if *u* is an ancestor of the parent of *V*
- **Descendant**: A node *v* is a descendant of a node *U* if *U* is an ancestor of *V*
- **Subtree**: The subtree of *T* rooted at a node *v* is the tree consisting of all the descendants of *v* in *T* (including *V* itself)
- **Traversing**: Traversing means passing through nodes in a specfic order

![Binary Tree](https://www.tutorialspoint.com/data_structures_algorithms/images/binary_tree.jpg)

[Credit](https://www.tutorialspoint.com/data_structures_algorithms)

#### Edge and paths in trees

- **Edge**: An edge of a tree *T* is a pair of nodes (*U*,*V*) such that *U* is the parent of *V*, or vice versa.

- **Path**: A path of *T*is sequence of nodes such that any two consective nodes in the sequence form an edge.

### Orderd Trees

If a tree is ordered if there is a meaningful linear order among the children of each node; that is, we purposefully identify the children of a node as being the first, second , third and so on. Such order is usually visualized by arranging siblings left to right, according to their order.

### The Tree abstract data type

A position object for a tree supports the following methods:

**Position**

`getElement()`: Returns the elements stored at this position

**Accessor Method:** 

`root()`: Returns the position of the root of the tree (or null if empty)

`parent(p)`: Returns the position of the parent of position *p*(or null if o is the root)

`children(p)`: Returns an iterable collection containing the children of position *p*(if any)

`numChildren(p)`: Returns the number of children of position *p*

**Query Methods**:

`isInternal(p)`: Returns true if position *P* has at least one child

`inEnternal(p)`: Return true if position *p* does not have any children

`isRoot()`: Returns true if position *p* is the root of the tree 

**General Methods:**

`size()`: Returns the number of positions(a hence elements) that are contained in the tree

`isEmpty()`: Returns true if the tree does not contain any position (and thus no elements)

`iterator()`: Returns an iterator for all the elements in the tree (so that the tree itself is Iterable)

`positions()`: Returns an iterable collection of all the position of the tree

**The Tree interface**
```java
public interface Tree<E> extends Iterable{
    Position<E> root();
    Position<E> parent(Position<E> p)throws IllegalArgumentException;
    Iterable<Position <E>> children(Position<E> p)throws IllegalArgumentException;
    int numChildren(Position<E> p)throws IllegalArgumentException;
    boolean isInternal(Position<E> p)throws IllegalArgumentException;
    boolean isEnternal(Position<E> p) throws IllegalArgumentException;
    boolean isRoot(Position<E> p) throws IllegalArgumentException;
    int size();
    boolean isEmpty();
    Iterator<E> iterator();
    Iterable<Position <E>> positions();
}
```

#### An Abstract Tree base class

Interface class cannot include definitions for any of those above methods. In constrast , an abstract class may define concrete implementations for some of its methods, while leaving other abstract methods without definition. Abstract class is designed to server as a base class, through inheritance. 

Example of abstract base class interface 
```java
public abstract class AbstractTree<E> implements Tree<E> {
    public boolean isInternal(Position<E> p) {
        return numChildren(p) > 0;
    }
    public boolean isExternal(Position<E> p){
        return numChildren(p) == 0;
    }
    public boolean isRoot(Position<E> p){
        return p == root();
    }
    public boolean isEmpty(){ return size() == 0;}
}
```

In Java, an abstract class can implement an interface, and not provide implementations of all the interface's methods. 

#### Tree depth 

Let *P* be a position within tree *T*. The depth of *P* is the number of ancestor of *P*, other than *P* itself. If *P* is the root, then the depth of *P*is 0. Otherwise, the depth of P is one plus the depth of the parent of *P*.

```java
public int depth(Position<E> p) {
    if(isRoot(p)) return 0;
    else return 1 + depth(parent(p));
}
```

Running time for `depth(p)`for position *P* is $\mathcal{0(dp + 1)}$. Worst-case time is $\mathcal{O(n)}$ wher *n* is the total number of positions of *T*



#### Tree height 

Height of a tree to be equal to the maximum of the depths of its positions (or zero, if the tree is empty). 

```java
private int heightBad(){
    int h = 0;
    for(Position<E> p: positions())
        if(isExternal(p)) //look for leaf positions only
            h = Math.max(h, depth(p));
    return h;
}
```

If *P* is a leaf, then the height of *P* is 0. Otherwise, the height of *P* is one more than the maximum of the heights of *P's* children.

```java
public int height(Position<E> p){
    int h = 0;
    for(Position<E> c:children(p))
        h = Math.max(h, 1 + height(c));
    return h;
}
```

### Binary Trees

A binary tree is an ordered tree, where every node has at most two children. Each child node is labeled as being either a *left child* or a *right child*. A *left child* precedes a *right child*in the order of children of a node. 

**Left subtree** or **Right subtree**: The subtree rooted at a left or right child of an internal node *V* is called left subtree or right substree. 

A binary tree is proper if each node has either zero or two children. Some people also refer to such trees as being full binary trees. Thus, in a proper binary tree, every internal node has exactly two children. 

#### A binary tree ADT

A binary tree supports the following methods:

`left(p)`: Returns the position of the left child of *P* or null if *P* has no left child

`right(p)`: Return the position of the right child of *P* or null if *P* has no right child

`sibling(p)`: Returns the position of sibling of *P* or null if *P* has no sibling 

#### BinaryTree interface

```java
public interface BinaryTree<E> extends Tree<E>{
    Position<E> left(Position<E> p) throws IllegalArgumentException;
    Position<E> right(Position<E> p) throws IllegalArgumentException;
    Position<E> sibling(Position<E> p) throws IllegalArgumentException;
}
```

![img](https://i.imgur.com/BrwBiti.png)

#### An AbstractBinaryTree class

To make code more reusable we will use AbstractTree, it will provide additional concrete methods that can be derived from the newly declared left and right methods

![img](https://imgur.com/LoJ13in.png) 

Defining an AbstractBinaryTree base class 

```java
public abstract class AbstractBinaryTree<E> extends AbstractTree<E> implements BinaryTree<E>{
    public Position<E> sibling(Position<E> p){
        Position<E> parent = parent(p);
        if(p == null) return null;
        if(p == left(parent)) return right(parent);
        else return left(parent);
    }
    
    public int numChildren(Position<E> p){
        int count = 0;
        if(left(p) != null) count ++;
        if(right(p) != null) count ++;
        return count ++;
    }
    
    public Iterable<Position<E>> children(Position<E> p){
        List<Position<E>> snapshot = new ArrayList<>(2);
        if(left(p) != null) snapshot.add(left(p));
        if(right(p) != null) snapshot.add(right(p));
        return snapshot;
    }
}
```

#### Linked structure for BinaryTree

LinkedBinaryTree methods:

`addRoot(e)`: Creates a root for an empty tree, storing element e and returns the position of that root;  error if tree is not empty

`addLeft(p, e)`: Creates a left child of position *P*, storing element e and returns the position of the new node; error if *P*already has a left child

`addRight(p, e)`: Creates a right child of position *P*, storing element e and returnt he position of the new node; error if *P*already has a right child

`set(p, e)`: Replaces the element stored at position *P*with element e, and returns the previously stored element

`attach(p, T1, T2)`: Attaches the internal structure of trees T1 and T2 as the respective left and right subtrees of leaf position *P* and resets T1 and T2 to empty trees; error if condition occurs if *P *is not a leaf

`remove(p)`: Removes the node at position *P*replacing it with its child (if any), and returns the element that had been stored at *P*; error occurs if *P*has two children