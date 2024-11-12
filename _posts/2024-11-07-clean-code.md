---
title: Clean Code (Robert C Martin)- Notes
date: 2024-11-07 10:00:00 -500
categories: [book-notes, clean-code]
tags: [clean-code]
---

## Introduction

There are two parts to learning craftsmanship: knowledge and work. Learning to write clean code is hard work. It requires more than just the knowledge of principles and patterns. You must sweat over it. You must practice it yourself, and watch yourself fail. You must watch others practice it and fail.

## 1. Clean Code

By following clean code, we want to become better programmers.

### There Will Be Code

Someone might argue that, code will not more needed hence programmer won't be needed because business people will generate programs from specifications.

We will never be rid of code, because code represents the details of the requirements. At some level those details cannot be ignored or abstracted

Remember that code is really the language in which we ultimately express the requirements. We may create languages that are closer to the requirements. We may create tools that help us parse and assemble those requirements into formal structures. But we will never eliminate necessary precision—so there will always be code.

### Bad Code

Author knows a company, who wrote a _killer_ app. Company basically rushed the product to market and has made a huge mess in the code such that they aren't able to fix bugs in next release cycle and as they add more and more features it was getting worst until they simply could not manage it any longer. _It was the bad code that brought the company down_

We probably faced or write bad code, when we don't have time to do the job, the boss will angry if we take any more time to clean up the code. Eventually we leave it for another day to fix that.

### The Total Cost of Owning a Mess

If you have been a programmer for longer than two or three years, you have probably been slowed down by messy code. The degree of the slowdown can be significant. Teams that were moving very fast at the beginning of a project can find themselves moving at a snail’s pace. It takes time to understand any addition or modification in the code.

As the mess builds, the productivity of the team continues to decrease. They add more staff to the project in hopes of increasing productivity.

#### The Grand Redesign in the Sky

Eventually the team rebels. They inform management that they cannot continue to develop in this odious code base but they cannot deny that productivity is terrible. Eventually lands up to redesign the system.

A new tiger team is selected. Everyone wants to be on this team because it’s a green-field project. Management will not replace the old system until the new system can do everything that the old system does.

#### Attitude

We might have commonly seen the conditions where something took week to do what should have taken hours? OR We should have been a one-line change, made instead of hundreds of different modules?

Why does that happen? All time we blamed stupid managers, colleagues, and so and so forth, but the truth is We are unprofessional.

It's common to blame somebody for bad design of the project, Even Mangers and marketers look to us for information they need to make promises and commitments.

Managers may defend the schedule and requirements with passion, but it's their job. It's our job to defend the code with equal passion.

It is unprofessional for programmers to bend to the will of managers who don’t understand the risks of making messes.

#### The Primal Conundrum

All developers with more than a few years of experience know that the previous mess slowed them down, but still they feel the pressure to make messes in order to meet deadlines.

True professional takes care of new mess coming in the way, they try hard to write code as clean as possible to avoid that mistake again.

#### The Art of Clean Code?

Most important for us is not just to identify the bad code from any code, We should know how to write clean code.

Writing clean code requires the disciplined use of myriad little techniques applied through a acquired sense of "cleanliness". The "code-sense" is the key.

A programmer without "code-sense" will have no idea what to do when they found messy code. A programmer with "code-sense" will have options and variants to fix when they find messy code.

#### What Is Clean Code?

Author asked to well-known and deeply experienced programmers, what they thought.

- Bjarne Stroustrup (Inventor of C++)

_I like my code to be elegant and efficient. The logic should be straightforward to make it hard for bugs to hide, the dependencies minimal to ease maintenance, error handling complete according to an articulated strategy, and performance close to optimal so as not to tempt people to make the code messy with unprincipled optimizations. Clean code does one thing well._ - Elegant (Pleasing): Clean code is pleasing to read, it makes you smile. - Efficiency: Expected from inventor of C++ - Tempts: Bad code tempts the mess to grow! - Error handling should be complete - Shows discipline of paying attention to details.

- Grady Booch, author of _Object Oriented Analysis and Design with Applications_

