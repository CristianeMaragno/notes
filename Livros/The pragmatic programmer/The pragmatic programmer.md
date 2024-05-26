

The word pragmatic comes from the Latin pragmaticus—"skilled in business"—which itself is derived from the Greek, meaning "to do." This is a book about doing.

We feel that there is no point in developing software unless you care about doing it well.

Never run on auto-pilot. Constantly be thinking, critiquing your work in real time. Over the long term, your time investment will be repaid as you and your team become more efficient, write code that's easier to maintain, and spend less time in meetings.


"Kaizen" is a Japanese term that captures the concept of continuously making many small improvements. 

Every day, work to refine the skills you have and to add new tools to your repertoire. Unlike the Eton lawns, you'll start seeing results in a  matter of days. Over the years, you'll be amazed at how your experience has blossomed  and your skills have grown.


**The Cat Ate My Source Code
  
A Pragmatic Programmer takes charge of his or her own career, and isn't afraid to admit ignorance or error.

Don't blame someone or something else, or make up an excuse. Don't blame all the  problems on a vendor, a programming language, management, or your coworkers. Any and all of these may play a role, but it is up to you to provide solutions, not excuses.

Run through the conversation in your mind. What is the other person likely to say? Will they ask, "Have you tried this…" or "Didn't you consider that?" How will you respond?

  
**Software Entropy
  
Entropy is a term from physics that refers to the amount of "disorder" in a system. One broken window, left unrepaired for any substantial length of time, instills in the inhabitants of the building a sense of abandonment—a sense that the powers that be don't care about the building. So another window gets broken. People start littering. Graffiti appears. Serious structural damage begins. In a relatively short space of time, the building becomes damaged beyond the owner's desire to fix it, and the sense of abandonment becomes reality.

Don't leave "broken windows" (bad designs, wrong decisions, or poor code) unrepaired. Fix each one as soon as it is discovered. If there is insufficient time to fix it properly, then  board it up. Perhaps you can comment out the offending code, or display a "Not  Implemented" message, or substitute dummy data instead. Take some action to prevent  further damage and to show that you're on top of the situation.


**Stone Soup and Boiled Frogs

You may be in a situation where you know exactly what needs doing and how to do it. The entire system just appears before your eyes—you know it's right. But ask permission to tackle the whole thing and you'll be met with delays and blank stares.
It's time to bring out the stones. Work out what you can reasonably ask for. Develop it well.  Once you've got it, show people, and let them marvel. Then say "of course, it would be better if we added…." Pretend it's not important. Sit back and wait for them to start asking you to add the functionality you originally wanted. People find it easier to join an ongoing success. Show them a glimpse of the future and you'll get them to rally around.  

**Good-Enough Software

it is equally unprofessional to promise impossible time scales and to cut basic engineering corners to meet a deadline. The scope and quality of the system you produce should be specified as part of that system's requirements.


**Your Knowledge Portfolio

- Learn at least one new language every year. Different languages solve the same problems in different ways. By learning several different approaches, you can  help broaden your thinking and avoid getting stuck in a rut.

- Read a technical book each quarter. Read nontechnical books, too. It is important to remember that computers are used by people—people whose needs you are trying to satisfy. 

- Take classes.

- Experiment with different environments. 

The last important point is to think critically about what you read and hear. You need to  ensure that the knowledge in your portfolio is accurate and unswayed by either vendor or  media hype.

**Communicate!

When you're faced with an  important meeting or a phone call with a major client, jot down the ideas you want to communicate, and plan a couple of strategies for getting them across.

Say you want to suggest a Web-based system to allow your end users to submit bug  reports. You can present this system in many different ways, depending on your audience. 
End users will appreciate that they can submit bug reports 24 hours a day without waiting on the phone. Your marketing department will be able to use this fact to boost sales. 

Managers in the support department will have two reasons to be happy: fewer staff will be  needed, and problem reporting will be automated. Finally, developers may enjoy getting  experience with Web-based client-server technologies and a new database engine. By  making the appropriate pitch to each group, you'll get them all excited about your project

**The Evils of Duplication

Every piece of knowledge must have a single, unambiguous, authoritative  representation within a system.

- Imposed duplication. Developers feel they have no choice—the environment seems to require duplication.

- Inadvertent duplication. Developers don't realize that they are duplicating information.

- Impatient duplication. Developers get lazy and duplicate because it seems easier.

