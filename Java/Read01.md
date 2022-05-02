# Java

## Access modifiers

They are used to set the level of access for `classes` `attributes` and `methods`

### for classes

* public: accessible by any class
* default: accessible only by the classes in the same package

### for attributes and methods

* public: Accessible for any class
* default: the variable or method is created without access modifier and it is accessible by any class inside the package
* protected: Provides the same access as the default access modifier, with the addition that subclasses can access protected methods and variables of the superclass
* private: accessible only within the declared class itself
It's a best practice to keep the variables within a class private. The variables are accessible and modified using Getters and Setters.

## OOP Concepts

### Encapsulation

The idea behind encapsulation is to ensure that implementation details are not visible to users. The variables of one class will be hidden from the other classes, accessible only through the methods of the current class. This is called data hiding.
To achieve encapsulation in Java, declare the class' variables as private and provide public setter and getter methods to modify and view the variables' values.

for example:

```java
class BankAccount {
private double balance=0;
public void deposit(double x) {
    if(x > 0) {
    balance += x;
    }
}
}
```

This implementation hides the balance variable, enabling access to it only through the deposit method, which validates the amount to be deposited before modifying the variable.

### Inheritance

Inheritance is the process that enables one class to acquire the properties (methods and variables) of another. With inheritance, the information is placed in a more manageable, hierarchical order.

The class inheriting the properties of another is the subclass (also called derived class, or child class); the class whose properties are inherited is the superclass (base class, or parent class).

To inherit from a class, use the extends keyword.
This example shows how to have the class Dog to inherit from the class Animal.

```java
class Dog extends Animal {
 // some code
}
```

Here, Dog is the subclass, and Animal is the superclass

When one class is inherited from another class, it inherits all of the superclass' `non-private variables and methods`.
Example:

```java
class Animal {
  protected int legs;
  public void eat() {
    System.out.println("Animal eats");
  }
}

class Dog extends Animal {
  Dog() {
    legs = 4;
  }
}
```

### Polymorphism

Polymorphism, which refers to the idea of "having many forms", occurs when there is a hierarchy of classes related to each other through inheritance.
A call to a member method will cause a different implementation to be executed, depending on the type of the object invoking the method.
Here is an example: Dog and Cat are classes that inherit from the Animal class. Each class has its own implementation of the makeSound() method.

```java
class Animal {
  public void makeSound() {
    System.out.println("Grr...");
  }
}
class Cat extends Animal {
  public void makeSound() {
    System.out.println("Meow");
  }
}
class Dog extends Animal {
  public void makeSound() {
    System.out.println("Woof");
  }
}
```

### Method Overriding

As we saw in the previous lesson, a subclass can define a behavior that's specific to the subclass type, meaning that a subclass can implement a parent class method based on its requirement.
This feature is known as method overriding.
Example:

```java
class Animal {
    public void makeSound() {
        System.out.println("Grr...");
    }
}
class Cat extends Animal {
    public void makeSound() {
        System.out.println("Meow");
    }
}
```

In the code above, the `Cat` class overrides the `makeSound()` method of its superclass `Animal`.

Rules for Method Overriding:

* Should have the same return type and arguments
* The access level cannot be more restrictive than the overridden method's access level (Example: If the superclass method is declared public, the overriding method in the sub class can be neither private nor protected)
* A method declared final or static cannot be overridden
* If a method cannot be inherited, it cannot be overridden
* Constructors cannot be overridden

### Method Overloading

When methods have the same name, but different parameters, it is known as method overloading.
This can be very useful when you need the same method functionality for different types of parameters.
The following example illustrates a method that returns the maximum of its two parameters.

```java
int max(int a, int b) {
  if(a > b) {
    return a;
  }
  else {
    return b;
  }
}
```

The method shown above will only work for parameters of type integer.
However, we might want to use it for doubles, as well. For that, you need to overload the max method:

```java
double max(int a, int b) {
  if(a > b) {
    return a;
  }
  else {
    return b;
  }
}
```

Now, our max method will also work with doubles.
An overloaded method must have a different argument list; the parameters should differ in their type, number, or both.
