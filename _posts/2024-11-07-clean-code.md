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

If you have been a programmer for longer than two or three years, you have probably been slowed down by messy code. The degree of the slowdown can be significant. Teams that were moving very fast at the beginning of a project can find themselves moving at a snail's pace. It takes time to understand any addition or modification in the code.

As the mess builds, the productivity of the team continues to decrease. They add more staff to the project in hopes of increasing productivity.

#### The Grand Redesign in the Sky

Eventually the team rebels. They inform management that they cannot continue to develop in this odious code base but they cannot deny that productivity is terrible. Eventually lands up to redesign the system.

A new tiger team is selected. Everyone wants to be on this team because it's a green-field project. Management will not replace the old system until the new system can do everything that the old system does.

#### Attitude

We might have commonly seen the conditions where something took week to do what should have taken hours? OR We should have been a one-line change, made instead of hundreds of different modules?

Why does that happen? All time we blamed stupid managers, colleagues, and so and so forth, but the truth is We are unprofessional.

It's common to blame somebody for bad design of the project, Even Mangers and marketers look to us for information they need to make promises and commitments.

Managers may defend the schedule and requirements with passion, but it's their job. It's our job to defend the code with equal passion.

It is unprofessional for programmers to bend to the will of managers who don't understand the risks of making messes.

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

_Clean code is simple and direct. Clean code reads like well-written prose. Clean code never obscures the designer's intent but rather is full of crisp abstractions and straightforward lines of control._ - Readability perspective - Live novel, clean code should clearly expose the tension in the problem to be solved. - Crisp Abstraction ("crisp" near to word concrete)

- "Big" Dave Thomas, founder of OTI, godfather of the Eclipse strategy

_Clean code can be read, and enhanced by a developer other than its original author. It has unit and acceptance tests. It has meaningful names. It provides one way rather than many ways for doing one thing. It has minimal dependencies, which are explicitly defined, and provides a clear and minimal API. Code should be literate since depending on the language, not all necessary information can be expressed clearly in code alone._ - Desire for readability - Code without test is not clean - Minimal: Smaller code is better

- Michael Feathers, author of _Working Effectively with Legacy Code_

_I could list all of the qualities that I notice in clean code, but there is one overarching quality that leads to all of them. Clean code always looks like it was written by someone who cares. There is nothing obvious that you can do to make it better. All of those things were thought about by the code's author, and if you try to imagine improvements, you're led back to where you are, sitting in appreciation of the code someone left for you—code left by someone who cares deeply about the craft._

- Ron Jeffries, author of _Extreme Programming Installed_ and _Extreme Programming Adventures in C#_

_In recent years I begin, and nearly end, with Beck's rules of simple code. In priority order, simple code:_
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

Widely used in early Windows C API development to manage variables of various types (handles, pointers, strings) when compilers couldn't enforce type safety.

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

The first rule of function is that they should be small. The second rule of the function is that _they should be smaller than that_.

In eighties, People used to say that a function should be no bigger than a screen full. Function should hardly ever be 20 lines long.

Uncle Bob visited Kent Beck at this home. They sat down and did some programming together. Kent Beck showed the code and Uncle Bob was amazed by looking at small functions. Each function was transparently obvious.

#### Blocks and Indenting

This implies that the blocks within `if` statements, `else` statements, `while` statements, and so on should be one line long.

This also implies that the function should not be large enough to hold nested structure. Therefore, the indent level of a function should not be greater than one or two. This, of course, makes the function easier to read and understand.

### Do One Thing

**_FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL. THEY SHOULD DO IT ONLY._**

If a function does only those steps that are one level below the stated name of the function, then the function is doing one thing. For example

```java
public static String renderPageWithSetupsAndTeardowns(
	PageData pageData, boolean isSuite) throws Exception {
    if (isTestPage(pageData))
	   includeSetupAndTeardownPages(pageData, isSuite);
    return pageData.getHtml();
}
```

If we want to extract function again, we could extract `if` condition in above code, but that would simply restates the code without changing the level of abstraction.

#### Sections within Functions

```java
import java.util.*;

public class GeneratePrimes {
    /**
     * @param maxValue is the generation limit.
     */
    public static int[] generatePrimes(int maxValue) {
        if (maxValue >= 2) // the only valid case
        {
            // declarations
            int s = maxValue + 1; // size of array
            boolean[] f = new boolean[s];
            int i;
            // initialize array to true.
            for (i = 0; i < s; i++)
                f[i] = true;

            // get rid of known non-primes
            f[0] = f[1] = false;

            // sieve
            int j;
            for (i = 2; i < Math.sqrt(s) + 1; i++) {
                if (f[i]) // if i is uncrossed, cross its multiples.
                {
                    for (j = 2 * i; j < s; j += i)
                        f[j] = false; // multiple is not prime
                }
            }

            // how many primes are there?
            int count = 0;
            for (i = 0; i < s; i++) {
                if (f[i])
                    count++; // bump count.
            }

            int[] primes = new int[count];

            // move the primes into the result
            for (i = 0, j = 0; i < s; i++) {
                if (f[i]) // if prime
                    primes[j++] = i;
            }

            return primes; // return the primes
        } else // maxValue < 2
            return new int[0]; // return null array if bad input.
    }
}
```

This is an obvious symptom of doing more than one thing. Functions that do one thing cannot be reasonably divided into sections.

### One Level of Abstraction per Function

In order to make sure our functions are doing **one thing**, we need to make sure that the statements within our function are all at the same level of abstraction.

Mixing levels of abstraction within a function is always confusing.

#### Reading Code from Top to Bottom: _The Stepdown Rule_

We want the code to read like a top-down narrative. We want every function to be followed by those at the next level of abstraction so that we can read the program, descending one level of abstraction at a time as we read down the list of functions. Author calls this _The Step-down Rule_.

It turns out to be very difficult for programmers to learn to follow this rule and write functions that stay at a single level of abstraction. But learning this trick is also very important.

It is the key to keeping functions short and making sure they do "one thing."

### Switch Statements

It's hard to make a small `switch` statement. It is also hard to make `switch` statement that does one thing. By their nature `switch` statement always do _N_ things.

```java
public Money calculatePay(Employee e)
throws InvalidEmployeeType {
    switch (e.type) {
        case COMMISSIONED:
            return calculateCommissionedPay(e);
        case HOURLY:
            return calculateHourlyPay(e);
        case SALARIED:
            return calculateSalariedPay(e);
        default:
            throw new InvalidEmployeeType(e.type);
    }
}
```

Potential issues with above code

- It's large!
- When new employee types are added, it will grow
- It very clearly does more than one thing
- It violates the Single Responsibility Principle (SRP), because there is more than one reason for it to change.
- It violates Open Closed Principle (OCP) because it mush change whenever new types are added.

Using multiple functions with a switch statement to handle different Employee types results in poor code structure.

We may have similar structure for multiple methods, such as...

```java
isPayday(Employee e, Date date),

// OR

deliverPay(Employee e, Money pay),
```

Hide the switch statement inside an **Abstract Factory**, which handles creating appropriate Employee instances.

This allows methods like `calculatePay`, `isPayday`, and `deliverPay` to be called polymorphically, improving code organization and maintainability.

### Use Descriptive Names

The names should describe what the function does. It is hard to overestimate the value of good names.

Remember Ward's principle: "_You know you are working on clean code when each routine turns out to be pretty much what you expected._"

Half the battle to achieving that principle is choosing good names for small functions that do one thing.

Don't be afraid to make a name long. A long descriptive name is better than a short enigmatic name.

Choosing descriptive names will clarify the design of the module in your mind and help you to improve it. Be consistent in your names. Use the same phrases, nouns, and verbs in the function names you choose for your modules.

### Function Arguments

The ideal number of arguments for a function is zero (niladic). Next comes one (monadic), followed closely by two (dyadic). Three arguments (triadic) should be avoided where possible. More than three (polyadic) requires very special justification—and then shouldn't be used anyway.

Arguments are hard. They take a lot of conceptual power. When you are reading the story told by the module, `includeSetupPage()` is easier to understand than `includeSetupPageInto(newPage-Content)`. The argument is at a different level of abstraction than the function name and forces you to know a detail.

Arguments are even harder from a testing point of view, more than 2 arguments will make testing the function hard.

Output arguments are harder to understand than input arguments.

#### Common Monadic Forms

There are two common reasons to pass a single argument into a function:

1. **To ask a question about the argument**, like in `boolean fileExists("MyFile")`, where the function checks something about the input.
2. **To transform the argument** into something else and return the result, like `InputStream fileOpen("MyFile")`, which converts a file name into an InputStream.

These are the patterns readers expect, so it's important to name functions clearly and use them consistently.

A less common but useful case for single-argument functions is when they act as **events**. Here, the argument doesn't return anything but signals a state change, like `void passwordAttemptFailedNtimes(int attempts)`. This should be used carefully and should clearly indicate it's an event.

Avoid confusing single-argument functions that don't fit these patterns. For example, using an argument to pass back output (instead of returning it) can make the function harder to understand. A function that transforms input should always return the transformed value rather than altering an argument directly.

#### Flag Arguments

Flag arguments are ugly. The function does more than one thing. It does one thing if the flag is true and another if the flag is false!

