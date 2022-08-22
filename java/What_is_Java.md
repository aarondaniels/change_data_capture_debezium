# What Is Java?

Java is a class-based, object-oriented programming language that is designed to have as few platform dependencies as possible.

An important concept to understand is that Java, unlike Python, which is only interpreted, is also a compiled programming language. Typically, a compiler’s main functionality is to convert high-level language to low-level language that can be understood by the machine.

Basically, the Java compiler, just like any other compiler, does the task of translation. In other words, a compiler translates code from human-understandable form to a platform- (i.e., operating system-) understandable code.

The Java compiler does not translate Java classes directly to machine code. Rather, it converts the Java classes called bytecodes by generating files with the .class file extensions. This bytecode is created for a virtual platform, the Java virtual machine (JVM).

First, the bytecode verifier in the JVM checks the bytecode. Then, the JVM converts the bytecode to machine-understandable code.

This explains how Java achieves its platform independence. Since the JVM converts the bytecode to a machine specific code, there are different JVMs for different platforms.

# What Are Data Types in Java and How Do They Differ?

Every time that a variable is used within your code, the compiler must know how to interpret and use the variable’s data. Java programming, by design, has set data types to avoid undesired errors when processing data. This is why Java is referred to as a statically typed programming language. This also means a variable’s type cannot change once declared, unlike in other languages, such as Python.

For example, consider that you’re writing a simple function that, given two integers, calculates the average. The function would look something like this:

average = (a+b) / 2;

Ask yourself: What should happen if either a or b are not of type integer? What if they are a float, a double, or even a string? Java solves this by having strict data typing rules. Unlike Python and other languages, in Java, you must declare a variable’s data type, as it is instantiated.

The eight primitive data types in Java are delineated in the table below:

## Java Data Types

| Byte | Whole numbers 
- E.g., 128 to 127
- One byte of storage required |
| Long | Large whole numbers

E.g., 9,223,372,036,854,775,808 to 9,223,372,036,854,775,807
Eight bytes of storage required
 Float

 Decimal numbers

Stores six or seven decimal digits
Four bytes of storage required
 Double

 Precise decimal numbers

Stores up to 15 decimal digits
Eight bytes of storage required
 Boolean

 True or false

One bit of storage required
 Char (Character)

 Single characters

Two bytes of storage required
E.g., A, 4, or #
 Short

 Whole numbers

E.g., 32,768 to 32,767
Two bytes of storage required
int, long, float, double, boolean, char
 Int (Integer)

 Whole numbers

E.g., 2,147,483,648 to 2,147,483,647
Four bytes of storage required
What Is Casting?

Casting is a technique used in Java, and in Python as well, to change a variable’s data type. If a string needs to be converted into an integer, the string will need to be casted as an int, as shown below.

String stringnumber  = “12”;
Int number  = Integer.valueof(stringnumber);

Note: It is possible to do the same conversion from an integer to a string by using the code below:

String.valueOf([integer])

Data Type Hierarchy

In Java, there is a specified hierarchy of data types when performing math operations. One common rule of Java is that the result of a math operation will always inherit the most precise data type used within the equation. For example, when taking the sum of a double and an integer, the result will always be a double. When dividing two integers, the answer will always result in an integer.

This may seem counterintuitive at first, but it is one of the many quirks of Java.

To see this Java characteristic in practice, try it out. Try dividing different data types to see the different outputs. See some examples below:

2 / 3 = 0
0 / 3 = 0.66666667
0/3.0 = 0.66666667
Classes vs. Objects in Java

Java classes and objects go hand in hand and are often misused in conversation. To get a better understanding of the differences, think of a class as a recipe and an object as the completed dish.

Classes are what you, the programmer, write out and set characteristics to. Like a recipe, each class can have required ingredients; these are a class’s variables and constructor parameters. The recipe will also have instructions on how to use these ingredients; these are methods within the class that utilize the variables.

Objects, on the other hand, resemble a finished dish. Objects are instances of a predefined class within a program. After writing a recipe, the chef will send out copies to all of their friends, who will then go and make their own instances of that recipe and use it to feed their families.

How Can Classes and Objects Be Used in My Java Program?

In most cases, a completed program is going to consist of hundreds, if not thousands, of lines of code. If this were all written in a single Java file, debugging and adding features would become nearly impossible. Java solves this problem by allowing the use of packages. Packages allow for programmers to reference certain parts of code even though it may be outside another code’s directory. This produces one of Java’s most desired features: modularity.

Packages allow a programmer to instantiate classes into objects within other classes. This may seem complex at first. However, if you continue to use the recipe metaphor from above, it can be simplified.

If a chef friend were to send you their cookbook, they could simply not tell you to make chicken and expect you to reference a specific recipe. This is because there are most likely multiple chicken recipes within the cookbook. In order for you to complete the task, your friend must tell you specifically to “Cook the Pesto Chicken on page 144.” Packages act in a similar way. If a programmer wishes to generate a new object from a class and that class is not in the current directory, then the programmer must provide a location to look for the class.

This all is done with an import statement at the beginning of the code. Once a package is imported, the classes within the package can now be used in the current scope, as they are defined within the new class itself.