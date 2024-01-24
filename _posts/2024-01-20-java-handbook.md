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
// image

When Java program compiles by `javac` compiler the Java code converted into `byte code` that is then understood by the JVM and then `byte code` is converted into `machine code`.

// image
### JVM (Java Virtual Machine)
Java Virtual Machine is platform dependent that means it needs to be install on every machine required to run Java Program. while Java Program is Java Independent that means Java Program developed on one machine can execute on all the Machines which has JVM Install.

JVM is used to convert `byte code` to `machine code`.

JVM consist of JIT (Just-In-Time) which is used to improve the performance by compiler the `byte code` to `machine code`.

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
|-----------------|---------------------|
| Integer         | Array               |
| Float           | Class               |
| Character       | Interfaces          |
| Boolean         | Strings             |
|                 | Enums               |

### Integers

| Integers | Size    |
|----------|---------|
| int      | 4 bytes |
| long     | 8 bytes |
| short    | 2 byte  |
| byte     | 1 byte  |

### Floats

| Floats | Size    |
|--------|---------|
| float  | 4 bytes |
| double | 8 bytes |

### Others

| Others     | Size    |
|------------|---------|
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