The method call `render(true)` is just plain confusing to a poor reader. Mousing over the call and seeing `render(boolean isSuite)` helps a little, but not that much. We should have split the function into two: `renderForSuite()` and `renderForSingleTest()`.

#### Dyadic Functions

A function with two arguments is harder to understand than a monadic (single argument) function.

For Example,

```java
writeField(name)
```

is easier to understand then

```java
writeField(output-stream, name)
```

It takes a pause to ignore first parameter, while we should never ignore any part of code. The parts we ignore are where the bugs will hide.

There are times, of course, where two arguments are appropriate. For example, `Point p = new Point(0,0);` is perfectly reasonable.

Even obvious dyadic functions like `assertEquals(expected, actual)` are problematic. How many times have you put the `actual` where the `expected` should be?

#### Triads

Functions that take three arguments are significantly harder to understand than dyads. The issues of ordering, pausing, and ignoring are more than doubled. Think very carefully before creating a triad.

For example, consider the common overload of `assertEquals` that takes three arguments: `assertEquals(message, expected, actual)`. How many times have you read the `message` and thought it was the `expected`?

#### Argument Objects

When a function seems to need more than two or three arguments, it is likely that some of those arguments ought to be wrapped into a class of their own. Consider, for example...

```java
Circle makeCircle(double x, double y, double radius);
Circle makeCircle(Point center, double radius);
```

Reducing the number of arguments by creating objects out of them may seem like cheating, but it's not.

#### Argument Lists

Sometimes we want to pass a variable number of arguments into a function. Consider, for example, the `String.format` method:

```java
String.format("%s worked %.2f hours.", name, hours);
```

If the variable arguments are all treated identically, as they are in the example above, then they are equivalent to a single argument of type `List`.

```java
void monad(Integer… args);
void dyad(String name, Integer… args);
void triad(String name, int count, Integer… args);
```

#### Verbs and Keywords

Choosing good names for a function can go a long way toward explaining the intent of the function and the order and intent of the arguments.

For example, `write(name)` is very evocative. Whatever this "name" thing is, it is being "written." An even better name might be `writeField(name)`, which tells us that the "name" thing is a "field."

For example, `assertEquals` might be better written as `assertExpectedEqualsActual(expected,` `actual)`.

### Have No Side Effects

Side effects are lies. Your function promises to do one thing, but it also does other _hidden_ things.

```java
public class UserValidator {
    private Cryptographer cryptographer;

    public boolean checkPassword(String userName, String password) {
        User user = UserGateway.findByName(userName);
        if (user != User.NULL) {
            String codedPhrase = user.
            getPhraseEncodedByPassword();
            String phrase = cryptographer.decrypt(codedPhrase, password);
            if ("Valid Password".equals(phrase)) {
                Session.initialize();
                return true;
            }
        }
        return false;
    }
}
```

This code has side effect, calling `Session.initialize()`, The name of function doesn't implies that it's also initializing session.

If this function goes out of over at abstracted level, it create side effect and it could be hard to recognize as well (hidden side effect).

In this case we might rename the function `checkPasswordAndInitializeSession`, though that certainly violates "Do one thing."

#### Output Arguments

Apparently, We see arguments as input arguments, it's natural for all to consider argument as inputs.

```java
appendFooter(s);
```

In this code, does this function append `s` as the footer or something? Is it input argument or output argument?

It doesn't take long to look at the function signature and see:

```java
public void appendFooter(StringBuffer report)
```

This clarifies the issue. Anything that forces you to check the function signature is equivalent to a double-take.

it would be better for `appendFooter` to be invoked as

```java
report.appendFooter();
```

In general output arguments should be avoided. If your function must change the state of something, have it change the state of its owning object.

### Command Query Separation

Functions should either do something or answer something, but not both. Either your function should change the state of an object, or it should return some information about that object.

```java
public boolean set(String attribute, String value);
```

This function sets the value of ta names attribute and returns `true` if it successful and `false` if no such attribute exists. Calling this leads to odd statement like:

```java
if (set("username", "john")) {
   ...
}
```

The author intended `set` to be a verb, but in the context of the `if` statement it _feels_ like an adjective. We should do something like:

```java
if (attributeExists("username")) {
    setAttribute("username", "unclebob");
	…
}
```

### Prefer Exceptions to Returning Error Codes

Returning error codes from command functions is a subtle violation of command query separation. It promotes commands being used as expressions in the predicates of `if` statements.

```java
if (deletePage(page) == E_OK)
```

When you return an error code, you create the problem that the caller must deal with the error immediately.

```java
if (deletePage(page) == E_OK) {
    if (registry.deleteReference(page.name) == E_OK) {
        if (configKeys.deleteKey(page.name.makeKey()) == E_OK) {
            logger.log("page deleted");
        } else {
            logger.log("configKey not deleted");
        }
    } else {
        logger.log("deleteReference from registry failed");
    }
} else {
    logger.log("delete failed");
    return E_ERROR;
}
```

On the other hand, if you use exceptions instead of returned error codes, then the error processing code can be separated from the happy path code and can be simplified:

```java
try {
    deletePage(page);
    registry.deleteReference(page.name);
    configKeys.deleteKey(page.name.makeKey());
} catch (Exception e) {
    logger.log(e.getMessage());
}
```

#### Extract Try/Catch Blocks

Try to extract the bodies of the `try` and `catch` blocks out into functions of their own.

```java
public void delete(Page page) {
    try {
        deletePageAndAllReferences(page);
    } catch (Exception e) {
        logError(e);
    }
}

private void deletePageAndAllReferences(Page page) throws Exception {
    deletePage(page);
    registry.deleteReference(page.name);
    configKeys.deleteKey(page.name.makeKey());
}

private void logError(Exception e) {
    logger.log(e.getMessage());
}
```

It's easy to look at block of code and ignore, For example error handling code in this code.

This provides a nice separation that makes the code easier to understand and modify.

#### Error Handling Is One Thing

Functions should do one thing. Error handling is one thing. Thus, a function that handles errors should do nothing else. if `try` exists in the function, it should be very first word of the function body, and there should be nothing after the `catch/finally` blocks.

#### The `Error.java` Dependency Magnet

Returning error codes usually implies that there is some class or `enum` in which all the error codes are defined.

```java
public enum Error {
    OK,
    INVALID,
    NO_SUCH,
    LOCKED,
    OUT_OF_RESOURCES,

    WAITING_FOR_EVENT;
}
```

This type of classes used widely in the code, addition/modification in this classes requires rebuild and redeploy. So people reuse old error codes instead of adding new ones.

When you use exceptions rather than error codes, then new exceptions are _derivatives_ of the exception class. They can be added without forcing any recompilation or redeployment.

### Don't Repeat Yourself

Duplication may be the root of all evil in software. Many principles and practices have been created for the purpose of controlling or eliminating it.

In databases, we focus on normalization to eliminate duplication of data. Consider how Object Oriented Programming serves the concentrate code into base classes that would otherwise be redundant.

### Structured Programming

Dijkstra said that every function, and every block within a function, should have one entry and one exit. Following these rules means that there should only be one `return` statement in a function, no `break` or `continue` statements in a loop, and never, _ever,_ any `goto` statements.

if you keep your functions small, then the occasional multiple `return`, `break`, or `continue` statement does no harm and can sometimes even be more expressive than the single-entry, single-exit rule.

### How Do You Write Functions Like This?

Writing software is like any other kind of writing. You thought down first before writing anything and change it until that reads better.

Author writes long and complicated function and then breaks it down, break down to new classes but also He have suite of unit tests that cover every one of those lines of code. They refine the code while keeping the tests passing.

## 4. Comments

Programming languages are descriptive enough, such that comments are mostly negligible.

The proper use of comments is to compensate for our failure to express ourselves in code. Note that Author used the word _failure_.

We must have them because we cannot always figure out how to express ourselves without them.

So when you find yourself in a position where you need to write a comment, think it through and see whether there isn't some way to turn the tables and express yourself in code. Every time you express yourself in code, you should pat yourself on the back. Every time you write a comment, you should feel the failure of your ability of expression.

Programmers should be disciplined enough to keep the comments in a high state of repair, relevance, and accuracy. they should. But I would rather that energy go toward making the code so clear and expressive that it does not need the comments in the first place.

Comments are sometimes necessary, we will expend significant energy to minimize them.

### Comments Do Not Make Up for Bad Code

Comments become necessity when code is bad, We better forced towards writing comment instead of cleaning the code.

Clear and expressive code with few comments is far superior to cluttered and complex code with lots of comments.

### Explain Yourself in Code

There are certainly times when code makes a poor vehicle for explanation.

```java
// Check to see if the employee is eligible for full benefits
if ((employee.flags & HOURLY_FLAG) &&
	(employee.age > 65))
```

can better be

```java
if (employee.isEligibleForFullBenefits())
```

It takes only a few seconds of thought to explain most of your intent in code.

### Good Comments

Some comments are necessary or beneficial.

#### Legal Comments

Sometimes our corporate coding standards force us to write certain comments for legal reasons.

```java
// Copyright (C) 2003,2004,2005 by Object Mentor, Inc. All rights reserved.
// Released under the terms of the GNU General Public License version 2 or later.
```

#### Informative Comments

