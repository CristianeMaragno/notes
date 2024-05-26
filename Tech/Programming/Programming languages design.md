Most of the content of this page comes from insights of the book concepts of programming languages from Robert w. Sebesta

### Why learn concepts and design of a variety of programming languages?

The vocabulary/grammar that we know shapes or limits our thought process.

> *...we have learned is that people who speak different languages do indeed think differently and that even flukes of grammar can profoundly affect how we see the world.

Font: https://www.edge.org/conversation/lera_boroditsky-how-does-our-language-shape-the-way-we-think

Because of this phenomenon, a programmer can expand its knowledge of different languages aiming to also expand their ability of problem solving and abstract thinking. Ex of use: Simulate associative arrays in a language that doesn't have them

The knowledge of programming languages also helps the developer to choose the most adequate language that includes features to best address the problem at hand and will make the process of learning a new language easier. The market is constantly changing and evolving, what will make a developer adapt to new technologies multiple times through their career.

Know all the features, design choices and implementation issues gives the programmer a solid control of the language, so it can be explored in its full capacity.

### Domain

The goal of utilization of a language affects directly the priorities and choices made on its design and implementation

- Scientific applications: Simple data structures, but require large numbers of floating-point arithmetic computations. The first high level languages(Fortran and Algol) competed with assembly, so efficiency was a big concern;
- Business applications: Characterized by facilities for producing reports, precise ways of dealing with decimal numbers and character data. Their representative, COBOL, appeared in 1960.
- Artificial intelligence: The first language widely used for IA was the functional programming language LISP in 1959 and later Prolog.
- Systems programming: Used almost continuously and so requires eficiency. The unix OS is written mostly in C that doesn't have many restrictions and can be used for optimization.
- Web software: Supported by a vast collection of languages

### Language evaluation criteria

Following, there is list of criteria that can be used to analyse and compare different languages and understand the ideal choice for the domain in question.

There is always a trade-off and have all the criteria is impossible.

**Readability**
In the 70s, was understood the importance of maintenance, particularly in terms of cost, what made languages try to achieve 
- Overall simplicity: Have a smaller number of basic constructs, avoid having multiple ways of doing the same thing(feature multiplicity) and refrain from giving the same operator different functions(operator overload).
- Orthogonality: Is the balance of the possible combinations of primitives. Suppose a language has four primitive data types(int, float, double and char) and two type operators(array and pointer), this makes possible to have a large number of data structures defined by applying the operators to themselves and to the primitive data types(Array of pointers, array of char, pointer of int, etc). A lack of orthogonality leads to exceptions to the rules of the language and too much orthogonality can generate extremely complex constructs. Both extremes make learning the language harder.
- Data types: Enough to facilitate the comprehension of the code. If there is no boolean type, you can simulate using the number 1, bus this can be harder to understand

**Writability**
Affected by the same characteristics of readability because the developer has to frequently read the code already written. Also has to taken in consideration

- Support for abstraction: Abstraction means the ability to define and the use complicated structures or operations in ways that allow many of the details to be ignored.
- Expressiveness: A language has convenient ways of doing things. Examples: count++ instead of count = count + 1

**Reliability**
A program is said to be reliable if it performs to its specifications under all conditions. Features that improve a language reliability are

- Type checking: Testing for type errors on a program, either by compiler ou during execution. 
- Exception handling: The capacity of a program to identify run-time errors, take measures and continue the execution.
- Aliasing: Having two or more names used to access the same memory cell, Is widely accepted that is a dangerous feature for a language.

**Cost**
The cost of a programming language is a combinations of factors
- Training of programmers
- Time programming
- Hardware cost for compiling
- Hardware cost for executing
- Cost of licenses and similares
- Cost of error(Low reliability)

### Influences

**Architecture**

The language design is also influenced by the computer organization and architecture. Currently, the [[Von Neumann]] is mainly used, what benefits the most popular languages that are [[imperative programming]] language and use
- Variables: Model memory cell/address
- Statements: Based on piping operations
- Iterative repetition