_Clean code is simple and direct. Clean code reads like well-written prose. Clean code never obscures the designer’s intent but rather is full of crisp abstractions and straightforward lines of control._ - Readability perspective - Live novel, clean code should clearly expose the tension in the problem to be solved. - Crisp Abstraction ("crisp" near to word concrete)

- “Big" Dave Thomas, founder of OTI, godfather of the Eclipse strategy

_Clean code can be read, and enhanced by a developer other than its original author. It has unit and acceptance tests. It has meaningful names. It provides one way rather than many ways for doing one thing. It has minimal dependencies, which are explicitly defined, and provides a clear and minimal API. Code should be literate since depending on the language, not all necessary information can be expressed clearly in code alone._ - Desire for readability - Code without test is not clean - Minimal: Smaller code is better

- Michael Feathers, author of _Working Effectively with Legacy Code_

_I could list all of the qualities that I notice in clean code, but there is one overarching quality that leads to all of them. Clean code always looks like it was written by someone who cares. There is nothing obvious that you can do to make it better. All of those things were thought about by the code’s author, and if you try to imagine improvements, you’re led back to where you are, sitting in appreciation of the code someone left for you—code left by someone who cares deeply about the craft._

- Ron Jeffries, author of *Extreme Programming Installed* and *Extreme Programming Adventures in C#*

_In recent years I begin, and nearly end, with Beck’s rules of simple code. In priority order, simple code:_
• _Runs all the tests;_
• _Contains no duplication;_
• _Expresses all the design ideas that are in the system;_
• _Minimizes the number of entities such as classes, methods, functions, and the like._
Mainly his idea is to have No duplication, one thing, expressiveness, tiny abstractions.

- Ward Cunningham, inventor of Wiki, inventor of Fit, coinventor of eXtreme Programming. Motive force behind Design Patterns. Smalltalk and OO thought leader. The godfather of all those who care about code.

_You know you are working on clean code when each routine you read turns out to be pretty much what you expected. You can call it beautiful code when the code also makes it look like the language was made for the problem._ - He expects that when you read clean code, you won't be surprised at all. - You will read it, and it will be pretty much what you expected.

### Schools of Thought

Martial artists do not all agree about the best martial art, or the best technique within a martial art. Often master martial artists will form their own schools of thought and gather students to learn from them.

Author mentioned that We spent more time reading the code rather writing the code. We spent around 10:1 ratio of reading:writing the code. Because this ratio is so high, we want the reading of code to be easy, even if it makes the writing harder.

### The Boy Scout Rule

_Leave the campground cleaner than you found it._

The idea is to keep the code clean over time. We've all seen code rot and degrade as time passes. So we must take an active role in preventing this degradation.

The cleanup doesn't need to be something big, Changing variable names for the better, break up code into well named functions, eliminate small bit of duplication, clean up composite `if` statement.

## 2. Meaningful Names

### Introduction

Names are everywhere in software, We name our variables, functions, arguments, classes, methods etc. Because We do so much of it, We'd better do it well.

### Use Intention-Revealing Name

It is easy to say that names should reveal intent. Choosing good names take time but saves more than it takes.

If a name requires a comment, then the name does not reveal its intent

```java
int d; // elapsed time in days
```

The name `d` reveals nothing, It doesn't evoke a sense of elapsed time, nor of days. better we should choose...

```java
int elapsedTimeInDays;

int daysSinceCreation;

int daysSinceModification;

int fileAgeInDays;
```

What is the purpose of this code?

```java
public List<int[]> getThem() {
	List<int[]> list1 = new ArrayList<int[]>();
	for (int[] x : theList)
		if (x[0] == 4)
			list1.add(x);
	return list1;
}
```

The problem is not simplicity but it's **implicity** of the code, The code implicitly requires that we know the answer to question like, What kind of things are in `theList`? What is the significance of the value 4? etc.

```java
public List<int[]> getFlaggedCells() {
	List<int[]> flaggedCells = new ArrayList<int[]>();
	for (int[] cell : gameBoard)
		if (cell[STATUS_VALUE] == FLAGGED)
			flaggedCells.add(cell);
	return flaggedCells;
}
```