It is sometimes useful to provide basic information with a comment. For example, consider this comment that explains the return value of an abstract method:

```java
// Returns an instance of the Responder being tested.
protected abstract Responder responderInstance();
```

A comment like this can sometimes be useful, but it is better to use the name of the function to convey the information where possible. eg. `responderBeingTested`

```java
// format matched kk:mm:ss EEE, MMM dd, yyyy
Pattern timeMatcher = Pattern.compile("\\d*:\\d*:\\d* \\w*, \\w* \\d*, \\d*");
```

In this case the comment lets us know that the regular expression is intended to match a time and date that were formatted with the `SimpleDateFormat.format` function using the specified format string.

#### Explanation of Intent

Sometimes a comment goes beyond just useful information about the implementation and provides the intent behind a decision.

```java
public int compareTo(Object o) {
     if (o instanceof WikiPagePath) {
         WikiPagePath p = (WikiPagePath) o;
         String compressedName = StringUtil.join(names, "");
         String compressedArgumentName = StringUtil.join(p.names, "");
         return compressedName.compareTo(compressedArgumentName);
     }
     return 1; // we are greater because we are the right type.
 }
```

You might not agree with the programmer's solution to the problem, but at least you know what he was trying to do.

#### Clarification

Sometimes it is just helpful to translate the meaning of some obscure argument or return value into something that's readable.

Clarification is important but it's risky too, while someone forget to change the comment while modifying code, It's become risk.

#### Warning of Consequences

Sometimes it is useful to warn other programmers about certain consequences. For example, here is a comment that explains why a particular test case is turned off:

```java
// Don't run unless you
// have some time to kill.
public void _testWithReallyBigFile() {
    writeLinesToFile(10000000);

    response.setBody(testFile);
    response.readyToSend(this);
    String responseString = output.toString();
    assertSubString("Content-Length: 1000000000", responseString);
    assertTrue(bytesSent > 1000000000);
}
```

Nowadays, of course, we'd turn off the test case by using the `@Ignore` attribute with an appropriate explanatory string. `@Ignore("Takes too long to run")`.

Another example:

```java
public static SimpleDateFormat makeStandardHttpDateFormat() {
    //SimpleDateFormat is not thread safe,
    //so we need to create each instance independently.
    SimpleDateFormat df = new SimpleDateFormat("EEE, dd MMM yyyy HH: mm: ss z");
    df.setTimeZone(TimeZone.getTimeZone("GMT"));
    return df;
}
```

#### TODO Comments

It is sometimes reasonable to leave "To do" notes in the form of `//TODO` comments. In latest IDEs and Editors TODO comments get highlights so that people can easily recognize it.

```java
//TODO-MdM these are not needed
// We expect this to go away when we do the checkout model
protected VersionInfo makeVersion() throws Exception {
    return null;
}
```

`TODO`s are jobs that the programmer thinks should be done, but for some reason can't do at the moment.

#### Amplification

A comment may be used to amplify the importance of something that may otherwise seem not so important.

```java
String listItemContent = match.group(3).trim();
// the trim is real important.  It removes the starting
// spaces that could cause the item to be recognized
// as another list.
new ListItemWidget(this, listItemContent, this.level + 1);
return buildList(text.substring(match.end()));
```

#### Javadocs in Public APIs

If you are writing a public API, then you should certainly write good javadocs for it.

There is nothing quite so helpful and satisfying as a well-described public API.

### Bad Comments

Most comments fall into this category. Usually they are excuses for poor code or justifications for insufficient decisions.

#### Mumbling

Plopping in a comment just because you feel you should or because the process requires it, is a hack.

```java
public void loadProperties() {
    try {
        String propertiesPath = propertiesLocation + "/" + PROPERTIES_FILE;
        FileInputStream propertiesStream = new FileInputStream(propertiesPath);
        loadedProperties.load(propertiesStream);
    } catch (IOException e) {
        // No properties files means all defaults are loaded
    }
}
```

What does that comment in the catch block mean?

The author seems to be unclear about how the code handles loading default properties when an `IOException` occurs. If there's no properties file, the defaults are supposedly loaded, but it's not clear who is actually doing this.

Questions arise, like: Were the defaults loaded before calling `loadProperties.load`? Did `loadProperties.load` handle the exception, load the defaults, and then let the exception go? Or did it load the defaults first, then try to load the file?

There's also concern that the empty `catch` block might indicate the author intended to handle it later but never did, which is worrisome.

#### Redundant Comments

```java
// Utility method that returns when this.closed is true. Throws an exception
// if the timeout is reached.
public synchronized void waitForClose(final long timeoutMillis)
throws Exception {
    if (!closed) {
        wait(timeoutMillis);
        if (!closed)
            throw new Exception("MockResponseSender could not be closed");
    }
}
```

What purpose does this comment serve? They serve no documentary purpose at all. We want to avoid this type of redundant comment, simply because it serves no purpose.

#### Misleading Comments

Sometimes, with all the best intentions, a programmer makes a statement in his comments that isn't precise enough to be accurate.

The method does not return _when_ `this.closed` becomes `true`. It returns _if_ `this.closed` is `true`; otherwise, it waits for a blind time-out and then throws an exception _if_ `this.closed` is still not `true`.

Misleading comments leads to long debugging session and sometimes frustrate developers.

#### Mandated Comments

It is just plain silly to have a rule that says that every function must have a javadoc, or every variable must have a comment.

```java
/**
 *
 * @param title The title of the CD
 * @param author The author of the CD
 * @param tracks The number of tracks on the CD
 * @param durationInMinutes The duration of the CD in minutes
 */
public void addCD(String title, String author,
    int tracks, int durationInMinutes) {
    CD cd = new CD();
    cd.title = title;
    cd.author = author;
    cd.tracks = tracks;
    cd.duration = duration;
    cdList.add(cd);
}
```

This clutter adds nothing and serves only to obfuscate the code and create the potential for lies and misdirection.

#### Journal Comments

Sometimes people add a comment to the start of a module every time they edit it. These comments accumulate as a kind of journal, or log, of every change that has ever been made.

```java
* Changes (from 11-Oct-2001)
    * --------------------------
    * 11-Oct-2001 : Re-organised the class and moved it to new package
    *               com.jrefinery.date (DG);
    * 05-Nov-2001 : Added a getDescription() method, and eliminated NotableDate
    *               class (DG);
    * 12-Nov-2001 : IBD requires setDescription() method, now that NotableDate
    *               class is gone (DG);  Changed getPreviousDayOfWeek(),
    *               getFollowingDayOfWeek() and getNearestDayOfWeek() to correct
    *               bugs (DG);
    * 05-Dec-2001 : Fixed bug in SpreadsheetDate class (DG);
    * 29-May-2002 : Moved the month constants into a separate interface
    *               (MonthConstants) (DG);
    * 27-Aug-2002 : Fixed bug in addMonths() method, thanks to N???levka Petr (DG);
    * 03-Oct-2002 : Fixed errors reported by Checkstyle (DG);
    * 13-Mar-2003 : Implemented Serializable (DG);
    * 29-May-2003 : Fixed bug in addMonths method (DG);
    * 04-Sep-2003 : Implemented Comparable.  Updated the isInRange javadocs (DG);
    * 05-Jan-2005 : Fixed bug in addYears() method (1096282) (DG);
```

Long ago, We didn't have source code version system that did it for us. Nowadays, however, these long journals are just more clutter to obfuscate the module.

#### Noise Comments

Sometimes you see comments that are nothing but noise. They restate the obvious and provide no new information.

```java
 /**
  * Default constructor.
  */
 protected AnnualDateRule() {}
```

another example could be

```java
// The day of the month.
private int dayOfMonth;
```

These comments are so noisy that we learn to ignore them. As we read through code, our eyes simply skip over them.

```java
private void startSending() {
    try {
        doSending();
    } catch (SocketException e) {
        // normal. someone stopped the request.
    } catch (Exception e) {
        try {
            response.add(ErrorResponder.makeExceptionString(e));
            response.closeAll();
        } catch (Exception e1) {
            //Give me a break!
        }
    }
}
```

The programmer should have recognized that his frustration could be resolved by improving the structure of his code. He should have redirected his energy to extracting that last `try`/`catch` block into a separate function such as:

```java
private void startSending() {
    try {
        doSending();
    } catch (SocketException e) {
        // normal. someone stopped the request.
    } catch (Exception e) {
        addExceptionAndCloseResponse(e);
    }
}

private void addExceptionAndCloseResponse(Exception e) {
    try {
        response.add(ErrorResponder.makeExceptionString(e));
        response.closeAll();
    } catch (Exception e1) {}
}
```

#### Scary Noise

Javadocs can also be noisy. What purpose do the following Javadocs (from a well-known open-source library) serve? Answer: nothing.

```java
/** The name. */
private String name;

/** The version. */
private String version;

/** The licenceName. */
private String licenceName;

/** The version. */
private String info;
```

If authors aren't paying attention when comments are written (or pasted), why should readers be expected to profit from them?

#### Don't Use a Comment When You Can Use a Function or a Variable

```java
// does the module from the global list <mod> depend on the
// subsystem we are part of?
if (smodule.getDependSubsystems().contains(subSysMod.getSubSystem()))
```

This could be rephrased without the comment as:

```java
ArrayList moduleDependees = smodule.getDependSubsystems();
String ourSubSystem = subSysMod.getSubSystem();
if (moduleDependees.contains(ourSubSystem))
```

The author of the original code may have written the comment first (unlikely) and then written the code to fulfill the comment. However, the author should then have refactored the code, as I did, so that the comment could be removed.

#### Position Markers

Sometimes programmers like to mark a particular position in a source file.

```java
// Actions //////////////////////////////////
```

There are rare times when it makes sense to gather certain functions together beneath a banner like this. But in general they are clutter that should be eliminated—especially the noisy train of slashes at the end.

#### Closing Brace Comments

Sometimes programmers will put special comments on closing braces.

```java
public class wc {
    public static void main(String[] args) {
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        String line;
        int lineCount = 0;
        int charCount = 0;
        int wordCount = 0;
        try {
            while ((line = in .readLine()) != null) {
                lineCount++;
                charCount += line.length();
                String words[] = line.split("\\W");
                wordCount += words.length;
            } //while
            System.out.println("wordCount = " + wordCount);
            System.out.println("lineCount = " + lineCount);
            System.out.println("charCount = " + charCount);
        } // try
        catch (IOException e) {
            System.err.println("Error:" + e.getMessage());
        } //catch
    } //main
}
```

If you find yourself wanting to mark your closing braces, try to shorten your functions instead.

#### Attributions and Bylines

```java
/* Added by Rick */
```

Source code control systems are very good at remembering who added what, when.

You might think that such comments would be useful in order to help others know who to talk to about the code. But the reality is that they tend to stay around for years and years, getting less and less accurate and relevant.

#### Commented-Out Code

```java
 InputStreamResponse response = new InputStreamResponse();
 response.setBody(formatter.getResultStream(), formatter.getByteCount());
 // InputStream resultsStream = formatter.getResultStream();
 // StreamReader reader = new StreamReader(resultsStream);
 // response.setContent(reader.read(formatter.getByteCount()));
```

Others who see that commented-out code won't have the courage to delete it. They'll think it is there for a reason and is too important to delete.

```java
this.bytePos = writeBytes(pngIdBytes, 0);
//hdrPos = bytePos;
writeHeader();
writeResolution();
//dataPos = bytePos;
if (writeImageData()) {
    writeEnd();
    this.pngBytes = resizeByteArray(this.pngBytes, this.maxPos);
} else {
    this.pngBytes = null;
}
return this.pngBytes;
```

Why are those two lines of code commented? Are they important, Were they left as reminder, or someone commented-out years ago and has simply not bothered to clean up.

#### HTML Comments

HTML in source code comments is hard to read while comments are mean to be easier to read.

```java
/**
 * Task to run fit tests.
 * This task runs fitnesse tests and publishes the results.
 * <p/>
 * <pre>
 * Usage:
 * &lt;taskdef name=&quot;execute-fitnesse-tests&quot;
 *     classname=&quot;fitnesse.ant.ExecuteFitnesseTestsTask&quot;
 *     classpathref=&quot;classpath&quot; /&gt;
 * OR
 * &lt;taskdef classpathref=&quot;classpath&quot;
 *             resource=&quot;tasks.properties&quot; /&gt;
 * <p/>
 * &lt;execute-fitnesse-tests
 *     suitepage=&quot;FitNesse.SuiteAcceptanceTests&quot;
 *     fitnesseport=&quot;8082&quot;
 *     resultsdir=&quot;${results.dir}&quot;
 *     resultshtmlpage=&quot;fit-results.html&quot;
 *     classpathref=&quot;classpath&quot; /&gt;
 * </pre>
 */
```

#### Nonlocal Information

If you must write a comment, then make sure it describes the code it appears near. Don't offer systemwide information in the context of a local comment.

```java
/**
 * Port on which fitnesse would run. Defaults to 8082.
 *
 * @param fitnessePort
 */
public void setFitnessePort(int fitnessePort) {
    this.fitnessePort = fitnessePort;
}
```

Aside from the fact that it is horribly redundant, it also offers information about the default port.

Of course there is no guarantee that this comment will be changed when the code containing the default is changed.

#### Too Much Information

Don't put interesting historical discussions or irrelevant descriptions of details into your comments.

```java
/*
	    RFC 2045 - Multipurpose Internet Mail Extensions (MIME)
	    Part One: Format of Internet Message Bodies
	    section 6.8.  Base64 Content-Transfer-Encoding
		The encoding process represents 24-bit groups of input bits as output strings of 4 encoded characters. Proceeding from left to right, a 24-bit input group is formed by concatenating 3 8-bit input groups. These 24 bits are then treated as 4 concatenated 6-bit groups, each of which is translated into a single digit in the base64 alphabet. When encoding a bit stream via the base64 encoding, the bit stream must be presumed to be ordered with the most-significant-bit first. That is, the first bit in the stream will be the high-order bit in the first 8-bit byte, and the eighth bit will be the low-order bit in the first 8-bit byte, and so on.
 */
```

#### Inobvious Connection

The connection between a comment and the code it describes should be obvious. Readers should be able to understand the comments.

```java
/*
 * start with an array that is big enough to hold all the pixels
 * (plus filter bytes), and an extra 200 bytes for header info
 */
this.pngBytes = new byte[((this.width + 1) * this.height * 3) + 200];
```

What is a filter byte? Does it relate to the +1? Or to the x3? Both? Is a pixel a byte? Why 200?

#### Function Headers

Short functions don't need much description. A well-chosen name for a small function that does one thing is usually better than a comment header.

#### Javadocs in Nonpublic Code

As useful as javadocs are for public APIs, they are anathema to code that is not intended for public consumption. Generating javadoc pages for the classes and functions inside a system is not generally useful, and the extra formality of the javadoc comments amounts to little more than cruft and distraction.

## 5. Formatting

When people look under the hood, we want them to be impressed with the neatness, consistency, and attention to detail that they perceive.

### The Purpose of Formatting

First of all, let's be clear. Code formatting is _important_. It is too important to ignore and it is too important to treat religiously.

The functionality that you create today has a good chance of changing in the next release, but the readability of your code will have a profound effect on all the changes that will ever be made.

What are the formatting issues that help us to communicate best?

### Vertical Formatting

Let's start with vertical size. How big should a source file be? In Java, file size is closely related to class size.

