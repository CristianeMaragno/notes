

![[history.jpg|600]]

The focus is on the languages that caused more impact and also subjectively chosen and don't cover all of computer history.

#### Fortran
Together with the first computer to implement indexing and float-point instructions in hasrdware(IBM 704), "The IBM mathematical FORmula TRANslating system" is considered the first widely used high level language and brought great advances to computing.

**Context**
- Small, slow and unreliable memory
- Primary use for scientific computing
- The cost of computers were higher than programmers, so the focus was on computing speed

They created the highly optimized compilers and changed the way computers were used, exceeding expectations on efficiency compared with the code produced by hand.
![[fortran.jpg|300]]

#### LISP
The functional programming was invented to facilitate list processing, what was a necessity in the area of artificial intelligence. 

Pure LISP  has two data structures: Atom(symbols or numeric literals(Ex: +7.0)) and lists
All computation is made by applying functions to arguments. The is no need for assignment of statements and variables like imperative programming  and the loops are replaced by recursive function calls.

Two widely used dialects of LISP are 
Scheme: Small language with simple syntax suited for educational applications.
COMMON LISP: Was created combining features of different dialects with the purpose of solving the portability problem

![[lisp.jpg|300]]


#### ALGOL 60
After FORTRAN, many languages began to be created, but all of the were tied to specific computer architectures(Ex: UNIVAC and IBM 700). So, it was decided to create a universal language for scientific applications.

In many ways it was a descendant of Fortran, trying to combine simplicity and elegance, ALGOL: 
- Formalized the concepts of datatypes
- Added the ideiafo compound statements(connect statements like ```statement1 ^ statement2```)
- Generalised some of Fortran features(Like size of identifiers and array dimensions)
- Allowed nested statements
- Added the concept of block structures
- Procedures could be recursive

Every imperative language since 1960 has some influence from ALGOL 60

![[algol.jpg|300]]

#### COBOL
Similar to ALGOL, the goal was to make a common language, now focused on business. During the design process, the creators wanted the language
- To use english as much as possible
- To be easy to use
- To separate data description and executable operations
- Allowed meaningful names(up to 30 characters)
- Added hierarchical data structures(Ex: Trees)

#### ALGOL 68
Brought several ideias that later influenced many modern languages, even although never had widespread use.
- Primary focus on othogonality
- User defined data types(Offers primitive types and allow the user to combine those in a bigger number of structures)
- Dynamic arrays(The storage allocation happens during assigments)

#### Pascal
Made by a member of ALGOL 60 development team, Pascal is descendant that focus on what its predecessor failed the most: Simplicity
By the mid 70s, it was widely used for teaching programming, even if too limited to advanced applications

![[pascal.jpg|400]]

#### C
Influenced by ALGOL 68, C adopted
- For and Switch statements
- Assigning operators
- Pointers treatment

The lack of type checking got critics, but some like the flexibility. C's great popularity in the 80s is thanks to its compiler being part of UNIX OS

#### Prolog
The PROgramming LOGic language uses predicate calculus(Symbolic logic that exhibits the logical relations between sentences) instead of procedures.

```
//Facts
food(burger).  // burger is a food
food(sandwich). // sandwich is a food

//Rules
meal(X) :- food(X). // Every food is a meal OR Anything is a meal if it is a food

//Queries / Goals
?- food(pizza). // Is pizza a food?
?- meal(X), lunch(X). // Which food is meal and lunch?
?- dinner(sandwich) // Is sandwich a dinner?
```

For being highly inefficient and being a good approach for only a small areas, never was widely used.

#### Ada
Name inspired by the countess of lovelace, Ada is language created to solve the problems of the Department of defense(DoD), that widely used embedded systems and with over 500 different languages. It was designed by a large international group and is inspired in Pascal, some of the main contributions of this languages was
- Packages for encapsulating objects, data types etc
- Facilities for exception handling
- Concurrent execution

But, Ada became to large and complex. Some even called unreliable, what goes against its initial purpose.
![[ada.jpg|400]]

Ada 95 is a sucessor and embodied important ingredients of object oriented programming on the language like inheritance and polymorphism, but its popularity suffered because DoD stopped requiring Ada for military software and C++ success. 

#### Smalltalk
Smalltalk is the first language to fully support object oriented programming, being influenced by SIMULA 67. The creator wanted to make a simple and graphical language because he believed that normal people would be programming when the price of computers dropped significantly. 
The syntax is vastly different from other programming languages because it uses messages instead of arithmetic and logic expressions.
![[smalltalk.png|300]]
![[smalltalk2.jpg|300]]

#### C++
C++ was build on top of C influenced by SIMULA 67 to support what smalltalk pioneered on. Different from C, has object oriented programming and type checking. Through the years, received multiple corrections based on users feedback.
Has both functions(set of instructions to perform a task) and methods(set of instructions associated with an object) supports procedural and object oriented programming, has a good and inexpensive compiler and is almost backwards compatible with C. On the other hand is large, complex and inherited several insecurities from C, which makes less safer than Ada and Java.

#### Java
Java was based on C++, but designed to be smaller, simpler and reliable. The original use was for embedded customer eletronic devices, like toasters and ovens, even through the products that used the language never were marketed. Java became popular with the creations on the world wide web, in particular because of the java applets, relatively small programs.
- Is not possible to write stand-alone subprograms in Java, only inside a class, what makes the language only support object oriented programming
- Facilitate concurrency with its threads
- Has garbage collection that relives the programmers of doing the memory liberation 

#### Perl
Early script languages were a set of commands put in a file(script) to be interpreted without the need of compiling. The sh(shell) was the first of the type and it was used to call the OS subprograms. After that, many features were added to these languages to become more powerful, like ksh and awk.

Perl was a combination of sh and awk, but still needed to be compiled into a intermediate language.
- Has statically typed variables, with the first character to define namespace(scalar variables, arrays and hashs)
- Dynamic length arrays
- It has problems causing errors converting strings or array indexing depending on the context and not trowing exceptions(errors)

#### JavaScript
Computing in the browser stated with the Java applets, but rapidly were replaced by scripting languages like JavaScript that is interpreted when the html+jd file is displayed.
The primary uses of js was to validate forms and create a dynamic html file.
- Is not typed
- Arrays have dynamic length
- Doesn't support object orientation, but it was influenced by
- Doesn't support inheritance
- Defines object hierarchical model based on the html document(DOM)

#### PHP
PHP was created to track visitors on a website, the original name was Personal Home Page, but later it was renamed to Hypertext Preprocessor.
It was a language born for the web, it's open source and is interpreted on the web server. It started to support OO later

#### Python
Python is a open source, object oriented scripting language.
- Is type checked, but dynamicaly typed
- Instead of arrays, python has lists, immutable lists(tuples) and hashed(dictionaries)
- Has exception handling
- Garbage collection

#### Ruby
Ruby was born because its creator was unsatisfied with Perl and Python, languages that are not purely object oriented. Similar to Smalltalk, in Ruby every data value is an object and any operation happens via method call. Classes and objects are dynamic in the sense that the methods can change at different moment of execution.


#### C#'
C# was developed by Microsoft and is based on C++ and Java. Some believe that the advance of Java was to eliminate some C++ features, but C# brings several ones back with improvements.



