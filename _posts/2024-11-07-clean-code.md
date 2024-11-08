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

- Grady Booch, author of *Object Oriented Analysis and Design with Applications*

_Clean code is simple and direct. Clean code reads like well-written prose. Clean code never obscures the designer’s intent but rather is full of crisp abstractions and straightforward lines of control._ - Readability perspective - Live novel, clean code should clearly expose the tension in the problem to be solved. - Crisp Abstraction ("crisp" near to word concrete)

- “Big” Dave Thomas, founder of OTI, godfather of the Eclipse strategy

_Clean code can be read, and enhanced by a developer other than its original author. It has unit and acceptance tests. It has meaningful names. It provides one way rather than many ways for doing one thing. It has minimal dependencies, which are explicitly defined, and provides a clear and minimal API. Code should be literate since depending on the language, not all necessary information can be expressed clearly in code alone._ - Desire for readability - Code without test is not clean - Minimal: Smaller code is better

- Michael Feathers, author of *Working Effectively with Legacy Code*

_I could list all of the qualities that I notice in clean code, but there is one overarching quality that leads to all of them. Clean code always looks like it was written by someone who cares. There is nothing obvious that you can do to make it better. All of those things were thought about by the code’s author, and if you try to imagine improvements, you’re led back to where you are, sitting in appreciation of the code someone left for you—code left by someone who cares deeply about the craft._

- Ron Jeffries, author of *Extreme Programming Installed* and *Extreme Programming Adventures in C#*

_In recent years I begin, and nearly end, with Beck’s rules of simple code. In priority order, simple code:_
• *Runs all the tests;*
• *Contains no duplication;*
• *Expresses all the design ideas that are in the system;*
• *Minimizes the number of entities such as classes, methods, functions, and the like.*
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