Notice that the simplicity of the code has not changed but the code has become much more explicit.

We can even go further and write a simple class for cells instead of using an array of `int`s. It can include an intention-revealing function (call it `isFlagged`) to hide the magic numbers.

```java
public List<Cell> getFlaggedCells() {
	List<Cell> flaggedCells = new ArrayList<Cell>();
	for (Cell cell : gameBoard)
		if (cell.isFlagged())
			flaggedCells.add(cell);
	return flaggedCells;
}
```

With these simple changes, it's not difficult to understand what's going on. This is the power of choosing good names.

### Avoid Disinformation

Programmers must avoid leaving false clues that obscure the meaning of code. We want to avoid poor variable names such as `hp, aix, sco` etc.

Do not refer to a grouping of accounts as an `accountList` unless it's actually a `List` otherwise, it may lead to false conclusions. So `accountGroup` or `bunchOfAccoutns` or just plain `accounts` would be better.

Beware of using names which vary in small ways. eg. `XYZControllerForEfficientHandlingOfStrings` and `XYZControllerForEfficientStorageOfStrings`, It takes time to spot the subtle difference between both. If We're using IDE it's common mistake to write incorrect variable name while we use few letter and use auto completion.

A truly awful example of disinformative names would be the lower-case `L` or uppercase `O`.

```java
int a = l;
if ( O == l )
	a = O1;
else
	l = 01;
```

### Make Meaningful Distinctions

Programmer create problems for themselves when they write code solely to satisfy a compiler or interpreter.

Consider naming a variable name `klass` just because `class` is used for something else. We need to make sure that if names are different then they should also mean something.

It is not sufficient to add number series or noise words, even though the compiler is satisfied.

```java
public static void copyChars(char a1[], char a2[]) {
	for (int i = 0; i < a1.length; i++) {
		a2[i] = a1[i];
	}
}
```

This function reads much better when `source` and `destination` are used for the argument names.

Noise words are another meaningless distinction. Consider you have a `Product` class. If you have another called `ProductInfo` or `ProductData`, you have made the names different without making them mean anything different.

There is nothing wrong in using prefix conventions like `a` and `the` so long as they make meaningful distinction.

We want to avoid common given up practices, like...

- avoid `variable` as variable name, `table` as table name and so on
- avoid `nameString` as String variable name, Would a `Name` ever be a floating point number?
- avoid naming one class as `Customer` and another as `CustomerObject`.

There is an application we know of where this is illustrated, We've changed the names to protect the guilty.

```java
getActiveAccount();

getActiveAccounts();

getActiveAccountInfo();
```

How programmers supposed to know which one to call?

Similarly, `moneyAmount` is indistinguishable from `money`, `customerInfo` is indistinguishable from `customer`, `accountData` is indistinguishable from `account`. Distinguish names in such a way that the reader knows what the differences offer.

### Use Pronounceable Names

Humans are good at words, and words are by definition, pronounceable.

One company has `genymdhms` (generation date, year, month, day, hour, minute, and second). People were tolerating poor naming but Every new developer to have the variables explained to them.

```java
class DtaRcrd102 {
	private Date genymdhms;
	private Date modymdhms;
	private final String pszqint = "102";
	/* … */
};
```

```java
class Customer {
	private Date generationTimestamp;
	private Date modificationTimestamp;;
	private final String recordId = "102";
	/* … */
};
```

Compare above 2 code blocks, with second block, intelligent conversation is not possible, everybody will sue generation timestamp in their conversation.

### Use Searchable Names

Single-letter names and numeric constants have a particular problem in that they are not easy to locate across a body of text.

Easy to find: `MAX_CLASSES_PER_STUDENT`, but the number `7` could be more troublesome.

Likewise, the name `e` is a poor choice for any variable for which a programmer might need to search, It is the most common letter in the English language and likely to show up in every passage of text in every program.

Single-letter can ONLY be used as local variable inside short methods.

Compare

