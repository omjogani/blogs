---
title: Java Handbook
date: 2024-01-20 10:00:00 -500
categories: [handbooks, java]
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
boolean value = 1; // error
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
    }s
}
class Main {
    public static void main(String[] args) {
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
    public static void main(String[] args) {
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
    public static void main(String[] args) {
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
    public static void main(String[] args) {
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
    public static void main(String[] args) {
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
    public static void main(String[] args) {
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

A interface which has exactly one method is called functional interface. It is annotated with `@FunctionalInterface`. We can use lambda function if We've used Functional Interface.

```java
@FunctionalInterface
interface PokemonOperation {
    public List<Pokemon> getAllPokemons();
}

public class Main {
    // with anonymous class & without lambda expression
    PokemonOperation po = new PokemonOperation(){
        public List<Pokemon> getAllPokemons() {
            return pokemons;
        }
    }


    // with anonymous class & lambda expression
    PokemonOperation op = () -> {
        return pokemons;
    }
}
```

### Types of Interfaces

- **Normal Interface**: Basic Interface consist of two or more interfaces.

- **FunctionalInterface**: Allow only one method.

- **Marker Interface**: It is a blank interface, used for serializations.

## Exception

There are 2 types of Errors in Java.

1. Compile Time Errors
2. Run Time Errors

It's not possible to handle the errors like IO Errors etc.

There are 2 Types of Exceptions

1. Checked Exceptions: It is one of the type of Exception where It's mandatory to handle. eg. SQLException.

2. Unchecked Exceptions: It is one of those Exception which let you make your own choice weather to handle the Exception or not.

### Exception Handling

```java
try {
    /* ...Critical Statements...*/
} catch (Exception exception) {
    /* ...Exception Handler Code... */
}
```

It can have multiple catch after `try` block such that we can catch multiple Exceptions. If We want to handle Specific Exception, It can be done by replacing `Exception` with Specific Exception or Custom Exception. eg. ArithmeticException

It's always good idea to have `Exception` as last `catch` Block, because in any case if Exception is not handled with Specific Exception then It would be handle by `Exception` which is Super class of all the Exception.

Object => Throwable => Error, Exceptions.

### Throw

It is used to throw Exception manually.

```java
try {
    int a = 10;
    int b = 20;
    if(b == 0) {
        throw new ArithmeticException("Can't Divide by Zero");
    }
    int c = a / b;
} catch (Exception e) {
    System.out.println("Exception Thrown!");
}
```

### Custom Exception

All the Exceptions are thrown with It's super class called `Exception`. So, in order to have our custom exception we are required to extends `Exception` or `RuntimeException` Class.

```java
class MyException extends RuntimeException {
    public MyException(String message) {
        super(message);
    }
}
```

Now we can throw our Custom Exception as `throw new MyException("Invalid Stuff");`

### Throws

`Throws` is used to let parent method handle the Exception.

```java
void show() throws Exception {
    // Hey Parent, Handle my Exception
}
```

Any Exception thrown in above method will be handle by It's Parent Method. It's possible to handle chain of throws and the root method will handle the Exception.

### Try with Resources

Sometimes We need to close the resource we are working with. eg. SQL Connection, FileDescriptor etc.

We can make use of `finally` block which will always execute no matter Exception occurs or not. but There is a better way.

```java
// Using Finally Block
try {
    // Open SQL Connection
} catch(SQLException e) {
    // Handle Exception while opening connection
} finally {
    // Close SQL Connection
}

// Using try() Syntax
try(/*Open SQL Connection*/) {

} catch() {

}
```

If We use `try()` syntax then we don't need to close the connection manually. It will get close automatically.

## Threads

A Thread is a lightweight process. There are couple of ways to create threads in Java.

```java
class A extends Thread {
    public void run() {

    }
}
class B extends Thread {
    public void run() {

    }
}

class Main {
    public static void main(String []args) {
        A obj1 = new A();
        obj1.start();

        B obj2 = new B();
        obj2.start();
    }
}
```

Thread also has some priority which is between 1 to 10. The Default Priority of Thread is 5. It's changeable too.

```java
obj1.setPriority(9);
```

For setting Maximum Priority we can use `Thread.MAX_PRIORITY` and for minimum priority `Thread.MIN_PRIORITY`.

We can also make the thread sleep with `Thread.sleep(100);` The Thread will sleep for 100 Milliseconds.

### Thread using Runnable

```java
class A implements Runnable {
    public void run() {

    }
}

class B implements Runnable {
    public void run() {

    }
}

class Main {
    public static void main(String []args) {
        A obj1 = new A();
        B obj2 = new B();

        Thread t1 = new Thread(obj1);
        Thread t2 = new Thread(obj2);
        t1.start();
        t2.start();
    }
}
```

### Race Condition

While working with Thread There might be condition where multiple threads are in race to access the resource and eventually leads to infinity waiting that is called `Race Condition`.

We might loose the data while working with same resources with multiple threads.

We use `synchronized` keyword to Race Condition this problem.

```java
class Counter {
    private int count = 0;
    public synchronized void increment() {
        count++;
    }
}
```

## Collections

`Collections` in java provides architecture to store and work with different types of objects. It provides many interfaces like ArrayList, List, Stack, Queue, Priority Queue, Tree, HashSet, Set, Map etc.

- **List**: ArrayList, LinkedList
- **Queue**: DeQueue
- **Set**: HashSet, LinkedHashSet
- **Map**: HashMap

### List Example

```java
Collection<Integer> nums = new ArrayList<Integer>();
List<Integer> numList= new ArrayList<Integer>();
```

### Set Example

```java
Set<Integer> numSet = new HashSet<Integer>();
// for sorted list
Set<Integer> numSetSorted = new TreeSet<Integer>();

while(numSet.hasNext()){
    System.out.println(numSet.next());
}
```

### Map Example

```java
Map<String, Integer> data = new HashMap<String, Integer>();
data.put("Om", 20);
System.out.println(data.get("Om")); // 20
System.out.println(data.keySet()); // [Om, ...]

// for sorted Data
List<Integer> numList = ArrayList<Integer>();
Collection.sort(numList);
// OR
Collection.sort(numList, com); // custom compare function
```

Example of custom Comparator Function

```java
Comparator<Integer> com = new Comparator<Integer>() {
    public int compare (Integer i , Integer j) {
        if (i % 10 > j % 10) {
            return true;
        } else {
            return false;
        }
    }
}
```

## Stream API

While using Collection sometimes we have to perform some Operations on our Collection. We can use loops to iterate the Collection and perform the actions on the Collection, but It makes code unreadable and messy, for better readability and easy to work on we can apply Stream on the Collections.

We can add a layer as filters, map or reduce and add some terminal operations at the end to access the applied result.

### To Print the ArrayList

```java
List<Integer> num = new ArrayList<Integer>();
num.add(5);
num.add(3);
num.add(6);
num.forEach(n -> System.out.println(n));
```

### Consumers

It is used to accept the result and it can call when we run accept method of the consumer.

```java
Consumer<List<Integer>> listNumber = listOfInt -> {
    for(Integer i: listOfInt) {
        System.out.println(i);
    }
}

listNumber.accept(Array.asList(1,2,3,4));
```

#### `andThen()` of Consumer

```java
Consumer<List<Integer>> listNumber1 = listOfInt -> {
    for(Integer i: listOfInt) {
        System.out.println(i);
    }
}

Consumer<List<Integer>> listNumber2 = listOfInt -> {
    for(Integer i: listOfInt) {
        System.out.println(i + 1);
    }
}

listNumber1.andThen(listNumber2).accept(Array.asList(1,2,3,4));
```

First it will run listNumber1 then It runs listNumber2 with given List.

> Stream can only be used once. Once you use it, It will get expired but It's possible to convert existing stream to the new Stream, as like wise we can perform multiple nested operations.

```java
List<Integer> numList = new ArrayList<Integer>();
Stream<Integer> s1 = numList.stream();
Stream<Integer> s2 = s1.filter(n -> n % 10);
// can't use s1 any more
```

Once `s1` is used, we can't use s1 any more but we can create another stream out of it which is `s2` and can s2 further.

Alternatively we can use . operator to perform multiple operation within one stream.

```java
int result = nums.stream()
    .filter(n -> n % 2 == 0)
    .map(n -> n * 2)
    .toList();
```

## Records

When we have all the class member variables as final then we can define record instead of class.

Generally, We use records to hold the data. eg. Request & Response Holder, as well as Database Response holder etc.

```java
public record Person(String name, int age) {
    public Person {
        if (name == "") {
            System.out.println("Name is Empty");
        }
    }
}

public class Main {
    public static void main(String []args) {
        Person person = new Person("Om", 20);
    }
}
```

## Sealed Classes

Sealed Class is used to restrict the access of the class. We specify the classes to which We want to give access to our class.

```java
public sealed class PremiumVehicle permits Audi, BMW, RR {
    /* ...body... */
}
```

The class `PremiumVehicle` is only accessible by `Audi, BMW, RR`. None other than those class can access the `PremiumVehicle`.
