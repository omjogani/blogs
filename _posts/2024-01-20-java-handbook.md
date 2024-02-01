---
title: Java Handbook
date: 2024-01-20 10:00:00 -500
categories: [java, handbook]
tags: [java]
---


# Java Handbook

Java is a high-level, class-based, object-oriented programming language. It is a compiled language.

Java is consider as fully object oriented. It seems controversial topic because there are diversified thoughts on this like Java supports Primitive data type hence it's not considered as fully object oriented language.

Java program is WORA (Write once run anywhere).

## How Java works?

![JavaIntro-modified](https://github.com/omjogani/blogs/assets/72139914/b41a4e35-bedb-4dac-83f9-fb7fd58727fc)

When Java program compiles by `javac` compiler the Java code converted into `byte code` that is then understood by the JVM and then `byte code` is converted into `machine code`.

![JDKJREJVM](https://github.com/omjogani/blogs/assets/72139914/3abda2bb-4c3c-43a8-8cfe-7c9195eeb054)

### JVM (Java Virtual Machine)

Java Virtual Machine is platform dependent that means it needs to be install on every machine required to run Java Program. while Java Program is Java Independent that means Java Program developed on one machine can execute on all the Machines which has JVM Install.

JVM is used to convert `byte code` to `machine code`.

JVM consist of JIT (Just-In-Time) which is used to improve the performance by compiling the `byte code` to `machine code`.

### JRE (Java Runtime Environment)

Java Runtime Environment consists of collection of library and other components for Java Program.

It provide wide range of library to reuse the code already written.

### JDK (Java Development Kit)

When we download the JDK it gives JRE & JVM. It include couple of components like compiler, a debugger and other tools to develop Java Program.

---

Java is strongly type language that means we need to specify the type of variables while declaring in Java Code.

## Variables in Java

**Primitive Types** : Primitive data types specify the size and type of variable values. They are the building blocks of data manipulation and cannot be further divided into simpler data types.

**Non-Primitive Types** : Non-primitive data types or reference data types refer to instances or objects.

| Primitive Types | Non-Primitive Types |
| --------------- | ------------------- |
| Integer         | Array               |
| Float           | Class               |
| Character       | Interfaces          |
| Boolean         | Strings             |
|                 | Enums               |

### Integers

| Integers | Size    |
| -------- | ------- |
| int      | 4 bytes |
| long     | 8 bytes |
| short    | 2 byte  |
| byte     | 1 byte  |

### Floats

| Floats | Size    |
| ------ | ------- |
| float  | 4 bytes |
| double | 8 bytes |

### Others

| Others     | Size    |
| ---------- | ------- |
| characters | 2 bytes |
| boolean    | 1 bit   |

### Literals in Java

Literals are specific representation of the values in Java. Such as...

```java
int money = 10_00_000; // refers to 10M or 1000000
boolean value = 1; // value = true
```

### Type Casting and Conversion

Type Casting is the process of converting type of the from one data type to another data type.

**Types of Type Casting in Java**

**Widening Type Casting**: It refers to converting lower data type to higher data types. It is also refers as `Implicit Type Casting`.

```java
short smallValue = 10;
int largeValue = smallValue;
```

In above example `short` is getting type casted in `int`, because `int` is higher data type (4 bytes) and `short` is lower data type (2 bytes).

---

**Narrowing Type Casting** : It refers to converting higher data types to lower data types. It is also refers as `Explicit Type Casting`.

```java
int largeValue = 257;
byte smallValue = (byte) largeValue; // not a good idea
```

It's never recommended to use Narrowing Type Casting because it may leads to data loss. Suppose in above example `largeValue` has value `99000` then it's anyway not possible to fit in `smallValue` then we'll lose the value.

`smallValue` will have value = `257 (largeValue) % 256 (Range of byte) = 1`

---

### Type Promotion

```java
byte a = 10;
byte b = 30;
int output = a * b; // answer of a x b exceed range of the byte.
```

Because result of the expression `a * b` exceeds the range of `byte` the type is promoted as `int`.

## Conditional Statements and Looping

### if, else & else if

`if, else & else if` is used to run the code based on some condition.

```java
int age = 19;
if (age >= 18) {
    System.out.println("You can Drive!");
} else if (age < 18) {
    System.out.println("You can't Drive!");
} else {
    System.out.println("Invalid Age!");
}
```

if first condition matches then It'll print the message `"You can Drive!"`. else second condition matches then It'll print the message `"You can't Drive!"`. If none of above condition matches It'll print the message `"Invalid Age!"`.

### While, Do-While, For & ForEach Loop

Loops are used to run code iteratively. You're required to provide base condition that define when to exits the loop. Otherwise there will be infinite looping and eventually leads to `segmentation fault`.

### While Loop

```java
int age = 0;
while(age != 18) {
    age++;
}
System.out.println("Your age is 18!");
```

### Do-While Loop

```java
int age = 0;
do {
    age++;
} while(age != 18);
System.out.println("Your age is 18!");
```

No matter what, `Do-While` Loop at least execute once. because it first run the code once and then check condition and run the code again until condition is unsatisfied.

### For Loop

```java
int age = 0;
for(int i = 0; i < 18; i++) {
    age++;
}
System.out.println("Your age is 18!");
```

Syntax for For loop consist of three parts, `initialization; condition; increment/decrement`.

### ForEach Loop

```java
int [] array = { 10, 20, 30, 40, 50 };

for(int value : array ) {
   System.out.println(value);
}
```

`ForEach` loop generally used with array or list. It will pickup elements from array one by one util it reaches the end of the loop.

## Classes and Objects

Class is blueprint of objects. Class contains member variables & methods. We tends to wrap the entity with their attributes and behavior together in form of class.

e.g. Car which has attributes as gear, steering, engine, tires etc. and Behavior as moving steering left and right, changing gear, rotating wheels etc.

```java
/* Calculator.java */

class Calculator {
    // Instance Variables
    int number1;
    int number2;

    // method
    public int add() {
        return a + b;
    }
}
```

```java
/* Main.java */
public static void main(String [] args){
    Calculator cal = new Calculator();
    cal.number1 = 10;
    cal.number2 = 20;
    int result = cal.add();
    System.out.println(result);
}
```

We created object `cal` of class `Calculator` and assign values to the member variables and run the method `add` of the class `Calculator`.

### How classes & objects works internally.

![JavaInternal-modified](https://github.com/omjogani/blogs/assets/72139914/6d91eae0-24aa-4707-87c2-b57ba0344e5c)

```java
class Calc {
    int num = 5;
    public int add(int n1, int n2){
        return n1 + n2;
    }
}

class Main {
    public static void main(String[] args) {
        int data = 10;
        Calc obj = new Calc();
        int r1 = obj.add(3, 2);
        System.out.println(r1);
    }
}
```

All the Objects and Collection will be stored in Heap Memory, Other than that will be stored in Stack Memory.

When Object is created it makes entry in Stack with address of object available in Heap Memory.

### Method Overloading

It refers to the term which says "Same name different behavior". We can define multiple method with same name but It mush have different number of arguments.

```java
class Calc {
    public int add(int a, int b) {
        return a + b;
    }

    public int add(int a, int b, int c) {
        return a + b + c;
    }
}
```

Whenever we pass 2 arguments, It will automatically call fist method. and When we pass 3 arguments, It will call second method.

It determines which one to call only with the parameters.

### Constructor

It is a special method called when Object it created. It must have the name exactly same as Class Name. We can overload the constructor too (Based on Parameters) just like Method Overloading.

```java
//default constructor
public class Human{
    public Human() {
        /* ...body... */
    }
}

// parameterized constructor
public class Human {
    public Human(int totalHands, int totalLegs){
        /* ...body... */
    }
}
```

Generally, We see `this` keyword in the constructor that eventually means the current class. eg. `this.totalHands` then It's pointing to current class member variable.

## Array

There are different types of arrays.

- Single Dimensional Array
- Multi Dimensional Array
- Jagged Array

### Single Dimensional Array

```java
int num[] = {2, 3, 4, 5};
int [] num = new int[5];

// foreach loop
for(int item: num){
    /* ...operation... */
}
```

### Multi Dimensional Array

```java
// row = 3, column = 4
int num[][] = new num[3][4];

for(int n[]: num) {
    for(int m: n) {
        /* ...body... */
    }
}
```

### Jagged Array

Jagged array where in each row columns are not fixed.

```java
int num[][] = new int [3][];
num[0] = int [4];
num[1] = int [3];
num[2] = int [2];
```

## String

The Behavior of String is not normal compare to other programming languages.

There are 2 types of Strings in Java.

- Mutable String (Can Change)
- Immutable String (Can't Change)

### Immutable String

```java
String name = new String("Om Jogani");
System.out.println(name);
```

It creates object `name` in Heap Memory. Above String is not changeable but If you try to change the String, There won't be any problem.

It gives and illusion of changing the String but Behind the Scene It pulls out String data and assign to new String and return new String instead of changing the existing String.

Now, Question is What are the alternative of Immutable String?

### String Buffer

```java
StringBuffer sb = new StringBuffer();
```

Default `sb` Size = 16 bytes \
If we assign `sb` = "hello" then size of `sb` would be 16 + 5 = 21 bytes.

There are many methods available on `StringBuffer` like `append`, `insert`, `ensureCapacity` etc.

`ensureCapacity` is used to set **initial capacity**.

## StringBuilder

```java
StringBuilder sb = new StringBuilder();
```

`StringBuilder` is same as `StringBuffer` but `StringBuilder` is thread safe while `StringBuffer` is not thread safe.

## Static

We can use `static` keyword with variables, functions and as a Block.

If We use static variables then It will be alive until execution of the Program ends that means We can have common variables across multiple objects.

If We use static methods then It's possible to call the method without Object.

Static methods can be called using ClassName only. eg. `ClassName.method();`

Static Block only called once despite creating 100s of Objects. Static Block is generally used to assign the value of the static variable.

It runs before constructor because It gets executed When Class is getting loaded.

JVM has Class Loader which loads the class first and then Object gets initiated.

### Load Class

```java
Class.forname("ClassName");
```

It won't create Object of Class rather It only loads the class. While Static Block runs when class load It will execute the Static Block reside in in that Class.

Static Methods only accepts Static variables. It doesn't accept non-static variables.

`main` method is static so that It doesn't required to have object to call it.

Example of Static Method

```java
public static void greetings() {
    System.out.println("Hello World");
}
```

## Object Oriented Programming Concepts

### Encapsulations

As real Capsule has outer cover and inside that It has Medicine that is not exposed directly.Based on the same concept, We want some variables to not accessed or modify directly by anyone.

So, We provide getters & setters for that and make that variable private. It also helps to perform some extra steps in setter method.

### Inheritance

Inheritance is used to derive the properties of one class to the another class. It provides code reusability.

We use `extends` keyword to extend the functionality of current class with inherited class.

```java
class Vehicle {
    public void move() {
        /* ...body... */
    }

    public void details(String model) {
        /* ...body... */
    }
}

class Bike extends Vehicle {
    public void bikeDetails(String model) {
        details(model);
    }
}
```

There are several types of Inheritance available in Java.

![inheritance1](https://github.com/omjogani/blogs/assets/72139914/b4c24112-fbd0-4dd4-8f71-04128fcf46cc)

### Polymorphism

There are 2 Types of Polymorphism.

- Compiler Time Polymorphism
- Run Time Polymorphism

In Compiler Time Polymorphism, Behavior decided at compile time. eg. Method Overloading. In Run Time Polymorphism, Behavior decided at run time. eg. Method Overriding.

```java
class Vehicle {
    public void move() {
        System.out.println("Move");
    }
}

class Bike extends Vehicle{
    public void move() {
        System.out.println("Bike move");
    }
}
class Main {
    public class main(String[] args) {
        Bike bike = new Vehicle();
        bike.move(); // call `move` of Vehicle Class
        bike = new Bike();
        bike.move(); // call `move` of Bike Class
    }
}
```

We can also reassign the object as shown above and it's also called dynamic method dispatch.

## Anonymous Class

```java
class Vehicle {
    public void move() {
        System.out.println("Move");
    }
}

class Bike {
    public void details() {
        System.out.println("Bike Details");
    }
}
class Main {
    public class main(String[] args) {
        Bike bike = new Bike();
        bike.details();
    }
}
```

Above code can be converted to Anonymous Class.

```java
class Vehicle {
    public void move() {
        System.out.println("Move");
    }
}

class Main {
    public class main(String[] args) {
        Bike bike = new Bike() {
            public void details() {
                System.out.println("Bike Details");
            }
        }
    }
}
```

## Anonymous Object

```java
new Calc();
```

It only called constructor of the class `Calc`. It cannot be reuse.

```java
new Calc().show();
```

## Method Overriding

While we have Single Inheritance we can override the method in the sub class Which is extended from super class.

```java
class Vehicle {
    public void move() {
        System.out.println("Move");
    }
}

class Bike {
    public void move() {
        System.out.println("Override Method");
    }
}
class Main {
    public class main(String[] args) {
        Bike bike = new Bike();
        bike.move();
    }
}
```

## Packages

Combine Multiple Classes to Package.

- tools
  - Calc
  - AdvanceCalc
- database
  - Connections
  - Operations

Here `tools & database` are packages & `Calc, AdvanceCalc, Connection, Operations` are Classes.

- tools
  - ui
    - login
    - home

Here `tools` is a package, `ui` is sub-package & `login & home` are Classes.

```java
import tools.*;
```

We can import everything from `tools` package with above lines.

## Access Modifier Table

|                                | Private | Protected | Public | Default |
| ------------------------------ | ------- | --------- | ------ | ------- |
| Same Class                     | YES     | YES       | YES    | YES     |
| Same Package Sub-Class         | NO      | YES       | YES    | YES     |
| Same Package Non-SubClass      | NO      | YES       | YES    | YES     |
| Different Package Sub-Class    | NO      | YES       | YES    | NO      |
| Different Package Non-SubClass | NO      | NO        | YES    | NO      |

## Final Keyword

Final keyword can be used with Variables, Functions as well as Classes.

If We use final with Variables then that Variable will become **constant**.

```java
final double PI = 3.14;
```

If We use final with Methods then It will prevent **method overriding**.

```java
public final void display() {
    System.out.println("I can't Override!");
}
```

If We use final with Classes then It will prevent **Inheritance**.

```java
final class MyClass {
    /* ...body... */
}
```

---

If we try to print the Object it will print `ClassName@HashCode`. Because the default implementation of the `toString()` method consist of `ClassName@HashCode`.

It is possible to customize the default behavior of `toString()` by overriding `toString()` method.

We have equal method to Override and have checks based on values. By default it compare with HashCode.

## UpCasting & DownCasting

```java
class Vehicle {
    public void move() {
        System.out.println("Move");
    }
}

class Bike {
    public void details() {
        System.out.println("Bike Details");
    }
}
class Main {
    public class main(String[] args) {
        Vehicle vehicle = (Vehicle) new Bike(); // UpCasting
        Bike bike = (Bike) vehicle; // DownCasting
    }
}
```

## Abstract

Abstract Method is used to just declare the method. Abstract method is only used in abstract class. We can't create object of abstract class.

```java
abstract class Vehicle {
    public abstract void show();
}

class Car extends Vehicle {
    public void show() {
        System.out.println("Show Method");
    }
}
```

## Inner Class

```java
class Transport {
    int num;
    public void show() {
        System.out.println("Transport Show");
    }

    // inner class
    class Vehicle {
        public void details() {
            System.out.println("Details");
        }
    }
}

class Main {
    public class main(String[] args) {
        Transport trans = new Transport();
        trans.show();
        Transport.Vehicle vehicle = trans.new Vehicle();
        vehicle.details();
    }
}
```

## Interfaces

All the method in interface are Public & Abstract.

```java
interface Pokemon {
    String name = "Pikachu";
    void getAbilities();
    void getHeight();
    void getWeight();
}

class PokeService implements Pokemon {
    /* implements all the methods of Pokemon*/
}

interface PokeDetails extends Pokemon {
    void details();
}
```

Every Variable in Interface is **Final & Static**.

```java
interface Pokemon {
    void getAbilities();

    // default implementation: No need to implement
    default void getDetails() {
        System.out.println("Pokemon Details");
    }
}
```

It's possible to provide default implementation of method inside interface so that It's not necessary to implement that method in implemented class.

## Enums

Enums are used to provide set of static values in Java. Enums also contain methods, constructors and variables.

```java
public enum Day {
    SUNDAY, MONDAY, TUESDAY, WEDNESDAY,
    THURSDAY, FRIDAY, SATURDAY
}
public class EnumTest {
    Day day;

    public EnumTest(Day day) {
        this.day = day;
    }

    public void tellItLikeItIs() {
        switch (day) {
            case MONDAY:
                System.out.println("Mondays are bad.");
                break;

            case FRIDAY:
                System.out.println("Fridays are better.");
                break;

            case SATURDAY: case SUNDAY:
                System.out.println("Weekends are best.");
                break;

            default:
                System.out.println("Midweek days are so-so.");
                break;
        }
    }

    public static void main(String[] args) {
        EnumTest firstDay = new EnumTest(Day.MONDAY);
        firstDay.tellItLikeItIs();
    }
}
```

## Annotation

It is always good idea to use `Annotation` because...

- Code will be clean & readable
- Prevent Temporary Typos
- Some Errors can be catch at compiler time. (eg. @FunctionalInterface will give compile time error in case we have more than 1 method in interface.)

e.g.

- @Override
- @Test
- @FunctionalInterface

## Functional Interface

A interface which has exactly one method is called functional interface. It is annotated with `@FunctionalInterface`. We can use lamda function if We've used Functional Interface.

```java
@FunctionalInterface
interface PokemonOperation {
    public List<Pokemon> getAllPokemons();
}

public class Main {
    // with anonymous class & without lamda expression
    PokemonOperation po = new PokemonOperation(){
        public List<Pokemon> getAllPokemons() {
            return pokemons;
        }
    }


    // with anonymous class & lamda expression
    PokemonOperation op = () -> {
        retrun pokemons;
    }
}
```
--- 

>TODOS
## Records

## Sealed Classes

## Lambda Functions

## Streams 