```java
for (int j=0; j<34; j++) {
	s += (t[j]*4)/5;
}
```

To

```java
int realDaysPerIdealDay = 4;
const int WORK_DAYS_PER_WEEK = 5;
int sum = 0;
for (int j=0; j < NUMBER_OF_TASKS; j++) {
	int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
	int realTaskWeeks = (realdays / WORK_DAYS_PER_WEEK);
	sum += realTaskWeeks;
}
```

In second block, `sum` is not particularly useful name but at least is searchable. It is more easy to search `WORK_DAYS_PER_WEEK` instead of number `5`.

### Avoid Encodings

We must avoid extra encoding layer on top of English language, It requires each new employee to learn yet another encoding "language" in addition to learning the body of code.

#### Hungarian Notation

Older programming languages (like Fortran and early BASIC) had limitations that forced programmers to use naming conventions, such as Hungarian Notation (HN), to encode variable types for easier identification.

Widely used in early Windows C API development to manage variables of various types (handles, pointers, strings) when compilers couldn’t enforce type safety.

Current programming languages have richer type systems and compilers that enforce types, reducing the need for such conventions.

Modern IDEs and editors can detect type errors early, providing additional support to programmers.

Using type encoding (like HN) today is discouraged as it complicates code maintenance, makes reading harder, and introduces potential for misinterpretation, especially with easily changeable names and types.

```java
PhoneNumber phoneString;
// name not changed when type changed!
```

#### Member Prefixes

We don't need to prefix member variable with `m_` anymore, while classes and functions should be small enough that you don't need them.

We should better prefer IDE or Editor that clearly highlights or colorizes to make them distinct.

```java
public class Part {
	private String m_dsc; // The textual description
	void setName(String name) {
		m_dsc = name;
	}
}

// --------------------------------------------

public class Part {
	String description;
	void setDescription(String description) {
		this.description = description;
	}
}
```

#### Interfaces and Implementations

There are sometimes a special case for encoding. For example We are building an ABSTRACT FACTORY for the creation of shapes. This factory will be an interface and will be implemented by a concrete class. What should we name them? `IShapeFactory` and `ShapeFactory`?

We don't want our users knowing that I'm handling them an interface. We just want them to know that it's `ShapeFactory`.

### Avoid Mental Mapping

Readers should not have to mentally translate our names into other names they already know.

For single-letter variable names, Certainly a loop counter may be names `i` or `j` or `k` (though never `l`!) If it's scope is very small and no other names can conflict with it.

There can be no worst reason for using the name `c` then because `a` and `b` were already taken.

In general programmers are pretty smart people. Smart people sometimes like to show off their smarts by demonstrating their mental juggling abilities.

One difference between a smart programmer and a professional programmer is that the professional understands that _clarity is king_. Professionals use their powers for good and write code that others can understand.

### Class Names

Classes and objects should have noun or noun phrase names like `Customer`, `WikiPage`, `Account`, and `AddressParser`. Avoid words like `Manager`, `Processor`, `Data`, or `Info` in the name of a class. A class name should not be a verb.

### Method Names

Methods should have verb or verb phrase names like `postPayment`, `deletePage`, or `save`. Accessors, mutators, and predicates should be named for their value and prefixed with `get`, `set`, and `is` according to the javabean standard.

### Don't Be Cute

Choose clarity over entertainment value. For example, instead of choosing cute function name `HolyHandGrenade` , choose `DeleteItems`.

Say what you mean, Mean what you say.

### Pick One Word per Concept

Pick one word for one abstract concepts and stick with it. For instance, it's confusing to have `fetch`, `retrieve`, and `get` as equivalent methods of different classes.

Likewise, It's confusing to have a `controller` and a `manager` and a `driver` in the same code base. What is the essential different between a `DeviceManager` and a `Protocol-Controller`? Why are both not `controllers` or both not `managers`?

A consistent lexicon is a great boon to the programmers who must use your code.

### Don't Pun

Avoid using the same word for two purposes. Using the same term for two different ideas is essentially a pun.