- Interdeveloper duplication. Multiple people on a team (or on different teams) duplicate a piece of information.

Structures in multiple languages can be built from a common metadata representation using a simple code generator each time the software is built

The DRY principle tells us to keep the low-level knowledge in the code, where it belongs,  and reserve the comments for other, high-level explanations. 

Say our analysis reveals that,  among other attributes, a truck has a type, a license number, and a driver. Similarly, a  delivery route is a combination of a route, a truck, and a driver. We code up some classes based on this understanding.

But what happens when Sally calls in sick and we have to change drivers? Both Truck and  DeliveryRoute contain a driver. Which one do we change? does a truck really have a driver as part of its underlying attribute set? Does a route? Or maybe there needs to be a third object that knits together a driver, a truck, and a route. 
Where possible, always use accessor functions to read and write the attributes of objects.

Impatient duplication is an easy form to detect and handle, but it takes discipline and a  willingness to spend time up front to save pain later.

On the other hand, perhaps the hardest type of duplication to detect and handle occurs  between different developers on a project.

At a high level, deal with the problem by having a clear design, a strong technical project  leader (see Pragmatic Teams), and a well-understood division of responsibilities within the  design. 

We feel that the best way to deal with this is to encourage active and frequent communication between developers. 


**Orthogonality

"Orthogonality" is a term borrowed from geometry. Two lines are orthogonal if they meet at  right angles, such as the axes on a graph. In vector terms, the two lines are independent.
Move along one of the lines, and your position projected onto the other doesn't change.

In computing, the term has come to signify a kind of independence or decoupling. Two or  more things are orthogonal if changes in one do not affect any of the others. In a well-designed system, the database code will be orthogonal to the user interface: you can change the interface without affecting the database, and swap databases without changing the interface.

Eliminate Effects Between Unrelated Things

**Design

Most developers are familiar with the need to design orthogonal systems, although they  may use words such as modular, component-based, and layered to describe the  process. Systems should be composed of a set of cooperating modules, each of which  implements functionality independent of the others. Sometimes these components are organized into layers, each providing a level of abstraction. This layered approach is a  powerful way to design orthogonal systems. Because each layer uses only the abstractions  provided by the layers below it, you have great flexibility in changing underlying implementations without affecting code. Layering also reduces the risk of runaway  dependencies between modules. 

Also ask yourself how decoupled your design is from changes in the real world. Are you  using a telephone number as a customer identifier? What happens when the phone  company reassigns area codes? Don't rely on the properties of things you can't control.

  

Coding

Keep your code decoupled. Write shy code—modules that don't reveal anything unnecessary to other modules and that don't rely on other modules' implementations.

  Avoid global data. 

  Avoid similar functions.

Testing

Building unit tests is itself an interesting test of orthogonality. What does it take to build and link a unit test? Do you have to drag in a large percentage of the rest of the system just to  get a test to compile or link? If so, you've found a module that is not well decoupled from the rest of the system.

Reversibility
Suppose you decide, early in the project, to use a relational database from vendor A. Much  later, during performance testing, you discover that the database is simply too slow, but  that the object database from vendor B is faster. With most conventional projects, you'd be  out of luck. Most of the time, calls to third-party products are entangled throughout the code. But if you really abstracted the idea of a database out—to the point where it simply provides persistence as a service—then you have the flexibility to change horses in midstream. There Are No Final Decisions

Flexible Architecture

While many people try to keep their code flexible, you also need to think about maintaining  flexibility in the areas of architecture, deployment, and vendor integration 

If you keep decisions soft and pliable, it won't be hard at all. If you have poor encapsulation, high coupling, and hard-coded logic or parameters in the code, it might be impossible.

Code That Glows in the Dark

Tracer bullets work because they operate in the same environment and under the same  constraints as the real bullets. They get to the target fast, so the gunner gets immediate feedback. And from a practical standpoint they're a relatively cheap solution.

To get the same effect in code, we're looking for something that gets us from a requirement  to some aspect of the final system quickly, visibly, and repeatably.

Prototyping generates disposable code. Tracer code is lean but complete, and forms part of the skeleton of the final system. Think of prototyping as the reconnaissance and intelligence gathering that takes place before a single tracer bullet is fired.


Prototypes and Post-it Notes

