Java is one of the main [[Programming languages]] that exists and is widely used for

The success is due to
- The friendly syntax
- Object oriented
- Memory management
- Portability("write once, run anywhere")
- Secure(Sandbox environment)

But, all those perks come at the cost of
- Poor performance(Because of JVM)
- Verbose code

**Java nowdays**
Used mostly for enterprise applications and android development, java still ranks as one the most popular languages. Java is the swiss army knife of programming languages.

**Enviroment**
To execute a program in java you need to download and install a JDK(Java development kit). Also need to add a PATH like bellow

```
export PATH=$PATH:/usr/lib/jvm/jdk-17-oracle-x64/bin
```

This is necessary because the OS doesn't know the commands java and javac, so we specify where java binary executable files are. After this, the computer can load all needed code, including the compiler and interpreter.

**Run**
- Write a java code in a file with the extension .java(Any java program needs at least one class and one main method. The main method is where your program will start to be executed)
- Compile your code using javac (Ex: javac Test.java), this will generate a bytecode file with .class extension
- You execute your bytecode file with the command java(Ex: java Test)

**Java versions**
When java 1.2 was out, the alterations where so important, that it was decided to call Java 2. After that, there was the versions 1.3 and 1.4 still called Java 2. When the 1.5 was published, they called java 5 or "Tiger"

![[java.jpg|400]]

**Info dump**
- A JAVA program is a group of classes, with one main method. If your final user doesn't have a JVM, you include JRE-Java Runtime Environment(even different ones for multiple platforms) on you app installation bundle.
- For distribution, you can bundle oyur classes in a Java Archive(.jar file) that uses the format pkzip. In this file, you can include a simple text called manifest that define which class has the main() method and other configurations

#### JVM
The JVM makes possible "write once, run anywhere" and is a virtual machine that runs on the host hardware.
Compiled language(like C and C++) are compiled to a specific platform machine code, Interpreted languages(like JavaScript and python) are executed directly without compiling. With java, the compiled byte code(.class files) can be run in any version of JVM.

The JVM has three components:
- Class Loader: Transform the byte code of class or interface to the original file, combines the class dependencies and executes the initialization method
- Runtime Memory/Data Area: Allocate and manipulate the class data in the Heap memory and administrate threads
- Execution Engine: Converts byte code into machine language and executes, trying to optimizate the code, and use garbage collector to remove useless classes

![[jvm.png]]
Link: https://www.freecodecamp.org/news/jvm-tutorial-java-virtual-machine-architecture-explained-for-beginners/

Stack: Where method calling and local variables stay
Heap: Where all objects, instance variable stay
#### Garbage collector
The JVM has a Heap memory where all objects created are saved, allocating space accordingly with the object needs(Like number of variables).

Also, there is an automated garbage collector that scans the heap memory and delete class that are no longer being used(Like unreachable/without reference objects). In Java, you don't have control over this process, unlike in languages like C and C++.

#### Java Fundamentals

**[[Data structures]] in Java**

**[[Object oriented programming]]**
- Superclasses are the parents and subclasses are the one that inherit;
- Public members are inherited, different from the privates;
- You can use the type of the super class when creating the instance of your object ```Animal myDog = new Dog()```. This permits things like polymorphic matrices.
- What can prevent a class of being extended?
	- If the class is not public(Can only be accessed from classes in the same package)
	- The final modifier in the class, indicating that the class is at the end of inheritance line
	- If only has private constructors
- You can't extend more than one class
- Interfaces are totally abstract classes(Can't be instantiated). They make possible to force behaviors even when inheritance is happening, because their abstract methods have to be implemented in the first concrete class in the inheritance line. You can have multiple interfaces, even when a class is extending another ```class Dog extends Canine implements Pet{}```. You can also use the interface class to reference any object that implements it(Like for list of Pets), even if the're not from different inheritance trees.
- Como saber se você deve criar uma classe, uma subclasse, uma classe
abstrata ou uma interface?
	- Crie uma classe que não estenda nada (a não ser Object) quando sua nova classe não passar no teste É-UM com nenhum outro tipo.
	- Crie uma subclasse (em outras palavras, estenda uma classe) somente quando tiver que criar uma versão mais específica de uma classe e precisar sobrepor ou adicionar novos comportamentos.
	- Use uma classe abstrata quando quiser definir um modelo para um grupo de subclasses e tiver pelo menos algum código de implementação que todas as subclasses possam usar. Torne a classe abstrata quando quiser garantir que ninguém possa criar objetos desse tipo.
	- Use uma interface quando quiser definir uma função que outras classes possam desempenhar, independentemente de onde essas classes estejam na árvore de herança.
- Constructors: Method executed when a class is instantiated with new
	- Can't have return type
	- You can have multiple constructors. This is called constructor overloading
	- 

**Packages**
Packages that begin with java are first class packages embodied in the language. The ones starting with javax were extensions promoted to embodied.
When you import a class, it doesn't makes your class file bigger(Different from include in C).
- Collections
- Serialization

**Syntax**
- public: Can be accessed from outside of the class;
- private: Can't be accessed from outside of the class;
- static: Allow a method to be executed without their class being instantiated. This is useful when a method will always do the same thing, so there is no need to create objects. In this case, the static method doesn't live in a object, but in the class.
- final: Classes can't be instantiated, methods can't be changed. 

Method overloading: You have two methods with the same name, but with different parameters. Is not polymorphism.  

A local variable lives while in the stack, that is, until method is executed

**Data types and variables**
Variables with primitive types: Boolean, char, byte, short, int, longo, float and double
Obs: The compiler always tries to avoid overflow, even if your number can fit in another variable(byte b = 24) because it can judge something to big and with potential of overflow.

Reference variables: When a object is created, you keep in the variable only the reference to the object that in fact lives in the heap. Each JVM has its own reference variable size and representation.

Instance variables are declared inside the class, but not inside methods(local variables). They have a default value even if you explicitly assign it(Boolean will receive false, integers 0, etc). 

Generics:

**Conditions**
- The operator == compares the bits

**Methods**
- When you pass a parameter, you are passing a copy of the variable. With objects, what you are passing is a copy of the reference to the object;
- The value returned has to be of the type declared or a type that can be implicitly elevated(Ex: A function that returns a byte to a int variable). Or the returned value can be explicitly converted to a lower type(Ex: Float to int);
- Function naming is camelCase;
- Parameters are local variables;

#### Threads

#### Deeper concepts

#### Tools and frameworks
Web frameworks

Build tools

ORM
#### Tests