Using consistent naming, like `add`, can be misleading if the method's behavior differs semantically from other `add` methods.

If a new method places a single parameter into a collection, using `add` may seem consistent but is incorrect.

Instead, choose names like `insert` or `append` would be more meaningful, keeping method name `add` will be pun.

### Use Solution Domain Names

Remember that the people who read your code will be programmers, so go head and use Computer Science terms, Algorithms names, Pattern Names, Math terms and so forth.

The name `AccountVisitor` means a great deal to a programmer who is familiar with the VISITOR pattern. What programmer would not know what a `JobQueue` was?

### Use Problem Domain Names

When there is no "programmer-eese" for what you're doing, use the name from the problem domain. Product people and PRDs will help in-case programmer looking for context.

Separating solution and problem domain concepts is part of the job of a good programmer and designer.

### Add Meaningful Context

There are a few names which are meaningful in and of themselves.

Imagine that you have variables named `firstName`, `lastName`, `street` and `zipcode`. Taken together it's pretty clear that they form an address. But what if you saw `state` variable being used alone in a method?

You can add context by using prefixes: `addrFirstName`, `addrLastName`, `addrState` and so on. Of course, a better solution is to create a class named `Address`.

Take a look at this code...

```java
private void printGuessStatistics(char candidate, int count) {
    String number;
    String verb;
    String pluralModifier;
    if (count == 0) {
        number = "no";
        verb = "are";
        pluralModifier = "s";
    } else if (count == 1) {
        number = "1";
        verb = "is";
        pluralModifier = "";
    } else {
        number = Integer.toString(count);
        verb = "are";
        pluralModifier = "s";
    }
    String guessMessage = String.format("There % s % s % s % s", verb, number, candidate, pluralModifier);
    print(guessMessage);
}
```

The function is a bit too long and the variables are used throughout. To split the function into smaller pieces we need to create a `GuessStatisticsMessage` class and make the three variables fields of this class. This provides a clear context for the three variables. They are _definitively_ part of the `GuessStatisticsMessage`. The improvement of context also allows the algorithm to be made much cleaner by breaking it into many smaller functions.

```java
public class GuessStatisticsMessage {
    private String number;
    private String verb;
    private String pluralModifier;

    public String make(char candidate, int count) {
        createPluralDependentMessageParts(count);
        return String.format(
            "There %s %s %s%s",
            verb, number, candidate, pluralModifier);
    }

    private void createPluralDependentMessageParts(int count) {
        if (count == 0) {
            thereAreNoLetters();
        } else if (count == 1) {
            thereIsOneLetter();
        } else {
            thereAreManyLetters(count);
        }
    }

    private void thereAreManyLetters(int count) {
        number = Integer.toString(count);
        verb = "are";
        pluralModifier = "s";
    }

    private void thereIsOneLetter() {
        number = "1";
        verb = "is";
        pluralModifier = "";
    }

    private void thereAreNoLetters() {
        number = "no";
        verb = "are";
        pluralModifier = "s";
    }
}
```

### Don't Add Gratuitous Context

In an imaginary application called "Gas Station Deluxe," it is a bad idea to prefix every class with `GSD`. When you type `G` it rewarded with mile-list of every class in the system.

Likewise, say you invented `MailingAddress` class in `GSD`'s accounting method and named it `GSDAccountAddress`. Later you need to use for customer contact application. Do you use `GSDAccountAddress`? Does it sound like the right name? Ten of 17 characters are redundant or irrelevant.

Shorter names are generally better than longer ones, so long as they are clear. Add no more context to a name than is necessary.

The names `accountAddress` and `customerAddress` are fine names for instances of the class `Address` but could be poor names for classes. `Address` is a fine name for a class.

## 3. Functions

Dumping everything in a single function will end up code mess, There will be too many context switch in a single function and increase levels of abstractions.

However, with just a few simple method extractions, some renaming and a little restructuring, It's clearly understandable with in approx 3x less time.

How to make function easy to read and understand? How can we make a function communicate its intent? What attributes can we give our functions that will allow a casual reader to intuit the kind of program they live inside?

### Small!