We tend to think of prototypes as code-based, but they don't always have to be. Like the car makers, we can build prototypes out of different materials. Post-it notes are great for prototyping dynamic things such as workflow and application logic. A user interface can be prototyped as a drawing on a whiteboard, as a nonfunctional mock-up drawn with a paint program, or with an interface builder.  

What sorts of things might you choose to investigate with a prototype? Anything that carries risk. Anything that hasn't been tried before, or that is absolutely critical to the final system

-Architecture

-New functionality in an existing system

-Structure or contents of external data

-Third-party tools or components

Performance issues

-User interface design

Here are some specific areas you may want to look for in the architectural prototype:

-Are the responsibilities of the major components well defined and appropriate?

-Are the collaborations between major components well defined?

-Is coupling minimized?

-Can you identify potential sources of duplication?

-Are interface definitions and constraints acceptable?

-Does every module have an access path to the data it needs during execution?

Estimating

basic estimating trick that always gives good answers: ask someone who's already done it. Before you get too committed to model building, cast around for someone who's been in a similar situation in the past.


The Basic Tools

Tools amplify your talent. The better your tools, and the better you know how to use them,  the more productive you can be. Start with a basic set of generally applicable tools. As you  gain experience, and as you come across special requirements, you'll add to this basic set. 

Like the craftsman, expect to add to your toolbox regularly. Always be on the lookout for better ways of doing things. If you come across a situation where you feel your current  tools can't cut it, make a note to look for something different or more powerful that would have helped. 

  
To ensure that we never lose any of our precious work, we should always use a Source  Code Control system—even for things such as our personal address book! And, since Mr. Murphy was really an optimist after all, you can't be a great programmer until you become highly skilled at Debugging.

  
Always Use Source Code Control

Always. Even if you are a single-person team on a one-week project. Even if it's a "throw-away" prototype. Even if the stuff you're working on isn't source code. Make sure  that everything is under source code control—documentation, phone number lists, memos to vendors, makefiles, build and release procedures, that little shell script that burns the CD master—everything. We routinely use source code control on just about everything we type (including the text of this book). Even if we're not working on a project, our day-to-day work is secured in a repository. 

There is a tremendous hidden benefit in having an entire project under the umbrella of a source code control system: you can have product builds that are automatic and  repeatable.

The project build mechanism can pull the latest source out of the repository automatically.
It can run in the middle of the night after everyone's (hopefully) gone home. You can run automatic regression tests to ensure that the day's coding didn't break anything. The automation of the build ensures consistency—there are no manual procedures, and you won't need developers remembering to copy code into some special build area.

Debugging

Fix the Problem, Not the Blame

It doesn't really matter whether the bug is your fault or someone else's. It is still your  problem.

Before you start debugging, it's important to adopt the right mindset. You need to turn off many of the defenses you use each day to protect your ego, tune out any project pressures you may be under, and get yourself comfortable. 

Beware of myopia when debugging. Resist the urge to fix just the symptoms you see: it is more likely that the actual fault may be several steps removed from what you are  observing, and may involve a number of other related things. Always try to discover the  root cause of a problem, not just this particular appearance of it.

- You may need to interview the user who reported the bug in order to gather more data than you were initially given.

- The best way to start fixing a bug is to make it reproducible. After all, if you can't  reproduce it, how will you know if it is ever fixed? 

- Often, the easiest way to discern what a program is doing—or what it is going to do—is to get a good look at the data it is operating on. The simplest example of this is a straightforward "variable name = data value" approach, which may be implemented as  printed text, or as fields in a GUI dialog box or list.

- Tracing statements are those little diagnostic messages you print to the screen or to a file  that say things such as "got here". Tracing is invaluable in any system where time itself is a factor: concurrent processes, real-time systems, and event-based applications

- A very simple but particularly useful technique for finding the cause of a problem is simply to explain it to someone else. It sounds simple, but in explaining the problem to another person you must explicitly state things that you may take for granted when going through the code yourself. 

Debugging Checklist

-Is the problem being reported a direct result of the underlying bug, or merely a symptom?

-Is the bug really in the compiler? Is it in the OS? Or is it in your code?

If you explained this problem in detail to a coworker, what would you say?

-If the suspect code passes its unit tests, are the tests complete enough? What happens if you run the unit test with this data?

-Do the conditions that caused this bug exist anywhere else in the system?

Pragmatic Paranoia

You Can't Write Perfect Software