![vertical-formatting](https://github.com/user-attachments/assets/4a2e0821-8070-4b7f-85ab-f7b25512c8c8)

The lines through the boxes show the minimum and maximum file lengths in each project. The box shows approximately one-third (one standard deviation) of the files. The middle of the box is the mean. So the average file size in the FitNesse project is about 65 lines, and about one-third of the files are between 40 and 100+ lines.

The largest file in FitNesse is about 400 lines and the smallest is 6 lines.

Junit, FitNesse, and Time and Money are composed of relatively small files. None are over 500 lines and most of those files are less than 200 lines. Tomcat and Ant, on the other hand, have some files that are several thousand lines long and close to half are over 200 lines.

What does that mean to us? It appears to be possible to build significant systems (FitNesse is close to 50,000 lines) out of files that are typically 200 lines long, with an upper limit of 500.

it should be considered very desirable. Small files are usually easier to understand than large files are.

#### The Newspaper Metaphor

Think of a well-written newspaper article. You read it vertically. At the top you expect a headline that will tell you what the story is about and allows you to decide whether it is something you want to read. Heading just reveal the context of the story, and as you go downwards you get more details about the story.

We would like a source file to be like a newspaper article. The name should be simple but explanatory. The name, by itself, should be sufficient to tell us whether we are in the right module or not.

#### Vertical Openness Between Concepts

Nearly all code is read left to right and top to bottom. Each line represents an expression or a clause, and each group of lines represents a complete thought.

```java
package fitnesse.wikitext.widgets;

import java.util.regex.*;

public class BoldWidget extends ParentWidget {
    public static final String REGEXP = "'''. + ? '''";
    private static final Pattern pattern = Pattern.compile("'''(. + ? )'''",
        Pattern.MULTILINE + Pattern.DOTALL
    );

    public BoldWidget(ParentWidget parent, String text) throws Exception {
        super(parent);
        Matcher match = pattern.matcher(text);
        match.find();
        addChildWidgets(match.group(1));
    }

    public String render() throws Exception {
        StringBuffer html = new StringBuffer(" < b > ");
        html.append(childHtml()).append(" < /b>");
            return html.toString();
    }
}
```

Consider this example, There are blank lines that separate the package declaration, the import(s), and each of the functions. This extremely simple rule has a profound effect on the visual layout of the code.

Taking those blank lines out, this has a remarkably obscuring effect on the readability of the code.

```java
package fitnesse.wikitext.widgets;
import java.util.regex.*;
public class BoldWidget extends ParentWidget {
    public static final String REGEXP = "'''. + ? '''";
    private static final Pattern pattern = Pattern.compile("'''(. + ? )'''",
        Pattern.MULTILINE + Pattern.DOTALL);
    public BoldWidget(ParentWidget parent, String text) throws Exception {
        super(parent);
        Matcher match = pattern.matcher(text);
        match.find();
        addChildWidgets(match.group(1));
    }
    public String render() throws Exception {
        StringBuffer html = new StringBuffer(" < b > ");
        html.append(childHtml()).append(" < /b>");
            return html.toString();
    }
}
```

This effect is even more pronounced when you unfocus your eyes. In the first example the different groupings of lines pop out at you, whereas the second example looks like a muddle.

#### Vertical Density

If openness separates concepts, then vertical density implies close association, If lines are together we think it's related and mean to be kept together.

```java
public class ReporterConfig {

    /**
     * The class name of the reporter listener
     */
    private String m_className;

    /**
     * The properties of the reporter listener
     */
    private List < Property > m_properties = new ArrayList < Property > ();

    public void addProperty(Property property) {
        m_properties.add(property);
    }
}
```

Below code is much easier to read, It fits in an "eye-full". While above code requires some time to realize that it has 2 variables and a method.

```java
public class ReporterConfig {
    private String m_className;
    private List < Property > m_properties = new ArrayList < Property > ();

    public void addProperty(Property property) {
        m_properties.add(property);
    }
}
```

#### Vertical Distance

It's common that we have to go through classes and functions in different files, scrolling up and down to understand what the code is doing. It's frustrating because you're trying to understand what they system does, but you're spending your time and mental energy on trying to locate and remember where the pieces are.

Concepts that are closely related should be kept vertically close to each other. Clearly this rule doesn't work for concepts that belong in separate files. But then closely related concepts should not be separated into different files unless you have a very good reason.

We want to avoid out readers to hop around our source file to understand what it does.

**Variable Declarations.** Variables should be declared as close to their usage as possible. Because our functions are very short, local variables should appear at the top of each function

```java
private static void readPreferences() {
    InputStream is = null;
    try {
        is = new FileInputStream(getPreferencesFile());
        setPreferences(new Properties(getPreferences()));
        getPreferences().load(is);
    } catch (IOException e) {
        try {
            if (is != null)
                is.close();
        } catch (IOException e1) {}
    }
}
```

Control variables for loops should usually be declared within the loop statement, as in this cute little function from the same source.

```java
public int countTestCases() {
    int count = 0;
    for (Test each: tests)
        count += each.countTestCases();
    return count;
}
```

In rare cases a variable might be declared at the top of a block or just before a loop in a long-ish function. You can see such a variable in this snippet from the midst of a very long function in TestNG.

```java
for (XmlTest test: m_suite.getTests()) {
    TestRunner tr = m_runnerFactory.newTestRunner(this, test); // here
    tr.addListener(m_textReporter);
    m_testRunners.add(tr);

    invoker = tr.getInvoker();

    for (ITestNGMethod m: tr.getBeforeSuiteMethods()) {
        beforeSuiteMethods.put(m.getMethod(), m);
    }

    for (ITestNGMethod m: tr.getAfterSuiteMethods()) {
        afterSuiteMethods.put(m.getMethod(), m);
    }
}
```

**Instance variables,** on the other hand, should be declared at the top of the class. This should not increase the vertical distance of these variables, because in a well-designed class, they are used by many, if not all, of the methods of the class.

Consider, for example the strange case of the `TestSuite` class in JUnit 4.3.1. Someone reading this code would have to stumble across the declarations by accident.

```java
public class TestSuite implements Test {
    static public Test createTest(Class << ? extends TestCase > theClass,
        String name) {…}

    public static Constructor << ? extends TestCase >
        getTestConstructor(Class << ? extends TestCase > theClass)
    throws NoSuchMethodException {…}

    public static Test warning(final String message) {…}

    private static String exceptionToString(Throwable t) {…}

    private String fName;

    private Vector < Test > fTests = new Vector < Test > (10);

    public TestSuite() {}

    public TestSuite(final Class << ? extends TestCase > theClass) {…}

    public TestSuite(Class << ? extends TestCase > theClass, String name) {…}
}
```

**Dependent Functions.** If one function calls another, they should be vertically close, and the caller should be above the callee, if at all possible.

the snippet from FitNesse below. Notice how the topmost function calls those below it and how they in turn call those below them. This makes it easy to find the called functions and greatly enhances the readability of the whole module.

```java
public class WikiPageResponder implements SecureResponder {
    protected WikiPage page;
    protected PageData pageData;
    protected String pageTitle;
    protected Request request;
    protected PageCrawler crawler;

    public Response makeResponse(FitNesseContext context, Request request)
    throws Exception {
        String pageName = getPageNameOrDefault(request, "FrontPage");
        loadPage(pageName, context);
        if (page == null)
            return notFoundResponse(context, request);
        else
            return makePageResponse(context);
    }

    private String getPageNameOrDefault(Request request, String defaultPageName) {
        String pageName = request.getResource();
        if (StringUtil.isBlank(pageName))
            pageName = defaultPageName;

        return pageName;
    }

    protected void loadPage(String resource, FitNesseContext context)
    throws Exception {
        WikiPagePath path = PathParser.parse(resource);
        crawler = context.root.getPageCrawler();
        crawler.setDeadEndStrategy(new VirtualEnabledPageCrawler());
        page = crawler.getPage(context.root, path);
        if (page != null)
            pageData = page.getData();
    }

    private Response notFoundResponse(FitNesseContext context, Request request)
    throws Exception {
        return new NotFoundResponder().makeResponse(context, request);
    }

    private SimpleResponse makePageResponse(FitNesseContext context)
    throws Exception {
        pageTitle = PathParser.render(crawler.getFullPath(page));
        String html = makeHtml(context);

        SimpleResponse response = new SimpleResponse();
        response.setMaxAge(0);
        response.setContent(html);
        return response;
    }
}
```

The "`FrontPage`" constant could have been buried in the `getPageNameOrDefault` function, but that would have hidden a well-known and expected constant in an inappropriately low-level function. It was better to pass that constant down from the place where it makes sense to know it to the place that actually uses it.

**Conceptual Affinity.** Certain bits of code _want_ to be near other bits. They have a certain conceptual affinity. Consider this example from Junit 4.3.1.

```java
public class Assert {
    static public void assertTrue(String message, boolean condition) {
        if (!condition)
            fail(message);
    }

    static public void assertTrue(boolean condition) {
        assertTrue(null, condition);
    }

    static public void assertFalse(String message, boolean condition) {
        assertTrue(message, !condition);
    }

    static public void assertFalse(boolean condition) {
        assertFalse(null, condition);
    }
}
```

These functions have a strong conceptual affinity because they share a common naming scheme and perform variations of the same basic task.

#### Vertical Ordering

In general, we want function call ordering, the function should be below the caller function. it helps to build nice flow down the source code.

This is exact opposite of language like Pascal, C and C++, In newspaper, we want important concepts to come first and we expect them to be expressed with the least amount of polluting detail. We except the low-level details to come last.

### Horizontal Formatting

How wide should a line be? To answer that, let's look at how wide lines are in typical programs.
![horizontal-formatting](https://github.com/user-attachments/assets/59d22158-e907-46df-b636-6b096039253c)

The regularity is impressive, especially right around 45 characters. Indeed, every size from 20 to 60 represents about 1 percent of the total number of lines. That's 40 percent! Perhaps another 30 percent are less than 10 characters wide. Remember this is a log scale, so the linear appearance of the drop-off above 80 characters is really very significant. Programmers clearly prefer short lines.

This suggests that we should strive to keep our lines short. Author used to keep line as short as readers don't have to scroll right.

#### Horizontal Openness and Density

We use horizontal white space to associate things that are strongly related and disassociate things that are more weakly related.

```java
private void measureLine(String line) {
    lineCount++;
    int lineSize = line.length();
    totalChars += lineSize;
    lineWidthHistogram.addLine(lineSize, lineCount);
    recordWidestLine(lineSize);
}
```

It is surrounded the assignment operators with white space to show separation obvious.

Another example of spaces could be:

```java
public class Quadratic {
    public static double root1(double a, double b, double c) {
        double determinant = determinant(a, b, c);
        return (-b + Math.sqrt(determinant)) / (2*a);
    }

    public static double root2(int a, int b, int c) {
        double determinant = determinant(a, b, c);
        return (-b - Math.sqrt(determinant)) / (2*a);
    }

    private static double determinant(double a, double b, double c) {
        return b*b - 4*a*c;
    }
}
```

Notice how nicely the equations read. The factors have no white space between them because they are high precedence. The terms are separated by white space because addition and subtraction are lower precedence.

#### Horizontal Alignment

```java
public class FitNesseExpediter implements ResponseSender {
    private   Socket           socket;
    private   InputStream     input;
    private   OutputStream     output;
    private   Request         request;
    private   Response         response;
    private   FitNesseContext context;
    protected long            requestParsingTimeLimit;
    private   long            requestProgress;
    private   long            requestParsingDeadline;
    private   boolean          hasError;

    public FitNesseExpediter(Socket s, FitNesseContext context) throws Exception {
	    this.context =            context;
	    socket =                  s;
	    input =                   s.getInputStream();
	    output =                  s.getOutputStream();
	    requestParsingTimeLimit = 10000;
    }
}
```

This kind of alignment is not useful the alignment seems to emphasize the wrong things and leads eye away from the true intent.

If we want to align lists that is long, _the problem is the length of the lists_ not the lack of alignment. above example can be done better:

```java
public class FitNesseExpediter implements ResponseSender {
    private Socket socket;
    private InputStream input;
    private OutputStream output;
    private Request request;

    private Response response;
    private FitNesseContext context;
    protected long requestParsingTimeLimit;
    private long requestProgress;
    private long requestParsingDeadline;
    private boolean hasError;

    public FitNesseExpediter(Socket s, FitNesseContext context) throws Exception {
        this.context = context;
        socket = s;
        input = s.getInputStream();
        output = s.getOutputStream();
        requestParsingTimeLimit = 10000;
    }
}
```

#### Indentation

A source file is organized in a structure similar to an outline, with different layers of information. It starts with details relevant to the whole file, then narrows down to individual classes, methods within those classes, and blocks within the methods. Each of these layers represents a distinct scope where names and statements are defined and interpreted.

To make this hierarchy of scopes visible, we indent the lines of source code in proportion to their position in the hierarchy.

Programmers rely heavily on this indentation scheme. They visually line up lines on the left to see what scope they appear in.

Consider the following programs that are syntactically and semantically identical:

```java
public class FitNesseServer implements SocketServer { private FitNesseContext
   context; public FitNesseServer(FitNesseContext context) { this.context =
   context; } public void serve(Socket s) { serve(s, 10000); } public void
   serve(Socket s, long requestTimeout) { try { FitNesseExpediter sender = new
   FitNesseExpediter(s, context);
   sender.setRequestParsingTimeLimit(requestTimeout); sender.start(); }
   catch(Exception e) { e.printStackTrace(); } } }

   -----


   public class FitNesseServer implements SocketServer {
     private FitNesseContext context;
     public FitNesseServer(FitNesseContext context) {
       this.context = context;
     }

     public void serve(Socket s) {
       serve(s, 10000);
     }

     public void serve(Socket s, long requestTimeout) {
       try {
         FitNesseExpediter sender = new FitNesseExpediter(s, context);
         sender.setRequestParsingTimeLimit(requestTimeout);
         sender.start();
       }
       catch (Exception e) {
         e.printStackTrace();
       }
    }
}
```

Your eye can rapidly discern the structure of the indented file. You can almost instantly spot the variables, constructors, accessors, and methods. It takes just a few seconds to realize that this is some kind of simple front end to a socket, with a time-out.

**Breaking Indentation.** It is sometimes tempting to break the indentation rule for short `if` statements, short `while` loops, or short functions.

```java
public class CommentWidget extends TextWidget
{
    public static final String REGEXP = "^#[^\r\n]*(?:(?:\r\n)|\n|\r)?";

    public CommentWidget(ParentWidget parent, String text){super(parent, text);}
    public String render() throws Exception {return ""; }
}
```

Author prefers to expand and indent the scopes instead, like this:

```java
public class CommentWidget extends TextWidget {
    public static final String REGEXP = " ^ #[ ^ \r\ n] * ( ? : ( ? : \r\ n) | \n | \r) ? ";

    public CommentWidget(ParentWidget parent, String text) {
        super(parent, text);
    }

    public String render() throws Exception {
        return"";
    }
}
```

#### Dummy Scopes

Sometimes the body of a `while` or `for` statement is a dummy, as shown below.

```java
while (dis.read(buf, 0, readBufferSize) != -1)
	;
```

When this type of dummy body is not avoided, we should make sure that it's properly indented and surrounded by braces.

### Team Rules

The title of this section is a play on words. Every programmer has his own favorite formatting rules, but if he works in a team, then the team rules.

A team of developers should agree upon a single formatting style, and then every member of that team should use that style. We want the software to have a consistent style.

When author started FitNesse project back in 2002, he set down with the team to work out a coding style, it took around 10 minutes to decide how they will name a classes, methods and variables, what would be indent size, etc.

Remember, a good software system is composed of a set of documents that read nicely. They need to have a consistent and smooth style.

## 6. Objects and Data Structures

There is a reason that we keep our variables private. We don't want anyone else to depend on them.

### Data Abstraction

Consider these code snippets, both represent the data of a point on the Cartesian plan. And yet one exposes its implementation and other completely hides it.

```java
public class Point {
    public double x;
    public double y;
}
```

```java
public interface Point {
    double getX();
    double getY();
    void setCartesian(double x, double y);
    double getR();
    double getTheta();
    void setPolar(double r, double theta);
}
```

In above code snippet, It represents more than just a data structure. The methods enforce an access policy. You can read the individual coordinates independently, but you must set the coordinates together as an atomic operation.

On the other hand (first code snippet), is very clearly implemented in rectangular coordinates, and it forces us to manipulate those coordinates independently. This exposes implementation. Indeed, it would expose implementation even if the variables were private and we were using single variable getters and setters.

Hiding implementation is about abstractions! A class does not simply push its variables out through getters and setters. Rather it exposes abstract interfaces that allow its users to manipulate the _essence_ of the data, without having to know its implementation.

Consider these snippets, First code snippet uses concrete terms to communication hence clearly reflect accessors of variables, while second code snippet uses abstraction hence you have no clue at all about the form of the data.

```java
public interface Vehicle {
	double getFuelTankCapacityInGallons();
	double getGallonsOfGasoline();
}
```

```java
public interface Vehical {
	double getPercentFuelRemaining();
}
```

In both of above cases the second option is preferable. We don't want to expose the details of our data. Rather we want to expose our data in abstracted form.

### Data/Object Anti-Symmetry

Objects hide their data behind abstractions and expose functions that operate on that data. Data structure expose their data and have no meaningful functions.

Consider this example, `Geometry` classes contain the behavior and Shape classes is just data structure without behavior.

```java
public class Square {
    public Point topLeft;
    public double side;
}

public class Rectangle {
    public Point topLeft;
    public double height;
    public double width;
}

public class Circle {
    public Point center;
    public double radius;
}

public class Geometry {
    public final double PI = 3.141592653589793;

    public double area(Object shape) throws NoSuchShapeException {
        if (shape instanceof Square) {
            Square s = (Square) shape;
            return s.side * s.side;
        } else if (shape instanceof Rectangle) {
            Rectangle r = (Rectangle) shape;
            return r.height * r.width;
        } else if (shape instanceof Circle) {
            Circle c = (Circle) shape;
            return PI * c.radius * c.radius;
        }
        throw new NoSuchShapeException();
    }
}
```

Consider what would happen if a `perimeter()` function were added to `Geometry`. The shape classes would be unaffected! Any other classes that depended upon the shapes would also be unaffected! On the other hand, if we add a new shape, We must change all the functions in `Geometry` to deal with it.

Consider this object-oriented solution, where the `area()` method is polymorphic. No `Geometry` class is necessary.So if I add a new shape, none of the existing _functions_ are affected, but if I add a new function all of the _shapes_ must be changed!

```java
public class Square implements Shape {
    private Point topLeft;
    private double side;

    public double area() {
        return side * side;
    }
}

public class Rectangle implements Shape {
    private Point topLeft;
    private double height;
    private double width;

    public double area() {
        return height * width;
    }
}

public class Circle implements Shape {
    private Point center;
    private double radius;
    public final double PI = 3.141592653589793;

    public double area() {
        return PI * radius * radius;
    }
}
```

This exposes the fundamental difference between objects and data structures:

_Procedural code (code using data structures) makes it easy to add new functions without changing the existing data structures. OO code, on the other hand, makes it easy to add new classes without changing existing functions._

The complement is also true:

_Procedural code makes it hard to add new data structures because all the functions must change. OO code makes it hard to add new functions because all the classes must change._

In any complex system there are going to be times where

- If we want to add new data types rather than new functions (New Shape) - Objects and OO are most appropriate
- If we wants to add new functions as opposed to data types (New Method) - Procedural Code and data structures will be more appropriate.

### The Law of Demeter

There is a well-known heuristic called the _Law of Demeter_2 that says a module should not know about the innards of the \_objects_ it manipulates.

Objects should not expose its internal structure through accessors.

In simpler terms, think of it like this: when you ask a friend for something, you should only speak to your friend directly and not to your friend's acquaintances. If your friend has to get something from someone else, let your friend do it and give you the result, instead of you reaching out to the third person.

Consider this example that violate the Law of Demeter:

```java
final String outputDir = ctxt.getOptions().getScratchDir().getAbsolutePath();
```

Here is why?

- `ctxt` is calling `getOptions()`, which gives you an object.
- Then, on that returned object, `getScratchDir()` is called.
- Finally, `getAbsolutePath()` is called on the result of `getScratchDir()`.

Another example could be:

```java
Expenses expenses = new Expenses(100, 10);
Employee employee = new Employee();
employee.getDepartment().getManager().approveExpense(expenses);
```

#### Train Wrecks

This kind of code is often called a _train wreck_ because it look like a bunch of coupled train cars. It is usually best to split them up:

```java
Options opts = ctxt.getOptions();
File scratchDir = opts.getScratchDir();
final String outputDir = scratchDir.getAbsolutePath();
```

Whether this is a violation of Demeter depends on whether or not `ctxt, Options`, and `ScratchDir` are objects or data structures.

- If they are objects then their internal structure should be hidden rather than exposed.
- If they are data structures with no behavior, then they naturally expose their internal structure, and so Demeter does not apply.

We won't think about Demeter if code was:

```java
final String outputDir = ctxt.options.scratchDir.absolutePath;
```

#### Hybrids

This confusion sometimes leads to unfortunate hybrid structures that are half object and half data structure.

Hybrids make it hard to add new functions but also make it hard to add new data structures.

#### Hiding Structure

What if `ctxt, options`, and `scratchDir` are objects with real behavior? Consider these code snippets:

```java
ctxt.getAbsolutePathOfScratchDirectoryOption();
```

```java
ctx.getScratchDirectoryOption().getAbsolutePath();
```

The first option could lead to an explosion of methods in the `ctxt` object. The second presumes that `getScratchDirectoryOption()` returns a data structure, not an object. Neither option is good.

If `ctxt` is an object, we should not ask for it's internal implementation. Consider this code snippet:

```java
String outFile = outputDir + "/" + className.replace(".", "/") + ".class";
FileOutputStream fout = new FileOutputStream(outFile);
BufferedOutputStream bos = new BufferedOutputStream(fout);
```

Ignoring dots and file extension, intent of this code to create a scratch file at absolute path.

We should better call it as:

```java
BufferedOutputStream bos = ctxt.createScratchFileStream(classFileName);
```

That seems like a reasonable thing for an object to do! This allows `ctxt` to hide its internals and prevents the current function from having to violate the Law of Demeter by navigating through objects it shouldn't know about.

### Data Transfer Objects

The data structure class, with public variables and no functions. This is sometimes called a data transfer object or DTO.

They are useful and comes handy when converting raw data in a database into objects in the application code.

```java
public class Address {
    private String street;
    private String streetExtra;
    private String city;
    private String state;
    private String zip;

    public Address(String street, String streetExtra,
        String city, String state, String zip) {
        this.street = street;
        this.streetExtra = streetExtra;
        this.city = city;
        this.state = state;
        this.zip = zip;
    }

    public String getStreet() {
        return street;
    }

    public String getStreetExtra() {
        return streetExtra;
    }

    public String getCity() {
        return city;
    }

    public String getState() {
        return state;
    }

    public String getZip() {
        return zip;
    }
}
```

#### Active Record

Active Records are special forms of DTOs. They are data structures with public variables. Typically these Active Records are direct translations from database tables, or other data sources.

It contains the methods such as `save`, `find` etc. but including business logic into Active Records is bad idea and leads to hybrid structure.

We should treat the Active Record as a data structure and to create separate objects that contain the business rules and that hide their internal data.

## 7. Error Handling

Error handling is important, _but if it obscures logic, it's wrong_.

### Use Exceptions Rather Than Return Codes

Back in the past, some languages doesn't have exceptions. We used to return error code or set an error flag at that time. Here is how:

```java
public class DeviceController {
    // …
    public void sendShutDown() {
        DeviceHandle handle = getHandle(DEV1);
        // Check the state of the device
        if (handle != DeviceHandle.INVALID) {
            // Save the device status to the record field
            retrieveDeviceRecord(handle);
            // If not suspended, shut down
            if (record.getStatus() != DEVICE_SUSPENDED) {
                pauseDevice(handle);
                clearDeviceWorkQueue(handle);
                closeDevice(handle);
            } else {
                logger.log("Device suspended.  Unable to shut down");
            }
        } else {
            logger.log("Invalid handle for: " + DEV1.toString());
        }
    }
    // …
}
```

The problem with these approaches is that they clutter the caller. The caller must check for errors immediately after the call.

To solve this problem it's better throw an exception when you encounter an error. Here is how:

```java
public class DeviceController {
    // …

    public void sendShutDown() {
        try {
            tryToShutDown();
        } catch (DeviceShutDownError e) {
            logger.log(e);
        }
    }

    private void tryToShutDown() throws DeviceShutDownError {
        DeviceHandle handle = getHandle(DEV1);
        DeviceRecord record = retrieveDeviceRecord(handle);

        pauseDevice(handle);
        clearDeviceWorkQueue(handle);
        closeDevice(handle);
    }

    private DeviceHandle getHandle(DeviceID id) {
        // …
        throw new DeviceShutDownError("Invalid handle
            for: "+id.toString());
        // …
    }

    //     …
}
```

In this code, the algorithm for device shutdown and error handling, are now separated.

### Write Your `Try-Catch-Finally` Statement First

One of the most interesting things about exceptions is that they _define a scope_ within your program. When you use `Try-Catch-Finally` you can start execution and abort at any point and then resume at the `catch`.

In a way, `try` blocks are like transactions, Your `catch` has to leave your program in a consistent state, no matter what happens in the `try`.

Let's look at an example. We need to write some code that accesses a file and reads some serialized objects.

We start with a unit test that shows that we'll get an exception when the file doesn't exist:

```java
@Test(expected = StorageException.class)
public void retrieveSectionShouldThrowOnInvalidFileName() {
    sectionStore.retrieveSection("invalid - file");
}
```

The test drives us to create this stub:

```java
public List<RecordedGrip> retrieveSection(String sectionName) {
    // dummy return until we have a real implementation
    return new ArrayList<RecordedGrip>();
}
```

Out test will fail, because it doesn't throw an exception. Now, we modify our code to access invalid file and throw exceptions:

```java
public List<RecordedGrip> retrieveSection(String sectionName) {
    try {
        FileInputStream stream = new FileInputStream(sectionName)
    } catch (Exception e) {
        throw new StorageException("retrieval error", e);
    }
    return new ArrayList<RecordedGrip>();
}
```

Now, our test will pass, and we can refactor. We can use specific exception instead of `Exception`.

```java
public List<RecordedGrip> retrieveSection(String sectionName) {
    try {
        FileInputStream stream = new FileInputStream(sectionName);
        stream.close();
    } catch (FileNotFoundException e) {
        throw new StorageException("retrieval error", e);
    }
    return new ArrayList<RecordedGrip> ();
}
```

Now, we can add logic in this code with following TDD. Our test should force us to have exceptions.

### Use Unchecked Exceptions

When Java introduced checked exception, It seemed like a great idea and beneficial. Turns out it wasn't. Now, It is clean that they aren't necessary for the production of robust software.

C#, C++, Python and even Ruby doesn't have checked exceptions. Still it is possible to write robust software in all mentioned languages.

Checked Exception is a Open/Close Principle violation. If you throw a checked exception from a method in your code and the `catch` is three level above, _you must declare that exception in the signature of each method between you and the `catch`_.

Consider the calling hierarchy of a large system. Function at the top call functions below them, which call more functions below them and so on.

Suppose, bottom most function modified that in a way that throw exception. We need to replicate the changes to all above functions with `throws` clause to its signature and so on.

Encapsulation is broken because all functions in the path of a throw must know about details of that low-level exception.

Checked exceptions can sometimes be useful if you are writing a critical library: You must catch them. But in general application development the dependency costs outweigh the benefits.

### Provide Context with Exceptions

Each exception that you throw should provide enough context to determine the source and location of an error. It can help in the stack trace but won't tell you the intent of the operation that failed.

Create informative message and pass them along with your exception. Mention the operation and type of failure and add the same in logging if you're using.

### Define Exception Classes in Terms of a Caller's Needs

There are many ways to classify errors. We can classify with their source (Did they come from one component or another) or their type (network failure, programming error etc.).

Example of poor exception classification:

```java
ACMEPort port = new ACMEPort(12);

try {
    port.open();
} catch (DeviceResponseException e) {
    reportPortError(e);
    logger.log("Device response exception", e);
} catch (ATM1212UnlockedException e) {
    reportPortError(e);
    logger.log("Unlock exception", e);
} catch (GMXError e) {
    reportPortError(e);
    logger.log("Device response exception");
} finally {…}
```

That statement contains a lot of duplication. The main idea is We have to record an error and make sure that we can proceed.

we can simplify our code considerably by wrapping the API that we are calling and making sure that it returns a common exception type:

```java
LocalPort port = new LocalPort(12);
try {
    port.open();
} catch (PortDeviceFailure e) {
    reportError(e);
    logger.log(e.getMessage(), e);
} finally {…}
```

Our `LocalPort` class is just a simple wrapper that catches and translates exceptions thrown by the `ACMEPort` class:

```java
public class LocalPort {
    private ACMEPort innerPort;

    public LocalPort(int portNumber) {
        innerPort = new ACMEPort(portNumber);
    }

    public void open() {
        try {
            innerPort.open();
        } catch (DeviceResponseException e) {
            throw new PortDeviceFailure(e);
        } catch (ATM1212UnlockedException e) {
            throw new PortDeviceFailure(e);
        } catch (GMXError e) {
            throw new PortDeviceFailure(e);
        }
    }
    //…
}
```

Wrappers like the one we defined for `ACMEPort` can be very useful. In fact, wrapping third-party APIs is a best practice. It helps to minimize your dependencies upon it, easier to mock out third-party calls in testing.

One final advantage of wrapping is that you aren't tied to a particular vendor's API design choices.

### Define the Normal Flow

If we keep separation between error handling and actual business login or algorithm, It helps to maintain clean code.

You wrap external APIs so that you can throw your own exceptions. and you define a handler above your code so that you can deal with any aborted computation. Most of the time this is a great approach, but there are some times when you may not want to abort.

Let's take a look at an example. Here is some awkward code that sums expenses in a billing application:

```java
try {
    MealExpenses expenses = expenseReportDAO.getMeals(employee.getID());
    m_total += expenses.getTotal();
} catch (MealExpensesNotFound e) {
    m_total += getMealPerDiem();
}
```

In this business, if mean are expensed, they become part of the total. If they aren't, the employee gets a meal _per diem_ amount for that day. The exception clutters the logic.

We can change the `ExpenseReportDAO` so that it always returns a `MealExpense` object. If there are no meal expenses, it returns a `MealExpense` object that returns the _per diem_ as its total:

```java
public class PerDiemMealExpenses implements MealExpenses {
	public int getTotal() {
		// return the per diem default
	}
}
```

You create a class or configure an object so that it handles a special case for you.

### Don't Return Null

We're more likely returning `null` in any such cases where we're blank, and we keep checking condition with `null` Here is the example:

```java
public void registerItem(Item item) {
    if (item != null) {
        ItemRegistry registry = peristentStore.getItemRegistry();
        if (registry != null) {
            Item existing = registry.getItem(item.getID());
            if (existing.getBillingPeriod().hasRetailOwner()) {
                existing.register(item);
            }
        }
    }
}
```

Whenever we're returning null, we're creating problems for our callers. All it takes is one missing `null` check to send an application spinning out of control. (CrowdStrike bug recently).

In above code what if `persistentStore` is null, We would have `NullPointerException` at runtime. We could have easily solved problem by adding a null check, but the problem is there are too many.

You're tempted to return `null` from a method, consider throwing exception rather.

Another example:

```java
List < Employee > employees = getEmployees();
if (employees != null) {
    for (Employee e: employees) {
        totalPay += e.getPay();
    }
}
```

`getEmployees()` can return null, but we can change it to return empty list instead of null.

```java
public List < Employee > getEmployees() {
    if (..there are no employees..) {
        return Collections.emptyList();
	}
}
```

Now, you minimized the chance of `NullpointerExceptions` and your code will be cleaner.

### Don't Pass Null

Returning `null` from methods is bad, but passing `null` into methods is worse.

```java
public class MetricsCalculator {
    public double xProjection(Point p1, Point p2) {
		return (p2.x - p1.x) * 1.5;
    }
}
```

What happens when someone passes `null` as an argument?

```java
calculator.xProjection(null, new Point(12, 13));
```

We'll get a `NullPointerException`, of course. How can we fix it?

```java
public class MetricsCalculator {
    public double xProjection(Point p1, Point p2) {
        if (p1 == null || p2 == null) {
            throw InvalidArgumentException("Invalid argument
                for MetricsCalculator.xProjection");
        }
        return (p2.x - p1.x) * 1.5;
    }
}
```

It might be little better than `Null` pointer exception. but remember, we have to define a handler for `InvalidArgumentException`.

Here is another alternative:

```java
public class MetricsCalculator {
    public double xProjection(Point p1, Point p2) {
        assert p1 != null: "p1 should not be null";
        assert p2 != null: "p2 should not be null";
        return (p2.x - p1.x) * 1.5;
    }
}
```

It's good documentation, but it doesn't solve the problem. If someone passes `null`, we'll still have a runtime error.

In most programming languages there is no good way to deal with a `null` that is passed by a caller accidentally.

## 8. Boundaries

We seldom control all the software in our system. Sometimes we buy third-party packages or use open source or depends on internal team.

### Using Third-Party Code

There is a natural tension between provider of an interface and user of an interface. Provider focuses on multiple environment so that all users can satisfied, on the other hand, one wants an interface for their specific need.

Consider the example of `java.util.Map`, Assume that We want to build up a `Map` and pass it around, Out intention might be that none of the recipients of our `Map` delete anything in the map. But `java.util.Map` has method `clear()`. Any User of the `Map` has the power to clear it.

Consider this example

```java
Map sensors = new HashMap();
```

Then when some other part of the code needs to access the sensor, you see this code:

```java
Sensor s = (Sensor)sensors.get(sensorId);
```

The client of this code carries the responsibility of getting an `Object` from the `Map` and casting it to the right type.

The readability of this code can be greatly improved by using generics:

```java
Map<Sensor> sensors = new HashMap<Sensor>();

Sensor s = sensors.get(sensorId);
```

A cleaner way to use `Map` might look like following. No user of Sensors would care one bit if generics were used or not.

```java
public class Sensors {
    private Map sensors = new HashMap();

    public Sensor getById(String id) {
        return (Sensor) sensors.get(id);
    }
}
```

Now, it doesn't required to change everywhere sensors is used. We are not suggesting that you not to pass `Map`s around your system. If you use a boundary interface like `Map`, keep it inside the class, or close family of classes, Where it is used.

### Exploring and Learning Boundaries

Third-party code helps us get more functionality delivered in less time. It's not our job to test third-party code but it's best interest to write tests for the third-party code we use.

It takes time to understand and might cause long debugging session. Learning the third-party code is hard. Integrating the third-party code is hard too. Doing both at the same time is doubly-hard.

In learning tests we call the third-party API, as we expect to use it in our application. We're essentially doing controlled experiments that check our understanding of that API. The tests focus on what we want out of the API.

### Learning `log4j`

Consider we want to use `log4j`, we download it and open introductory documentation page.

Without thinking much we write our first test case, expecting it to write
"Hello World" to the console:

```java
@Test
public void testLogCreate() {
    Logger logger = Logger.getLogger("MyLogger");
    logger.info("hello");
}
```

It gives error that tells us we need something called an `Appender`. Form Docs we find `ConsoleAppender`:

```java
@Test
public void testLogAddAppender() {
    Logger logger = Logger.getLogger("MyLogger");
    ConsoleAppender appender = new ConsoleAppender();
    logger.addAppender(appender);
    logger.info("hello");
}
```

This time we find that the `Appender` has no output stream. We might google the solution and come up with following:

```java
@Test
public void testLogAddAppender() {
    Logger logger = Logger.getLogger("MyLogger");
    logger.removeAllAppenders();
    logger.addAppender(new ConsoleAppender(
        new PatternLayout(" % p % t % m % n"),
        ConsoleAppender.SYSTEM_OUT));
    logger.info("hello");
}
```

That worked; a log message that include "hello" came out the console!

Turns out when we remove `ConsoleAppender.SystemOut`, it's still working, but if we remove the pattern it once again complains about the lack of output stream.

Looking a little more carefully at the documentation, we see that the default `ConsoleAppender` constructor is not configured.

A bit more googling, reading and testing and we eventually wind up with:

```java
public class LogTest {
    private Logger logger;

    @Before
    public void initialize() {
        logger = Logger.getLogger("logger");
        logger.removeAllAppenders();
        Logger.getRootLogger().removeAllAppenders();
    }

    @Test
    public void basicLogger() {
        BasicConfigurator.configure();
        logger.info("basicLogger");
    }

    @Test
    public void addAppenderWithStream() {
        logger.addAppender(new ConsoleAppender(
            new PatternLayout(" % p % t % m % n"),
            ConsoleAppender.SYSTEM_OUT));
        logger.info("addAppenderWithStream");
    }

    @Test
    public void addAppenderWithoutStream() {
        logger.addAppender(new ConsoleAppender(
            new PatternLayout(" % p % t % m % n")));
        logger.info("addAppenderWithoutStream");
    }
}
```

Now we know hot to get a simple console logger initialized, and we can encapsulate that knowledge into our own logger class so that the rest of our application is isolated from the `log4j` boundary interface.

### Learning Tests Are Better Than Free

The learning tests end up costing nothing. We had to learn the API anyway, and writing those tests was an easy and isolated way to get that knowledge. The learning tests were precise experiments that helped increase our understanding.

Not only are learning tests free, they have a positive return on investment.

- We have more knowledge about third-party packages
- We can identify the behavioral differences
- We can match our expectation with third-party packages
- We can test new change to third-party packages based on tests we wrote for our expectation

Whether you need the learning provided by the learning tests or not, a clean boundary should be supported by a set of outbound tests that exercise the interface the same way the production code does.

### Using Code That Does Not Yet Exist

There are often places in the code where our knowledge seems to drop off the edge.

While working on the project, the author encountered a boundary where the system needed to interact with an undefined API. To avoid delays, the author created a placeholder interface called **Transmitter**, with a method `transmit` that represented the desired functionality: transmitting data on a specific frequency.

By defining this interface, the author maintained control, kept the code clear and focused on its purpose, and ensured progress could continue without waiting for the final API design.

![using-code-that-is-not-exist](https://github.com/user-attachments/assets/dbd97c44-907a-4905-b9a7-2a7f9b597439)


They kept `TransmitterAdapter` that encapsulated the interaction with the API and provides a single place to change when the API evolves.

This design also gives us a very convenient seam in the code for testing. Using a suitable `FakeTransmitter`, we can test the `CommunicationsController` classes.

We can also create boundary tests once we have the `TransmitterAPI` that make sure we are using the API correctly.

### Clean Boundaries

Interesting things happen at boundaries. Change is one of those things. Good software designs accommodate change without huge investments and rework.

Code at the boundaries needs clear separation and tests that define expectations. It's better to depend on something you control than on something you don't control.

Either way our code speaks to us better, promotes internally consistent usage across the boundary, and has fewer maintenance points when the third-party code changes.
