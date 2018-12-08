1. What are the advantages and disadvantages on using array vs arraylist?
   ​	Array and ArrayList both provides $O(1)$ performance but adding an element in ArrayList, involves creating a new array in background and copying it to new array. Hence, ArrayList requires more memory to store same number of element comparing to array.  ArrayList is type safe because it supports generics data types, which allows compiler to check type error. Whereas, array provides runtime type checking by throwing array exception. 

2. Abstract class vs interface class differences

  ​	*Interface*: Is blueprint for a class that can be used to implement a class. Interface cannot have any concrete methods. Interface can have static members and method signatures. Interface can extend other *interfaces*

    ```java
    public interface Car{
        public static final wheels = 4;
        public void engine(String engine);
        public abstract void doStart();
    }
    ```
  ​	*Abstract*: Is also a blueprint for concrete classes but abstract classes may have implemented methods. Abstract classes can implement and extend*interface*.  Class can be abstract without having any methods inside it. Static members are allowed. 
    ```java
    public abstract class Car{
        public static final int wheels = 4;
        String turn(String dir){
        System.out.print("turning" +dir)
        }
        public abstract void doStart(String sound);
        public abstract void shutDown();
    }
    ```

3. Big O general questions 
   **Constant** $\mathcal{O(1)}$: Algorithm that will always execute in the same time or space regardless of  the input data set. 
   **Linear** $\mathcal{O(n)}$: Algorithm whose performance will grow linearly and in direct proportion to the size of the input data set.
   **Quadratic** $\mathcal{O(n^2)}$: Agorithm whose performance is directly proportional to the square of the size of the input data set. This algo involve nested iterations over the data set. `for(){ ... for(){...}}`. 
   **N-log-n** $\mathcal{n\ log\ n}$:

4. What are the advantages and disadvantages of Stacks and Queues?
   Stacks: Last in First Out LIFO 
   Queues: First in First Out FIFO 

5. What are two type of iterator which we can implement? Explain lazy iterator.
   We have twi kinds of iterator: 
   **snapshot iterator:** : Maintains its own private copy of the sequence of element but its runtime is $O(n)$ 
   **lazy iterator:** Does not make an upfront copy, instead performing a traversal of primary structure only when `next()`method is called. it's runtime is $O(1)$ 

6. Describe tree path. 

7. Describe depth and height from tree?

8. Describe children and siblings.

9. why we use abstract class?

10. What does `valid`function do from tree?

11. Define and explain Priority Queue.

12. What is sorted and unsorted PQ?

13. How do you remove element from tree; explain in words?

14. What does `heapUP() and heapDown()`do?

15. Effective way to have less collision; explain MAD method

16. How does linear probing work? explain in words 

17. What does `bucketGet()` and `budgetPut()`does? 

18. Write pseduo code for 

    1. bubble sort 
    2. selection sort 
    3. quick sort 

19. Understand the Big O's time and space 

20. How does stability sort works?