We are constantly interfacing with other people's code—code that might not live up to our high standards—and dealing with inputs that may or may not be valid. So we are taught to code defensively. If there's any doubt, we validate all information we're given. We use assertions to detect bad data. We check for consistency, put constraints on database columns, and generally feel pretty good about ourselves.

But Pragmatic Programmers take this a step further. They don't trust themselves, either.
Knowing that no one writes perfect code, including themselves, Pragmatic Programmers  code in defenses against their own mistakes.

It is a simple yet powerful technique that focuses on documenting (and agreeing to) the rights and responsibilities of software modules to ensure program correctness. What is a correct program? One that does no more and no less than it claims to do. Documenting  and verifying that claim is the heart of Design by Contract 

The greatest benefit of using DBC may be that it forces the issue of requirements and guarantees to the forefront. Simply enumerating at design time what the input domain range is, what the boundary conditions are, and what the routine promises to deliver—or, more importantly, what it doesn't promise to deliver—is a huge leap forward in writing better software.

Dead Programs Tell No Lies

All errors give you information. You could convince yourself that the error can't happen, and choose to ignore it. Instead, Pragmatic Programmers tell themselves that if there is an  error, something very, very bad has happened. It's easy to fall into the "it can't happen" mentality. Most of us have written code that didn't check that a file closed successfully, or that a trace statement got written as we expected.

And all things being equal, it's likely that we didn't need to—the code in question wouldn't fail under any normal conditions. But we're coding defensively. We're looking for rogue pointers in other parts of our program trashing the stack. We're checking that the correct versions of shared libraries were actually loaded.

Assertive Programming

"This code won't be used 30 years from now, so two-digit dates are fine." "This application will never be used abroad, so why internationalize it?" "count can't be negative." "This printf can't fail."

Let's not practice this kind of self-deception, particularly when coding.

When to Use Exceptions

In Dead Programs Tell No Lies, we suggested that it is good practice to check for every possible error—particularly the unexpected ones. However, in practice this can lead to some pretty ugly code; the normal logic of your program can end up being totally obscured by error handling

An error handler is a routine that is called when an error is detected. You can register a  routine to handle a specific category of errors. When one of these errors occurs, the  handler will be called.

There are times when you may want to use error handlers, either instead of or alongside  exceptions.

Use Exceptions for Exceptional Problems

How to Balance Resources

We all manage resources whenever we code: memory, transactions, threads, flies, timers. 

Finish What You Start
This tip is easy to apply in most circumstances. It simply means that the routine or object that allocates a resource should be responsible for deallocating it.


Bend or Break
In order to keep up with today's near-frantic pace of change, we need to make every effort to write code that's as loose—as flexible—as possible. 


Decoupling and the Law of Demeter

In Orthogonality, and Design by Contract, we suggested that writing "shy" code is  beneficial. But "shy" works two ways: don't reveal yourself to others, and don't interact with  too many people.

Spies, dissidents, revolutionaries, and such are often organized into small groups of people  called cells. Although individuals in each cell may know each other, they have no  knowledge of those in other cells. If one cell is discovered, no amount of truth serum will  reveal the names of others outside the cell. Eliminating interactions between cells protects everyone.

We feel that this is a good principle to apply to coding as well. Organize your code into cells (modules) and limit the interaction between them. If one module then gets compromised and has to be replaced, the other modules should be able to carry on.

When we ask an object for a particular service, we'd like the service to be performed on our behalf. We do not want the object to give us a third-party object that we have to deal with to get the required service.

Traversing relationships between objects directly can quickly lead to a combinatorial explosion of dependency relationships. You can see symptoms of this phenomenon in a number of ways:

1 Large C or C++ projects where the command to link a unit test is longer than the

2 "Simple" changes to one module that propagate through unrelated modules in the system

3 Developers who are afraid to change code because they aren't sure what might be  affected

Metaprogramming

First, we want to make our systems highly configurable. Not just things such as screen  colors and prompt text, but deeply ingrained items such as the choice of algorithms,  database products, middleware technology, and user-interface style. These items should  be implemented as configuration options, not through integration or engineering.


Configure, Don't Integrate

Metadata is any data that describes the application—how it should run, what resources it should use, and so on.

But we want to go beyond using metadata for simple preferences. We want to configure  and drive the application via metadata as much as possible. Our goal is to think  declaratively (specifying what is to be done, not how) and create highly dynamic and adaptable programs. We do this by adopting a general rule: program for the general case, and put the specifics somewhere else—outside the compiled code base

