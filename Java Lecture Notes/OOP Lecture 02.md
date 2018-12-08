## Object Oriented Review

###Abstraction

An ADT can be expressed by an interface, which is simply a list of method declarations, which each method has empty body. ADT classes can have more methods than those of interfaces 

###Encapsulation
States that different components of software system should not reveal the internal details of their respective implementations . It allows other programmer to write code that depends on the interface but not the internal decisions 

###Modularity 
Modularity refers to an organizing principle of code in which different components of a software system are divided into separate functional units 

###Design Patterns
Solution to typical software design problem, which provides a general template for a solution that can be applied in many different situations

##### 		Example of Design Patterns
- Recursion or Recursive 
- Divide-and-conquer
- Template method 
- Adapter 

####Interface class
Interface is a blueprint for your class that can be used to implement a class ( abstract or not); the point is interface cannot have any concrete methods. Concrete methods are those methods which have some code inside them; in one word - implemented. What your interface can have is static members and method signatures. The example below shall help you understand how to write an interface.

```java
public interface Brain{
  public static final int number = 1;
  public void talk( String name );
  public abstract void doProgramming();
}
```
   - Interface classes is like a class, except a Java interface can only contain method signatures and fields. 
  - Interfaces do not have constructors and they cannot be directly instantiated 
  - When simple class implements an interface, it must implement all of the method declared in the interface 

####Abstract class

Abstract classes are a bit different from interfaces. These are also used to create blueprints for concrete classes but abstract classes may have implemented methods. But to qualify as an abstract class, it must have at least one abstract method. Abstract classes can implement one or more interfaces and can extend one abstract class at most. There is a logical reason to this design which we will talk about later in this post. Here is an example of Abstract class creation.

```java
public abstract class Car{
  public static final int wheels = 4;
  String turn( String direction ){
   System.out.println( "Turning" + direction ); 
  }
  public abstract void startWithSound( String sound );
  public abstract void shutdown( );
}
```

- An abstract is a class that is declared abstract -- it may or may not include abstract methods. Abstract classes cannot be instantiated, but they can be subclassed
- Abstract class may also extend another class and be extended by further subclasses

####Interfaces vs Abstract classes

- Unlike interfaces, abstract classes can contain fields that are not static and final, and they can contain implemented methods

- Method of a interface are implicitly abstract and cannot have implementations

- An abstract class can extend only one class or one abstract class at a time, where as, interface can extend multiple interfaces at a time 
