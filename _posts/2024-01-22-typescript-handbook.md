---
title: TypeScript Handbook
date: 2024-01-22 10:00:00 -500
categories: [typescript, handbook]
tags: [typescript]
---


## Introduction to TypeScript

### What is TypeScript?

- A Programming language created by Microsoft.
- Disciplined JavaScript
- Top layer of JavaScript
- Every JavaScript code is also TypeScript code
- Features
    - Static Typed: Give type of variable at compile time.
- Drawback
    - Drawback: Compilation to JavaScript

### TSC configuration File

```typescript
tsc --init
```

- It will generate “tsconfig.json” file which includes all the configuration of how the TypeScript file will be compiled into JavaScript Files.
- We can Specify Source (TypeScript Files) and Destination (JavaScript Files) Path in this configuration JSON File.

### TSC Command

```bash
tsc
```

- It will generate “index.js.map” file which contains some of the configuration which is understood by the compiler.

### TypeScript Debugger in VSCODE

![TS Debugger VSCODE](https://github.com/omjogani/blogs/assets/72139914/5beba55c-930b-4f8c-aec8-a42da1c8e257)

- This is debug configuration file which will used for debugging purpose in VSCODE.
- Here we have added line no 15 that will let the compiler know to perform specified operation (It’s Case Sensitive).

### Hello World

```typescript
console.log("Hello World");
```

## Fundamentals of TypeScript

### Built in Types

- JavaScript
    - number
    - string
    - boolean
    - null
    - undefined
    - object
- TypeScript
    - any
    - unknown
    - never
    - enum
    - tuple
- Code Examples
    
    
    ```tsx
    let sales: number = 123_456_789; // if large number, put '_' to make code readable
    let course: string = 'TypeScript';
    let is_published: boolean = true;
    
    let sales1 = 123_456_789; 
    let course1 = 'TypeScript';
    let is_published1 = true;
    ```
    
    - Lines no 1 to 3 & Line No. 5 to 7 will be treated exactly same.
    

### Any Type

- Code Examples
    
    ```tsx
    let level;
    level = 1;
    level = "a";
    
    function render(document){ // ERROR: document is of type any
        console.log(document);
    }
    ```
    
    - This error can be solved by specifying “document: any” in arguments explicitly.
    - We can change flag “noImplicitAny"  to false in `tsconfig.json` file to solve this error.
    
    ![npImplicitAny](https://github.com/omjogani/blogs/assets/72139914/4fc2dba3-b42f-4e2b-918c-3556bcabebf8)
    
    - Only change this flag if you are aware about it otherwise it will cause the problem
    - For More: [https://www.typescriptlang.org/tsconfig#noImplicitAny](https://www.typescriptlang.org/tsconfig#noImplicitAny)

### Arrays

- Code Examples
    
    ```tsx
    let numbers: number[] = [1, 2, 3]; // type number[]
    let numbers1 = [1, 2, 3]; // type number[]
    let numbers3 = []; // type any[]
    numbers3[0] = 1;
    numbers3[1] = '1';
    ```
    
    - Like in third case we should mention type of the variable.

### Tuples

- Code Examples
    
    ```tsx
    let user: [number, string] = [1, "Om"];
    user.push(1); 
    // Above line will add third value but compiler is not complaining
    ```
    
    - Generally Used when we want to have key-value pairs.

### Enums

- Code Examples
    
    ```tsx
    const small = 1;
    const medium = 2;
    const large = 3;
    
    // PascalCase
    const enum Size {Small = 1, Medium, Large}
    let mySize: Size = Size.Medium;
    console.log(mySize); // 2
    ```
    
    - After Assigning one Enum, rest of all will be incremented like Medium will be 2, Large will be 3 etc.

### Functions

- Code Examples
    
    ```tsx
    function calculateTax(income: number, texYear = 2022): number {
        let x;
        if(texYear < 2022){
            return income * 1.2;
        }
        return income * 1.3;
    }
    
    calculateTax(10_000, 2022);
    ```
    
    - Default type of the function is void but it’s better to define return type in the function. It we set noImplicitReturn to true then It will give compiler time error if we don’t return any value.
    - if There is a variable passed in the argument but haven’t use then we set “noUnusedParameters” : true, this will give us warning that specified parameter isn’t used.
    - If there is a local variable declared and it is not used then we can set flag “noUnusedLocals” : true, It will give us warning that local variable isn’t used.
    
    ![noUnusedLocals](https://github.com/omjogani/blogs/assets/72139914/f0018202-ef94-42e6-a90d-8db6661b5544)
    
    - We can use traditional approach to deal with default parameter that is, Make the parameter optional and assign default parameter
    
    ```tsx
    function calculateTax(income: number, texYear?:number): number {
        if((texYear || 2022) < 2022){
            return income * 1.2;
        }
        return income * 1.3;
    }
    
    calculateTax(10_000);
    ```
    
    - Else We can directly assign default value in parameter it self.
    
    ```
    function calculateTax(income: number, texYear = 2022): number {
        if(texYear < 2022){
            return income * 1.2;
        }
        return income * 1.3;
    }
    
    calculateTax(10_000);
    ```
    

### Objects

- Code Examples
    
    ```tsx
    let employee: {
        readonly id: number,
        // name?: string, // Work fine
        name: string,
        retire: (date: Date) => void
    } = {
        id: 1,
        name: "Om",
        retire: (date: Date) => {
            console.log(date);
        }
    };
    ```
    
    - Whenever we want to assign value to specified object variables we can make that property optional that works fine.
    - readonly property will not allowed to change the value of that property anymore.

## Advanced Types

### Type Aliases

- Code Examples
    - The Problem with Simple Object is that We have to repeat the schema of object if we want to use it multiple times. So, to solve this problem we use **Type Aliases**
    
    ```tsx
    type Employee = {
        readonly id: number,
        name: string,
        retire: (date: Date) => void
    }
    
    let employee: Employee = {
        id: 1,
        name: "Om",
        retire: (date: Date) => {
            console.log(date);
        }
    };
    ```
    
    - We can use **Employee** at multiple places.

### Union Type

- Code Examples
    
    ```tsx
    function kgToLps(weight: number | string) {
        // Narrowing
        if (typeof weight == 'number') {
            return weight * 2.2;
        }
        return parseInt(weight) * 2.2;
    }
    
    kgToLps(10);
    kgToLps("10");
    ```
    
    - While we have used **Union Type** here then parameter can be send as number and string and that can be handled inside the function by narrowing operation (typeof).

### Intersection Type

- Code Examples
    
    ```tsx
    type Draggable = {
        drag: () => void
    };
    
    type Resizable = {
        resize: () => void
    };
    
    type UIWidget = Draggable & Resizable;
    
    let textBox:  UIWidget = {
        drag: () => {},
        resize: () => {},
    }
    ```
    
    - When we use **Intersection Type** then Type can be of both specified type, Here in this case it’s **Draggable and Resizable**.

### Literal Type

- Code Examples
    
    ```tsx
    // Literal (exact, specific);
    type Quantity = 50 | 100;
    let quantity: Quantity = 100;
    
    type Metric = 'cm' | 'inch';
    ```
    
    - When we want to make a variable to set specific size or value. Normally If we do something like ‘**let quantity : number;**’  then it can accept any number. So, we can use Literal here.
    - We have made literal use more productive and cleaner by using **Type Aliases** and **Union Type.**

### Nullable Type

- Code Examples
    
    ```tsx
    function greet(name: string | null | undefined) {
        if (name){
            console.log(name.toUpperCase());
        } else {
            console.log('Hoo!');
        }
    }
    
    greet(null);
    ```
    
    - When we work with null value and pass this value to the function which is not accepting the null values then we get an error, because it’s all handle by the flag “**strict**” **: true,** there is also other flag by overriding that flag we can get rid of null value.
    - The Flag is “**strictNullChecks**” **: false,** then default value will be changed to the false and it will not give error at compiler time. **We should not change this flag.**
    
    ![strictNullChecks](https://github.com/omjogani/blogs/assets/72139914/ae2f7342-8e02-4aa8-a61b-96ff92d581b9)
    

### Optional Chaining

- Code Examples
    
    ```tsx
    type Customer = {
        birthday?: Date,
    };
    
    function getCustomer(id: number) : Customer | null | undefined {
        return id === 0 ? null: { birthday: new Date()};
    }
    
    let customer = getCustomer(1);
    if(customer != null && customer != undefined){
        console.log(customer.birthday);
    }
    
    // Optional Property access operator
    console.log(customer?.birthday?.getFullYear());
    
    // Optional element access operator
    // console.log(customer?.[0]);
    
    // Optional call
    let log: any = (message: string) => console.log(message);
    log?.('a');
    ```
    
    - In the line no. 10, instead of checking condition that return value is null or undefined we can use optional chain operator that will execute the code if there is no null and undefined.
    - If there is null or undefined then it will print **undefined** in the console.
    - There is another use case of this operator that is last 2 lines of above program. when we have specified any as a type then it will accepts all the value including null and undefined so that we have to make sure that function  will not run on the type null or undefined so we can use **optional call**  at that moment.

### Nullish Coaelscing Operator

- Code Examples
    
    ```tsx
    let speed : number | null = null;
    let ride = {
        // Falsy (undefined, null, '', false, 0)
        // speed: speed || 30, // is speed is 0 then it will assign 30
        // nullish coaelscing operator
        speed: speed ?? 30, // use 30 if speed is not null and undefined
    }
    ```
    
    - In the above example if speed is 0 then it will assign speed to 30 because 0 is falsy value.
    - So, to solve this problem we have nullish coaelscing operator that will assign 30 only if speed is not null and undefined.

### Type Assertions

- Code Examples
    
    ```tsx
    // we say hey TS we know more about type of this object :)
    let phone = document.getElementById('phone') as HTMLInputElement;
    let phone2 = <HTMLInputElement> document.getElementById('phone');
    // * Above both lines are Same
    // HTMLElement - value not available
    // HTMLInputElement - value available
    let valueOfPhone = phone.value;
    ```
    
    - Here we are telling TypeScript that We know more about this object so please treat this object as I am saying.
    - We can do this by two ways
        1. By using **as objectName** 
        2. By Prefixing **<objectName>**

### The Unknown Type

- Code Examples
    
    ```tsx
    function render(document: unknown) {
        // Narrowing
        if (document instanceof WordDocument) {
            document.toUpperCase();
        }
        // document.move(); // can work in any, and crash if move not available
    }
    ```
    
    - If we have Primitive Types then we can use **typeof** and if we have custom types then we can use **instanceof** operator.

### The Never Type

- Code Examples
    
    ```tsx
    // specify this function will never returned
    function processEvents() : never {
        while (true) {
            // read a message from a queue
        }
    }
    
    processEvents();
    console.log("Hello World"); // dead code
    
    // -------------------------------
    
    function reject(message: string) : never {
        throw new Error(message);
    }
    
    reject('---');
    console.log("Hello World"); // dead code
    ```
    
    - We are specifying that this function will never gonna return so that code after written after call of the function will be dead code.
    - We can make use of tsconfig.json file to notify that there is dead code available in our code.
    - The Flag is **“allowUnreachableCode”: false,** that will give warning that this code is unreachable. ****
    
    ![allowUnreachableCode](https://github.com/omjogani/blogs/assets/72139914/3abe5213-02da-44c6-ad30-24015a77ee1c)
    

## Object Oriented Programming

### Classes

- Code Examples

    ```tsx
    class Account {
        id: number;
        owner: string;
        balance: number;
    
        constructor(id: number, owner: string, balance: number){
            this.id = id;
            this.owner = owner;
            this.balance = balance;
        }
    
        deposit(amount: number) : void{
            if (amount <= 0){
                throw new Error("Invalid Amount!");
            }
            this.balance += amount;
        }
    }
    ```
    
    - All the properties declared inside the class in the typescript will not be available in JavaScript after the compilation.

### Objects

- Code Examples
    
    ```tsx
    class Account {
        id: number;
        owner: string;
        balance: number;
    
        constructor(id: number, owner: string, balance: number){
            this.id = id;
            this.owner = owner;
            this.balance = balance;
        }
    
        deposit(amount: number) : void{
            if (amount <= 0){
                throw new Error("Invalid Amount!");
            }
            this.balance += amount;
        }
    }
    
    let account = new Account(1, 'Om', 0);
    account.deposit(100);
    console.log(account.balance);
    console.log(typeof account);
    console.log(account instanceof Account);
    ```
    
    - When we log **typeof account** then we get output as object so if we want to check that specific object is of specific Class then we can use **instancof.**

### Read only & Optional Parameter

- Code Examples
    
    ```tsx
    class Account {
        readonly id: number;
        owner: string;
        balance: number;
        nickname?: string; //optional
    
        constructor(id: number, owner: string, balance: number){
            this.id = id;
            this.owner = owner;
            this.balance = balance;
        }
    
        deposit(amount: number) : void{
            if (amount <= 0){
                throw new Error("Invalid Amount!");
            }
            this.balance += amount;
        }
    }
    
    let account = new Account(1, 'Om', 0);
    account.deposit(100);
    account.id = 0; // Invalid because it's readonly
    ```
    
    - We can define property as optional so that it doesn’t force to initialize in the constructor.
    - When we declare readonly property then that property will be only allowed to assign in constructor and if you try to assign value other than constructor then it gives you an error that **you can not assign value to readonly property.**

### Access Modifiers

- All Access Modifiers in TypeScript
    - Public
    - Private
    - Protected
- Code Examples
    
    ```tsx
    class Account {
        readonly id: number;
        owner: string;
        private _balance: number;
        nickname?: string;
    
        constructor(id: number, owner: string, balance: number){
            this.id = id;
            this.owner = owner;
            this._balance = balance;
        }
    
        deposit(amount: number) : void{
            if (amount <= 0){
                throw new Error("Invalid Amount!");
            }
            // Record a transaction
            this._balance += amount;
        }
    
        getBalance() :number {
            return this._balance;
        }
    
        private calculateTax(){
            // For Internal Use
        }
    }
    
    let account = new Account(1, 'Om', 0);
    account.deposit(100);
    // Private Property is not available here
    // but we can access it's value...
    console.log(account.getBalance());
    ```
    
    - Whenever we use private property then that variable or method won’t be available outside of that class.
    - It restrict then environment to use that specific property. By default all the properties are public.
    - GOOD CODE: Don’t use private properties for storing passwords and other secure information, although you can do that but it’s not good way to do that, there are some other ways for handling this situations.