Temporal Coupling

we are talking about the role of time as a design element of the software itself. There are two aspects of time that are important to us: concurrency (things happening at the same time) and ordering (the relative positions of things in time). 

Linear. That's the way most people think—do this and then always do that. But thinking this way leads to temporal coupling: coupling in time. Method A must always be called before method B; only one report can be run at a time; you must wait for the screen to redraw before the button click is received. Tick must happen before tock.

This approach is not very flexible, and not very realistic. We need to allow for concurrency

An activity diagram consists of a set of actions drawn as rounded boxes. The arrow leaving an action leads to either another action (which can start once the first action completes) or to a thick line called a synchronization bar. Once all the actions leading into a synchronization bar are complete, you can then proceed along any arrows leaving the bar. 

An action with no arrows leading into it can be started at any time.

and to think about decoupling any time or order dependencies. In

doing so, we can gain flexibility and reduce any time-based dependencies in many areas of 

development: workflow analysis, architecture, design, and deployment.

  

Architecture

  

We wrote an On-Line Transaction Processing (OLTP) system a few years ago. At its simplest, all the 

system had to do was read a request and process the transaction against the database. But we wrote 

a three-tier, multiprocessing distributed application: each component was an independent entity that 

ran concurrently with all other components. 

  

The design addresses the following constraints:

- Database operations take a relatively long time to complete.

- For each transaction, we must not block communication services while a database transaction 

is being processed.

- Database performance suffers with too many concurrent sessions.

- Multiple transactions are in progress concurrently on each data line.

  

<Img pg 196>

  

Each box represents a separate process; processes communicate via work queues. Each input 

process monitors one incoming communication line, and makes requests to the application server. All 

requests are asynchronous: as soon as the input process makes its current request, it goes back to 

monitoring the line for more traffic. Similarly, the application server makes requests of the database 

process,

[5]

 and is notified when the individual transaction is complete.

  

This example also shows a way to get quick and dirty load balancing among multiple consumer 

processes: the hungry consumer model.

In a hungry consumer model, you replace the central scheduler with a number of independent 

consumer tasks and a centralized work queue. Each consumer task grabs a piece from the work 

queue and goes on about the business of processing it. As each task finishes its work, it goes back to 

the queue for some more. This way, if any particular task gets bogged down, the others can pick up 

the slack, and each individual component can proceed at its own pace. Each component is temporally 

decoupled from the others.

  

Instead of components, we have really created services—independent, concurrent objects behind 

well-defined, consistent interfaces.

  

Design for Concurrency

  

To begin with, any global or static variables must be protected from concurrent access. Now may be a 

good time to ask yourself why you need a global variable in the first place. In addition, you need to 

make sure that you present consistent state information, regardless of the order of calls.

  

Objects must always be in a valid state when called, 

and they can be called at the most awkward times. You must ensure that an object is in a valid state 

any time it could possibly be called. Often this problem shows up with classes that define separate 

constructor and initialization routines (where the constructor doesn't leave the object in an initialized 

state).

  

It's Just a View

  

We'll start off with the concept of an event. An event is simply a special message that says "something 

interesting just happened" (interesting, of course, lies in the eye of the beholder). We can use events 

to signal changes in one object that some other object may be interested in.

Using events in this way minimizes coupling between those objects—the sender of the event doesn't

need to have any explicit knowledge of the receiver. In fact, there could be multiple receivers, each

one focused on its own agenda (of which the sender is blissfully unaware).

  

Publish/Subscribe: If we are interested in certain events generated by a Publisher, all we have to do is register ourselves. 

The Publisher keeps track of all interested Subscriber objects; when the Publisher generates an event 

of interest, it will call each Subscriber in turn and notify them that the event has occurred.

  

Model-View-Controller: Obviously, we don't want to have three separate copies of the data. So we create a model—the data 

itself, with common operations to manipulate it. Then we can create separate views that display the 

data in different ways: as a spreadsheet, as a graph, or in a totals box. Each of these views may have 

its own controller. The graph view may have a controller that allows you to zoom in or out, or pan 

around the data, for example. None of this affects the data itself, just that view.

  

Java Tree View: A good example of an MVC design can be found in the Java tree widget. The tree widget (which 

displays a clickable, traversable tree) is actually a set of several different classes organized in an MVC 

pattern.

To produce a fully functional tree widget, all you need to do is provide a data source that conforms to 

