##Generics

Generic classes and methods can operate on a variety of data types while often avoiding the need of explicit casts. Generics framework allows us to define a class in terms of a sef of formal type parameters, which can then be used as the declared type for variables, parameters and return values within the class definition 

*Advantages*:

- Stronger type checks at compile time

- Fixing compile-time error is easier than fixing runtime errors

- Type cast is not required 

  The following code snippet without generics requires casting: 

*This example is without generics and it requires casting* 

``` java 
List list = new ArrayList();
list.add("hello");
String s = (String) list.get(0);
```
*This example is with Generics and it does not requires casting*

```java
List<String> list = new ArrayList<String>();
list.add("hello");
String s = list.get(0);   // no cast
```

*Example*: 

```java
public class Pair<A, B>{
A first; 
B second;
public Pair(A a, B b){
first = a;
second = b;
}
public A getFirst() { return first; }
public B getFirst() { return second }	
}
```

#### Generic Data Type

Java Generic Type Naming convention helps us understanding code  easily and having a naming convention is one of the best practices of  java programming language. So generics also comes with it’s own naming  conventions. Usually type parameter names are single, uppercase letters  to make it easily distinguishable from java variables. The most commonly  used type parameter names are:

- E – Element (used extensively)
- K – Key (Used in Map)
- N – Number
- T – Type
- V – Value (Used in Map)

#### Generic Methods

Generic methods are those methods that are written with a single  method declaration and can be called with arguments of different types.  The compiler will ensure the correctness of whichever type is used.  

These are some properties of generic methods:

- Generic methods have type parameter `<data type>` before the return type of the method declaration
- Generic methods can have different type parameters separated by commas `<data type1, data-type2>`in the method signature
- Method body for a generic method is just like a normal method

####Nested classes

Java allows a class definition to be nested inside of another class. It is useful to use nested classes when defining a class that is strongly affiliated with another class. This can help increase encapsulation and reduce naming conflicts 

```java
public class CreditCard { #outerclass
private static class Transcation {} #Inner class 
Transaction[] history; 
}
```

Outer class (CreditCard) is also called containing class, and nested class (Transcation) is a member of outer class 