the TreeModel interface. Your code now becomes the model for the tree.

  

While MVC is typically taught in the context of GUI development, it is really a general-purpose

programming technique. The view is an interpretation of the model (perhaps a subset)—it doesn't

need to be graphical. The controller is more of a coordination mechanism, and doesn't have to be

related to any sort of input device.

  

<Imagem on PG 205>

  

This kind of model-viewer network is a common (and valuable) design technique. Each link decouples

raw data from the events that created it—each new viewer is an abstraction. And because the

relationships are a network (not just a linear chain), we have a lot of flexibility. Each model may have

many viewers, and one viewer may work with multiple models.

  

Blackboards

  

A blackboard system lets us decouple our objects from each other completely, providing a forum 

where knowledge consumers and producers can exchange data anonymously and asynchronously. 

As you might guess, it also cuts down on the amount of code we have to write.

  

With these systems, you can store active Java objects—not just data—on the blackboard, and retrieve

them by partial matching of fields (via templates and wildcards) or by subtypes. For example, suppose

you had a type Author, which is a subtype of Person. You could search a blackboard containing 

Person objects by using an Author template with a lastName value of "Shakespeare." You'd get Bill 

Shakespeare the author, but not Fred Shakespeare the gardener.

  

Programming by Coincidence

  

As developers, we also work in minefields. There are hundreds of traps just waiting to catch us each

day. Remembering the soldier's tale, we should be wary of drawing false conclusions. We should

avoid programming by coincidence—relying on luck and accidental successes— in favor of

programming deliberately.

  

Accidents of implementation are things that happen simply because that's the way the code is 

currently written. You end up relying on undocumented error or boundary conditions.

  

You can have "accidents of context" as well. Suppose you are writing a utility module. Just because 

you are currently coding for a GUI environment, does the module have to rely on a GUI being present? 

Are you relying on English-speaking users? Literate users? What else are you relying on that isn't 

guaranteed?

  

Coincidences can mislead at all levels—from generating requirements through to testing. Testing is

particularly fraught with false causalities and coincidental outcomes. It's easy to assume that X causes 

Y, but as we said in Debugging: don't assume it, prove it.

  

We want to spend less time churning out code, catch and fix errors as early in the development cycle 

as possible, and create fewer errors to begin with. It helps if we can program deliberately:

- Always be aware of what you are doing. Fred let things get slowly out of hand, until he ended 

up boiled, like the frog in Stone Soup and Boiled Frogs.

- Don't code blindfolded. Attempting to build an application you don't fully understand, or to use 

a technology you aren't familiar with, is an invitation to be misled by coincidences.

- Proceed from a plan, whether that plan is in your head, on the back of a cocktail napkin, or on 

a wall-sized printout from a CASE tool.

- Rely only on reliable things. Don't depend on accidents or assumptions. If you can't tell the 

difference in particular circumstances, assume the worst.

- Document your assumptions. Design by Contract, can help clarify your assumptions in your 

own mind, as well as help communicate them to others.

- Don't just test your code, but test your assumptions as well. Don't guess; actually try it. Write 

an assertion to test your assumptions (see Assertive Programming). If your assertion is right, 

you have improved the documentation in your code. If you discover your assumption is wrong, 

then count yourself lucky.

- Prioritize your effort. Spend time on the important aspects; more than likely, these are the 

hard parts. If you don't have fundamentals or infrastructure correct, brilliant bells and whistles 

will be irrelevant.

- Don't be a slave to history. Don't let existing code dictate future code. All code can be

replaced if it is no longer appropriate. Even within one program, don't let what you've already

done constrain what you do next—be ready to refactor (see Refactoring). This decision may 

impact the project schedule. The assumption is that the impact will be less than the cost of 

not making the change.

  

Algorithm Speed

The O() notation is a mathematical way of dealing with approximations. When we write that a 

particular sort routine sorts n records in O(n

2

) time, we are simply saying that the worst-case time 

taken will vary as the square of n. Double the number of records, and the time will increase roughly 

fourfold. 

  

If you're not sure how long your code will take, or how much memory it will use, try running it, varying 

the input record count or whatever is likely to impact the runtime. Then plot the results. You should 

soon get a good idea of the shape of the curve. Is it curving upward, a straight line, or flattening off as 

the input size increases? Three or four points should give you an idea.

Also consider just what you're doing in the code itself. A simple O(n

2

) loop may well perform better 

that a complex, O(n lg(n)) one for smaller values of n, particularly if the O(n lg(n)) algorithm has an 

expensive inner loop.

  

Refactoring

  

Rather than construction, software is more like 

gardening—it is more organic than concrete. 

  

When you come across a stumbling block because the code doesn't quite fit anymore, or you notice 

two things that should really be merged, or anything else at all strikes you as being "wrong," don't 

hesitate to change it There's no time like the present. Any number of things may cause code to qualify 

for refactoring:

- Duplication. You've discovered a violation of the DRY principle (The Evils of Duplication).

- Nonorthogonal design. You've discovered some code or design that could be made more

orthogonal (Orthogonality).

- Outdated knowledge. Things change, requirements drift, and your knowledge of the

problem increases. Code needs to keep up.

- Performance. You need to move functionality from one area of the system to another to

improve performance.

  

Refactor Early, Refactor Often

  

1. Don't try to refactor and add functionality at the same time.

2.Make sure you have good tests before you begin refactoring. Run the tests as often as 

possible. That way you will know quickly if your changes have broken anything.

3. Take short, deliberate steps: move a field from one class to another, fuse two similar methods 

into a superclass. Refactoring often involves making many localized changes that result in a 

larger-scale change. If you keep your steps small, and test after each step, you will avoid 

prolonged debugging.

  

Code That's Easy to Test

  

A software unit test is code that exercises a module. Typically, the unit test will establish some kind of 

artificial environment, then invoke routines in the module being tested. It then checks the results that 

are returned, either against known values or against the results from previous runs of the same test 

(regression testing).

  

We like to think of unit testing as testing against contract (see Design by Contract). We want to write 

test cases that ensure that a given unit honors its contract. This will tell us two things: whether the 

code meet the contract, and whether the contract means what we think it means. We want to test that 

the module delivers the functionality it promises, over a wide range of test cases and boundary 

conditions.

  

When you design a module, or even a single routine, you should design both its contract and the code 

to test that contract. By designing code to pass a test and fulfill its contract, you may well consider 

boundary conditions and other issues that wouldn't occur to you otherwise. There's no better way to fix 

errors than by avoiding them in the first place. In fact, by building the tests before you implement the 

code, you get to try out the interface before you commit to it.

  

Because we usually write a lot of test code, and do a lot of testing, we'll make life easier on ourselves 

and develop a standard testing harness for the project.

  

A test harness can handle common operations such as logging status, analyzing output for expected 

results, and selecting and running the tests. Harnesses may be GUI driven, may be written in the 

same target language as the rest of the project, or may be implemented as a combination of makefiles

and Perl scripts. 

  

Regardless of the technology you decide to use, test harnesses should include the following 

capabilities:

- A standard way to specify setup and cleanup

- A method for selecting individual tests or all available tests

- A means of analyzing output for expected (or unexpected) results

- A standardized form of failure reporting

  

Test Your Software, or Your Users Will

  

The Requirements Pit

  

 "Gathering"

implies that the requirements are already there—you need merely find them, place them in your

basket, and be merrily on your way.

It doesn't quite work that way. Requirements rarely lie on the surface. Normally, they're buried deep 

beneath layers of assumptions, misconceptions, and politics.

  

The simple answer is that a requirement is a statement of something that needs to be accomplished. 

Good requirements might include the following:

- An employee record may be viewed only by a nominated group of people.

- The cylinder-head temperature must not exceed the critical value, which varies by engine.

- The editor will highlight keywords, which will be selected depending on the type of file being 

edited.

  

The first statement in the list above may have been stated by the users as "Only an employee's 

supervisors and the personnel department may view that employee's records." Is this statement truly a 

requirement? Perhaps today, but it embeds business policy in an absolute statement. Policies change 

regularly, so we probably don't want to hardwire them into our requirements. Our recommendation is 

to document these policies separately from the requirement, and hyperlink the two. Make the 

requirement the general statement, and give the developers the policy information as an example of 

the type of thing they'll need to support in the implementation. Eventually, policy may end up as 

metadata in the application.

This is a relatively subtle distinction, but it's one that will have profound implications for the developers. 

If the requirement is stated as "Only personnel can view an employee record," the developer may end 

up coding an explicit test every time the application accesses these files. However, if the statement is 

"Only authorized users may access an employee record," the developer will probably design and 

implement some kind of access control system. When policy changes (and it will), only the metadata 

for that system will need to be updated. In fact, gathering requirements in this way naturally leads you 

to a system that is well factored to support metadata.

  

There's a simple technique for getting inside your users' requirements that isn't used often enough: 

become a user. Are you writing a system for the help desk? Spend a couple of days monitoring the 

phones with an experienced support person. Are you automating a manual stock control system? 

Work in the warehouse for a week.

[1]

 As well as giving you insight into how the system will really be 

used, you'd be amazed at how the request "May I sit in for a week while you do your job?" helps build 

trust and establishes a basis for communication with your users. Just remember not to get in the way!

  

So you are sitting down with the users and prying genuine requirements from them. You come across

a few likely scenarios that describe what the application needs to do. Ever the professional, you want

to write these down and publish a document that everyone can use as a basis for discussions—the

developers, the end users, and the project sponsors.

That's a pretty wide audience.

  

<Images in PG 247 e 248>

  

Just One More Wafer-Thin Mint…

  

Unfortunately, not many projects seem to track requirements actively. This means that they have no

way to report on changes of scope—who requested a feature, who approved it, total number of

requests approved, and so on.

The key to managing growth of requirements is to point out each new feature's impact on the schedule 

to the project sponsors. When the project is a year late from initial estimates and accusations start 

flying, it can be helpful to have an accurate, complete picture of how, and when, requirements growth 

occurred.

  

Solving Impossible Puzzles

  

The key to solving puzzles is both to recognize the constraints placed on you and to recognize the 

degrees of freedom you do have, for in those you'll find your solution. This is why some puzzles are so 

effective; you may dismiss potential solutions too readily.

  

When faced with an intractable problem, enumerate all the possible avenues you have before you. 

Don't dismiss anything, no matter how unusable or stupid it sounds. Now go through the list and 

explain why a certain path cannot be taken. Are you sure? Can you prove it?

Consider the Trojan horse—a novel solution to an intractable problem. How do you get troops into a

walled city without being discovered? You can bet that "through the front door" was initially dismissed

as suicide.

  

Should We Use Formal Methods?

  

Absolutely. But always remember that formal development methods are just one more tool in the

toolbox. If, after careful analysis, you feel you need to use a formal method, then embrace it—but

remember who is in charge. Never become a slave to a methodology: circles and arrows make poor

masters. Pragmatic Programmers look at methodologies critically, then extract the best from each and

meld them into a set of working practices that gets better each month. This is crucial. You should work

constantly to refine and improve your processes. Never accept the rigid confines of a methodology as

the limits of your world.

  

Testing the Tests

  

After you have written a test to detect a particular bug, cause the bug deliberately and 

make sure the test complains. This ensures that the test will catch the bug if it happens for 

real.

  

It's All Writing

  

There are basically two kinds of documentation produced for a project: internal and

external. Internal documentation includes source code comments, design and test

documents, and so on. External documentation is anything shipped or published to the

outside world, such as user manuals. But regardless of the intended audience, or the role

of the writer (developer or technical writer), all documentation is a mirror of the code. If

there's a discrepancy, the code is what matters—for better or worse.

  

Comments

  

We like to see a simple module-level header comment, comments for significant data and 

type declarations, and a brief per-class and per-method header, describing how the 

function is used and anything that it does that is not obvious.

Variable names, of course, should be well chosen and meaningful.

  

One of the most important pieces of information that should appear in the source file is the

author's name—not necessarily who edited the file last, but the owner. Attaching

responsibility and accountability to source code does wonders in keeping people honest

  

The extra mole

  

Give them that little bit more than they were expecting. The extra bit of effort it requires to 

add some user-oriented feature to the system will pay for itself time and time again in 

goodwill.

Listen to your users as the project progresses for clues about what features would really 

delight them. Some things you can add relatively easily that look good to the average user 

include:

- Balloon or ToolTip help

- Keyboard shortcuts

- A quick reference guide as a supplement to the user's manual

- Colorization

- Log file analyzers

- Automated installation

- Tools for checking the integrity of the system

- The ability to run multiple versions of the system for training

- A splash screen customized for their organization

  

Sign your work

  

We want to see pride of ownership. "I wrote this, and I stand behind my work." Your 

signature should come to be recognized as an indicator of quality. People should see your 

name on a piece of code and expect it to be solid, well written, tested, and documented. A 

really professional job. Written by a real professional.

A Pragmatic Programmer.

**