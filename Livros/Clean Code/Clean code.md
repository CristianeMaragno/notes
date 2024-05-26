
The 5S philosophy comprises these concepts:

• Seiri, or organization (think “sort” in English). Knowing where things are—using approaches such as suitable naming—is crucial. You think naming identifiers isn’t important? Read on in the following chapters.

• Seiton, or tidiness (think “systematize” in English). There is an old American saying: A place for everything, and everything in its place. A piece of code should be where you expect to find it—and, if not, you should re-factor to get it there.

• Seiso, or cleaning (think “shine” in English): Keep the workplace free of hanging wires, grease, scraps, and waste. What do the authors here say about littering your code with comments and commented-out code lines that capture history or wishes for the future? Get rid of them.

• Seiketsu, or standardization: The group agrees about how to keep the workplace clean. Do you think this book says anything about having a consistent coding style and set of practices within the group? Where do those standards come from? Read on.

• Shutsuke, or discipline (self-discipline). This means having the discipline to follow the practices and to frequently reflect on one’s work and be willing to change.
  

In code, mercilessly. You can improve yet one level further, as the TPM movement innovated over 50 years ago: build machines that are more maintainable in the first place. Making your code readable is as important as making it executable.

We abandon our code early, not because it is done, but because our value system focuses more on outward appearance than on the substance of what we deliver

There are two parts to learning craftsmanship: knowledge and work. You must gain the knowledge of principles, patterns, practices, and heuristics that a craftsman knows, and you must also grind that knowledge into your fingers, eyes, and gut by working hard and practicing.
  
Bad code: Every change they make to the code breaks two or three other parts of the code. No change is trivial. Every addition or modification to the system requires that the tangles, twists, and knots be “understood” so that more tangles, twists, and knots can be added.

Over time the mess becomes so big and so deep and so tall, they can not clean it up. There is no way at all.

Most managers want the truth, even when they don’t act like it. Most managers want good code, even when they are obsessing about the schedule. They may defend the schedule and requirements with passion; but that’s their job. It’s your job to defend the code with equal passion. To drive this point home, what if you were a doctor and had a patient who demanded that you stop all the silly hand-washing in preparation for surgery because it was taking too much time? Clearly the patient is the boss; and yet the doctor should absolutely refuse to comply. Why? Because the doctor knows more than the patient about the risks of disease and infection. It would be unprofessional (never mind criminal) for the doctor to comply with the patient. So too it is unprofessional for programmers to bend to the will of managers who don’t understand the risks of making messes.

Bjarne closes with the assertion that clean code does one thing well. It is no accident that there are so many principles of software design that can be boiled down to this simple admonition. Writer after writer has tried to communicate this thought. Bad code tries to do too much, it has muddled intent and ambiguity of purpose. Clean code is focused. Each function, each class, each module exposes a single-minded attitude that remains entirely undistracted, and unpolluted, by the surrounding details.

  
Our code should be matter-of-fact as opposed to speculative.
It should contain only what is necessary. Our readers should perceive us to have been
decisive.

  
Dave asserts that clean code makes it easy for other people to enhance it. This may seem obvious, but it can-not be overemphasized. There is, after all, a difference between code that is easy to read and code that is easy to change
  

Clean code is code that has been taken care of. Someone has taken the time to keep it simple and orderly. They have paid appropriate attention to details. They have cared.


I focus mostly on duplication. When the same thing is done over and over, it’s a sign that there is an idea in our mind that is not well represented in the code. I try to figure out what it is. Then I try to express that idea more clearly. Expressiveness to me includes meaningful names, and I am likely to change the names of things several times before I settle in.

  
I also look at whether an object or method is doing more than one thing. If it’s an object, it probably needs to be broken into two or more objects. If it’s a method, I will always use the Extract Method refactoring on it, resulting in one method that says more clearly what it does, and some submethods saying how it is done.

  
Reduced duplication, high expressiveness, and early building of simple abstractions.
That’s what makes clean code for me.


Indeed, the ratio of time spent reading vs. writing is well over 10:1.
We are constantly reading old code as part of the effort to write new code.
Because this ratio is so high, we want the reading of code to be easy, even if it makes the writing harder. Of course there’s no way to write code without reading it, so making it easy to read actually makes it easier to write.

  

The code has to be kept clean over time. We’ve all seen code rot and degrade as time passes. So we must take an active role in preventing this degradation. The Boy Scouts of America have a simple rule that we can apply to our profession.  Leave the campground cleaner than you found it.

If we all checked-in our code a little cleaner than when we checked it out, the code simply could not rot. The cleanup doesn’t have to be something big. Change one variable name for the better, break up one function that’s a little too large, eliminate one small bit of duplication, clean up one composite if statement.

  
**Meaningful Names**

The name of a variable, function, or class, should answer all the big questions. Itshould tell you why it exists, what it does, and how it is used. If a name requires a comment, then the name does not reveal its intent.

```
public List<int[]> getThem() {

 List<int[]> list1 = new ArrayList<int[]>();
 
 for (int[] x : theList){
   if (x[0] == 4){ 
   	 list1.add(x);
   	 return list1;
   }
 }
}


public List<int[]> getFlaggedCells() {

 List<int[]> flaggedCells = new ArrayList<int[]>();

 for (int[] cell : gameBoard){
   if (cell[STATUS_VALUE] == FLAGGED){
    flaggedCells.add(cell);
    return flaggedCells;
   }
 }
}
```

  

Programmers must avoid leaving false clues that obscure the meaning of code. We should
avoid words whose entrenched meanings vary from our intended meaning. For example,
hp, aix, and sco would be poor variable names because they are the names of Unix platforms or variants. Even if you are coding a hypotenuse and hp looks like a good abbreviation, it could be disinformative.

Do not refer to a grouping of accounts as an accountList unless it’s actually a List.
The word list means something specific to programmers. If the container holding the
accounts is not actually a List, it may lead to false conclusions.1 So accountGroup or
bunchOfAccounts or just plain accounts would be better.

Beware of using names which vary in small ways. How long does it take to spot the
subtle difference between a XYZControllerForEfficientHandlingOfStrings in one module
and, somewhere a little more distant, XYZControllerForEfficientStorageOfStrings? The
words have frightfully similar shapes.

With modern Java environments we enjoy automatic code completion. We write a few characters of a name and press some hotkey combination (if that) and are rewarded with a list of possible completions for that name. It is very helpful if names for very similar things sort together alphabetically and if the differences are very obvious, because the developer is likely to pick an object by name without seeing your copious comments or even the list of methods supplied by that class.

Noise words are another meaningless distinction. Imagine that you have a Product class. If you have another called ProductInfo or ProductData, you have made the names different without making them mean anything different. Info and Data are indistinct noise words like a, an, and the.


Note that there is nothing wrong with using prefix conventions like a and the so long
as they make a meaningful distinction. For example you might use a for all local variables
and the for all function arguments.3 The problem comes in when you decide to call a variable theZork because you already have another variable named zork.

  
If you can’t pronounce it, you can’t discuss it without sounding like an idiot. “Well, over here on the bee cee arr three cee enn tee we have a pee ess zee kyew int, see?” This matters because programming is a social activity.

  
```
class DtaRcrd102 {

  private Date genymdhms; 
  private Date modymdhms;
  private final String pszqint = "102";

  /* ... */
};

  

to


class Customer {

  private Date generationTimestamp; 
  private Date modificationTimestamp;;
  private final String recordId = "102";

 /* ... */

};

```

  

My personal preference is that single-letter names can ONLY be used as local variables inside short methods. The length of a name should correspond to the size of its scope If a variable or constant might be seen or used in multiple places in a body of code, it is imperative to give it a search-friendly name.

Encoding type or scope information into names simply adds an extra burden of deciphering.
You also don’t need to prefix member variables with m_ anymore. Your classes and functions should be small enough that you don’t need them. Besides, people quickly learn to ignore the prefix (or suffix) to see the meaningful part of the name.

**Class Names**

Classes and objects should have noun or noun phrase names like Customer, WikiPage, Account, and AddressParser. Avoid words like Manager, Processor, Data, or Info in the name of a class. A class name should not be a verb.

**Method Names**

Methods should have verb or verb phrase names like postPayment, deletePage, or save.
Accessors, mutators, and predicates should be named for their value and prefixed with get,
set, and is according to the javabean standard.

```
string name = employee.getName();

customer.setName("mike");

if (paycheck.isPosted())...

```

  

If names are too clever, they will be memorable only to people who share the author’s sense of humor, and only as long as these people remember the joke. Will they know what the function named HolyHandGrenade is supposed to do? Sure, it’s cute, but maybe in this case DeleteItems might be a better name.

Choose clarity over entertainment value.

Pick one word for one abstract concept and stick with it. For instance, it’s confusing to
have fetch, retrieve, and get as equivalent methods of different classes. How do you
remember which method name goes with which class?

If you follow the “one word per concept” rule, you could end up with many classes that have, for example, an add method. As long as the parameter lists and return values of the various add methods are semantically equivalent, all is well.

However one might decide to use the word add for “consistency” when he or she is not in fact adding in the same sense.

Remember that the people who read your code will be programmers. So go ahead and use
computer science (CS) terms, algorithm names, pattern names, math terms, and so forth. It
is not wise to draw every name from the problem domain because we don’t want our coworkers to have to run back and forth to the customer asking what every name means when they already know the concept by a different name when there is no “programmer-eese” for what you’re doing, use the name from the problem domain.


There are a few names which are meaningful in and of themselves—most are not. Instead, you need to place names in context for your reader by enclosing them in well-named classes, functions, or namespaces. When all else fails, then prefixing the name may be necessary as a last resort.

Imagine that you have variables named firstName, lastName, street, houseNumber, city,
state, and zipcode. Taken together it’s pretty clear that they form an address. But what if
you just saw the state variable being used alone in a method? Would you automatically infer that it was part of an address? You can add context by using prefixes: addrFirstName, addrLastName, addrState, and so on. At least readers will understand that these variables are part of a larger structure. Of course, a better solution is to create a class named Address. Then, even the compiler knows that the variables belong to a bigger concept.


Shorter names are generally better than longer ones, so long as they are clear. Add no more context to a name than is necessary. The names accountAddress and customerAddress are fine names for instances of the class Address but could be poor names for classes. Address is a fine name for a class. If I need to differentiate between MAC addresses, port addresses, and Web addresses, I might consider PostalAddress, MAC, and URI. The resulting names are more precise, which is the point of all naming.

  

#### Functions

Functions are the first line of organization in any program. The first rule of functions is that they should be small.  Every function in this pro-gram was just two, or three, or four lines long. Each was transparently obvious. Each told a story. And each led you to the next in a compelling order. That’s how short your functions should be!

```
public static String renderPageWithSetupsAndTeardowns(

 PageData pageData, boolean isSuite) throws Exception {
 
 if (isTestPage(pageData)){
   includeSetupAndTeardownPages(pageData, isSuite);
   return pageData.getHtml();
 }
}
```

  

#### Blocks and Indenting

This implies that the blocks within if statements, else statements, while statements, and so on should be one line long. Probably that line should be a function call. Not only does this keep the enclosing function small, but it also adds documentary value because the function called within the block can have a nicely descriptive name.

This also implies that functions should not be large enough to hold nested structures.
Therefore, the indent level of a function should not be greater than one or two. This, of course, makes the functions easier to read and understand.

FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL.
THEY SHOULD DO IT ONLY.

If a function does only those steps that are one level below the stated name of the function, then the function is doing one thing. After all, the reason we write functions is to decompose a larger concept (in other words, the name of the function) into a set of steps at
the next level of abstraction.


In order to make sure our functions are doing “one thing,” we need to make sure that the
statements within our function are all at the same level of abstraction. It is easy to see how
Listing 3-1 violates this rule. There are concepts in there that are at a very high level of abstraction, such as getHtml(); others that are at an intermediate level of abstraction, such
as: String pagePathName = PathParser.render(pagePath); and still others that are remarkably low level, such as: .append("\n").

Mixing levels of abstraction within a function is always confusing.

We want every function to be followed by those at the next level of abstraction so that we can read the program, descending one level of abstraction at a time as we read down the list of functions. I call this The Stepdown Rule.

To say this differently, we want to be able to read the program as though it were a set of TO paragraphs, each of which is describing the current level of abstraction and referencing subsequent TO paragraphs at the next level down. 

To include the setups and teardowns, we include setups, then we include the test page content, and then we include the teardowns.

To include the setups, we include the suite setup if this is a suite, then we include the regular setup.

To include the suite setup, we search the parent hierarchy for the “SuiteSetUp” page and add an include statement with the path of that page.

To search the parent. . .

My general rule for switch statements is that they can be tolerated if they appear only once, are used to create polymorphic objects, and are hidden behind an inheritance relationship so that the rest of the system can’t see them. Of course every circumstance is unique, and there are times when I violate one or more parts of that rule.

  
The smaller and more focused a function is, the easier it is to choose a descriptive name.

Don’t be afraid to make a name long. A long descriptive name is better than a short enigmatic name. A long descriptive name is better than a long descriptive comment.

Don’t be afraid to spend time choosing a name. Indeed, you should try several different names and read the code with each in place. Modern IDEs like Eclipse or IntelliJ make it trivial to change names.

Choosing descriptive names will clarify the design of the module in your mind and help you to improve it. It is not at all uncommon that hunting for a good name results in a favorable restructuring of the code. 

Be consistent in your names. Use the same phrases, nouns, and verbs in the function
names you choose for your modules. Consider, for example, the names includeSetupAndTeardownPages, includeSetupPages, includeSuiteSetupPage, and includeSetupPage.

We could extract the if statement into a function named includeSetupsAndTeardownsIfTestPage, but that simply restates the code without changing the level of abstraction.

So, another way to know that a function is doing more than “one thing” is if you can extract another function from it with a name that is not merely a restatement of its implementation


#### Function Arguments

The ideal number of arguments for a function is zero (niladic). Next comes one (monadic), followed closely by two (dyadic). Three arguments (triadic) should be avoided where possible. More than three (polyadic) requires very special justification—and then shouldn’t be used anyway.

Arguments are even harder from a testing point of view. Imagine the difficulty of writing all the test cases to ensure that all the various combinations of arguments work properly.

There are two very common reasons to pass a single argument into a function. You may be
asking a question about that argument, as in boolean fileExists(“MyFile”). Or you may be
operating on that argument, transforming it into something else and returning it. For example, InputStream fileOpen(“MyFile”) transforms a file name String into an InputStream return value. These two uses are what readers expect when they see a function. You should choose names that make the distinction clear, and always use the two forms in a consistent context.

Flag arguments are ugly. Passing a boolean into a function is a truly terrible practice. It
immediately complicates the signature of the method, loudly proclaiming that this function
does more than one thing. It does one thing if the flag is true and another if the flag is false!


A function with two arguments is harder to understand than a monadic function. For example, writeField(name) is easier to understand than writeField(output-Stream, name).

There are times, of course, where two arguments are appropriate. For example,
Point p = new Point(0,0); is perfectly reasonable. Cartesian points naturally take two arguments.

Even obvious dyadic functions like assertEquals(expected, actual) are problematic.

How many times have you put the actual where the expected should be? The two arguments have no natural ordering.


Functions that take three arguments are significantly harder to understand than dyads. The
issues of ordering, pausing, and ignoring are more than doubled. I suggest you think very
carefully before creating a triad.

  
When a function seems to need more than two or three arguments, it is likely that some of
those arguments ought to be wrapped into a class of their own. Consider, for example, the
difference between the two following declarations:

Circle makeCircle(double x, double y, double radius);

Circle makeCircle(Point center, double radius);

Argument list

Functions that take variable arguments can be monads, dyads, or even triads. But it would be a mistake to give them more arguments than that.

void monad(Integer... args);

void dyad(String name, Integer... args);

void triad(String name, int count, Integer... args);

  
Choosing good names for a function can go a long way toward explaining the intent of
the function and the order and intent of the arguments. In the case of a monad, the function and argument should form a very nice verb/noun pair. For example, write(name) is very evocative. Whatever this “name” thing is, it is being “written.” An even better name might be writeField(name), which tells us that the “name” thing is a “field.”

This last is an example of the keyword form of a function name. Using this form we encode the names of the arguments into the function name. For example, assertEquals might be better written as assertExpectedEqualsActual(expected, actual). This strongly mitigates the problem of having to remember the ordering of the arguments.

```
public class UserValidator {

 private Cryptographer cryptographer;
 
 public boolean checkPassword(String userName, String password) {
 
   User user = UserGateway.findByName(userName);

   if (user != User.NULL) {
    String codedPhrase = user.getPhraseEncodedByPassword();
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

  

The side effect is the call to Session.initialize(), of course. The checkPassword function, by its name, says that it checks the password. The name does not imply that it initializes the session. So a caller who believes what the name of the function says runs the risk of erasing the existing session data when he or she decides to check the validity of the
user.

Temporal couplings are confusing, especially when hidden as a side effect. If you must have a temporal coupling, you should make it clear in the name of the function. In this case we might rename the function checkPasswordAndInitializeSession, though that certainly violates “Do one thing.”

  
In general output arguments should be avoided. If your function must change the state of something, have it change the state of its owning object.


Functions should either do something or answer something, but not both. Either your function should change the state of an object, or it should return some information about
that object. Doing both often leads to confusion.

  
```
if (set("username", "unclebob"))...

if (attributeExists("username")) {
	setAttribute("username", "unclebob");

... }
```

  
Prefer Exceptions to Returning Error Codes

```
if (deletePage(page) == E_OK) {

	if (registry.deleteReference(page.name) == E_OK) {
		if (configKeys.deleteKey(page.name.makeKey()) == E_OK){
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

  
try {
	deletePage(page);
	registry.deleteReference(page.name);
	configKeys.deleteKey(page.name.makeKey());
}
catch (Exception e) {
	logger.log(e.getMessage());
}
```
  

When I write functions, they come out long and complicated. They have lots of indenting and nested loops. They have long argument lists. The names are arbitrary, and there is duplicated code. But I also have a suite of unit tests that cover every one of those clumsy lines of code. 

So then I massage and refine that code, splitting out functions, changing names, eliminating duplication. I shrink the methods and reorder them. Sometimes I break out whole classes, all the while keeping the tests passing.

  

**Comments**

“Don’t comment bad code—rewrite it.”

Nothing can be quite so helpful as a well-placed comment. Nothing can clutter up a module more than frivolous dogmatic comments. Nothing can be quite so damaging as an old crufty comment that propagates lies and misinformation.

The proper use of comments is to compensate for our failure to express ourself in code. Note that I used the word failure. I meant it. Comments are always failures. We must have them because we cannot always figure out how to express ourselves without them, but their use is not a cause for celebration.

So when you find yourself in a position where you need to write a comment, think it through and see whether there isn’t some way to turn the tables and express yourself in code. Every time you express yourself in code, you should pat yourself on the back. Every time you write a comment, you should grimace and feel the failure of your ability of expression.

Code changes and evolves. Chunks of it move from here to there. Those chunks bifurcate and reproduce and come together again to form chimeras. Unfortunately the comments don’t always follow them—can’t always follow them. And all too often the comments get separated from the code they describe and become orphaned blurbs of everdecreasing accuracy.

Inaccurate comments are far worse than no comments at all. They delude and mislead.
They set expectations that will never be fulfilled. They lay down old rules that need not, or should not, be followed any longer.

Truth can only be found in one place: the code. Only the code can truly tell you what it does. It is the only source of truly accurate information. Therefore, though comments are sometimes necessary, we will expend significant energy to minimize them.

Clear and expressive code with few comments is far superior to cluttered and complex code with lots of comments. Rather than spend your time writing the comments that explain the mess you’ve made, spend it cleaning that mess.

  

Which would you rather see? This:

```
// Check to see if the employee is eligible for full benefits

if ((employee.flags & HOURLY_FLAG) && (employee.age > 65)) 
```

Or this?
```
if (employee.isEligibleForFullBenefits())
```

It takes only a few seconds of thought to explain most of your intent in code. In many cases it’s simply a matter of creating a function that says the same thing as the comment you want to write.


Good Comments

Sometimes our corporate coding standards force us to write certain comments for legal
reasons. For example, copyright and authorship statements are necessary and reasonable things to put into a comment at the start of each source file.

// format matched kk:mm:ss EEE, MMM dd, yyyy

Pattern timeMatcher = Pattern.compile(

 "\\d*:\\d*:\\d* \\w*, \\w* \\d*, \\d*");

In this case the comment lets us know that the regular expression is intended to match a time and date that were formatted with the SimpleDateFormat.format function using the specified format string.

Sometimes it is just helpful to translate the meaning of some obscure argument or return value into something that’s readable.

assertTrue(a.compareTo(a) == 0); // a == a

Sometimes it is useful to warn other programmers about certain consequences

TODOs are jobs that the programmer thinks should be done, but for some reason can’t do at the moment. It might be a reminder to delete a deprecated feature or a plea for someone else to look at a problem. It might be a request for someone else to think of a better name or a reminder to make a change that is dependent on a planned event. Whatever else a TODO might be, it is not an excuse to leave bad code in the system.


It is sometimes reasonable to leave “To do” notes in the form of //TODO comments. In the following case, the TODO comment explains why the function has a degenerate implementation and what that function’s future should be. 

//TODO-MdM these are not needed

// We expect this to go away when we do the checkout model

protected VersionInfo makeVersion() throws Exception{
	return null;
}

A comment may be used to amplify the importance of something that may otherwise seem inconsequential.

  
Bad Comments

Most comments fall into this category
Any comment that forces you to look in another module for the meaning of that comment has failed to communicate to you and is not worth the bits it consumes.

Redundante comments
```
// Utility method that returns when this.closed is true. Throws an exception

// if the timeout is reached.

public synchronized void waitForClose(final long timeoutMillis) throws Exception{
	if(!closed){
		wait(timeoutMillis);
		if(!closed) throw new Exception("MockResponseSender could not be closed");
	}
}
```

  

What purpose does this comment serve? It’s certainly not more informative than the code. It does not justify the code, or provide intent or rationale. It is not easier to read than the code. Indeed, it is less precise than the code and entices the reader to accept that lack of precision in lieu of true understanding.

Don’t Use a Comment When You Can Use a Function or a Variable
Consider the following stretch of code:

```
// does the module from the global list <mod> depend on the

// subsystem we are part of?

if (smodule.getDependSubsystems().contains(subSysMod.getSubSystem()))

This could be rephrased without the comment as

ArrayList moduleDependees = smodule.getDependSubsystems();

String ourSubSystem = subSysMod.getSubSystem();

if (moduleDependees.contains(ourSubSystem))
```
  

Few practices are as odious as commenting-out code. Don’t do this!

InputStreamResponse response = new InputStreamResponse();
response.setBody(formatter.getResultStream(), formatter.getByteCount());

// InputStream resultsStream = formatter.getResultStream();
// StreamReader reader = new StreamReader(resultsStream);
// response.setContent(reader.read(formatter.getByteCount()));

Others who see that commented-out code won’t have the courage to delete it. They’ll think it is there for a reason and is too important to delete. So commented-out code gathers like dregs at the bottom of a bad bottle of wine.

Why are those two lines of code commented? Are they important? Were they left as reminders for some imminent change? Or are they just cruft that someone commented-out years ago and has simply not bothered to clean up.

If you must write a comment, then make sure it describes the code it appears near. Don’t offer system wide information in the context of a local comment.

Don’t put interesting historical discussions or irrelevant descriptions of details into your comments.

The connection between a comment and the code it describes should be obvious. If you are
going to the trouble to write a comment, then at least you’d like the reader to be able to look at the comment and the code and understand what the comment is talking about. 

Formatting

When people look under the hood, we want them to be impressed with the neatness, consistency, and attention to detail that they perceive. We want them to be struck by the
orderliness. We want their eyebrows to rise as they scroll through the modules. We want them to perceive that professionals have been at work. If instead they see a scrambled mass of code that looks like it was written by a bevy of drunken sailors, then they are likely to conclude that the same inattention to detail pervades every other aspect of the
project.
  
You should take care that your code is nicely formatted. You should choose a set of simple rules that govern the format of your code, and then you should consistently apply those rules. If you are working on a team, then the team should agree to a single set of formatting rules and all members should comply. It helps to have an automated tool that can apply those formatting rules for you.
  
We would like a source file to be like a newspaper article. The name should be simple
but explanatory. The name, by itself, should be sufficient to tell us whether we are in the right module or not. The topmost parts of the source file should provide the high-level concepts and algorithms. Detail should increase as we move downward, until at the end we find the lowest level functions and details in the source file.

A newspaper is composed of many articles; most are very small. Some are a bit larger. Very few contain as much text as a page can hold. This makes the newspaper usable. If the newspaper were just one long story containing a disorganized agglomeration of facts, dates, and names, then we simply would not read it.

There are blank lines that separate the package declaration, the import(s), and each of the functions. This extremely simple rule has a profound effect on the visual layout of the code. Each blank line is a visual cue that identifies a new and separate concept.

  
If openness separates concepts, then vertical density implies close association. So lines of code that are tightly related should appear vertically dense.

Concepts that are closely related should be kept vertically close to each other. Clearly this rule doesn’t work for concepts that belong in separate files. But then closely related concepts should not be separated into different files unless you have a very good reason. Indeed, this is one of the reasons that protected variables should be avoided. 

For those concepts that are so closely related that they belong in the same source file, their vertical separation should be a measure of how important each is to the understandability of the other

  
Variables should be declared as close to their usage as possible. Because our functions are very short, local variables should appear a the top of each function

Instance variables, on the other hand, should be declared at the top of the class. This should not increase the vertical distance of these variables, because in a well-designed class, they are used by many, if not all, of the methods of the class.

PAREI AQUI
Dependent Functions. If one function calls another, they should be vertically close,

and the caller should be above the callee, if at all possible. This gives the program a natural

flow. If the convention is followed reliably, readers will be able to trust that function defini-

tions will follow shortly after their use.

  

Conceptual Affinity.

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

} ...

These functions have a strong conceptual affinity because they share a common naming

scheme and perform variations of the same basic task. The fact that they call each other is

secondary. Even if they didn’t, they would still want to be close together.

  

Horizontal Formatting

How wide should a line be? This suggests that we should strive to keep our lines short. The old Hollerith limit of

80 is a bit arbitrary, and I’m not opposed to lines edging out to 100 or even 120. But

beyond that is probably just careless.

  

Every programmer has his own

favorite formatting rules, but if he works

in a team, then the team rules. 

A team of developers should agree

upon a single formatting style, and then

every member of that team should use

that style. We want the software to have a

consistent style. We don’t want it to appear to have been written by a bunch of disagreeing

individuals.

  

Objects and Data Structures

  

Reler capítulo, não entendi

  

Error Handling

  

Many code bases are completely dominated by error handling. When I say dominated, I don’t mean that error handling is all that they do. I mean that it is nearly impossible to see what the code does because of all of the scattered error handling. Error handling is important, but if it obscures logic, it’s wrong

  

public class DeviceController {

 ...

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

 logger.log("Device suspended. Unable to shut down");

 }

 } else {

 logger.log("Invalid handle for: " + DEV1.toString());

 }

 }

 ...

}

  

Better

  

public class DeviceController {

 ...

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

 ...

 throw new DeviceShutDownError("Invalid handle for: " + id.toString());

 ...

 }

 ...

}

  

In a way, try blocks are like transactions. Your catch has to leave your program in a

consistent state, no matter what happens in the try. For this reason it is good practice to

start with a try-catch-finally statement when you are writing code that could throw

exceptions. This helps you define what the user of that code should expect, no matter what

goes wrong with the code that is executed in the try.

  

Try to write tests that force exceptions, and then add behavior to your handler to sat-

isfy your tests. This will cause you to build the transaction scope of the try block first and

will help you maintain the transaction nature of that scope.

  

Try to write tests that force exceptions, and then add behavior to your handler to sat-

isfy your tests. This will cause you to build the transaction scope of the try block first and

will help you maintain the transaction nature of that scope.

  

Each exception that you throw should provide enough context to determine the source and

location of an error. In Java, you can get a stack trace from any exception; however, a stack

trace can’t tell you the intent of the operation that failed. 

Create informative error messages and pass them along with your exceptions. Men-

tion the operation that failed and the type of failure. If you are logging in your application,

pass along enough information to be able to log the error in your catch.

  

There are many ways to classify errors. We can classify them by their source: Did they

come from one component or another? Or their type: Are they device failures, network

failures, or programming errors? However, when we define exception classes in an appli-

cation, our most important concern should be how they are caught.

  

LocalPort port = new LocalPort(12);

 try {

 port.open();

 } catch (PortDeviceFailure e) {

 reportError(e);

 logger.log(e.getMessage(), e);

 } finally {

 …

 }

Our LocalPort class is just a simple wrapper that catches and translates exceptions

thrown by the ACMEPort class:

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

 …

}

Wrappers like the one we defined for ACMEPort can be very useful. In fact, wrapping

third-party APIs is a best practice. When you wrap a third-party API, you minimize your

dependencies upon it: You can choose to move to a different library in the future without

much penalty. Wrapping also makes it easier to mock out third-party calls when you are

testing your own code.

  

Often a single exception class is fine for a particular area of code. The information

sent with the exception can distinguish the errors. Use different classes only if there are

times when you want to catch one exception and allow the other one to pass through.

  

If you follow the advice in the preceding

sections, you’ll end up with a good amount

of separation between your business logic

and your error handling. The bulk of your

code will start to look like a clean

unadorned algorithm. However, the pro-

cess of doing this pushes error detection

to the edges of your program. You wrap

external APIs so that you can throw your

own exceptions, and you define a handler above your code so that you can deal with any

aborted computation. Most of the time this is a great approach, but there are some times

when you may not want to abort.

  

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

If you work in a code base with code like this, it might not look all that bad to you, but it is

bad! When we return null, we are essentially creating work for ourselves and foisting

problems upon our callers. All it takes is one missing null check to send an application

spinning out of control

  

It’s easy to say that the problem with the code above is that it is missing a null check,

but in actuality, the problem is that it has too many. If you are tempted to return null from

a method, consider throwing an exception or returning a SPECIAL CASE object instead. If

you are calling a null-returning method from a third-party API, consider wrapping that

method with a method that either throws an exception or returns a special case object.

  

Right now, getEmployees can return null, but does it have to? If we change getEmployee so

that it returns an empty list, we can clean up the code

  

Returning null from methods is bad, but passing null into methods is worse. Unless you

are working with an API which expects you to pass null, you should avoid passing null in

your code whenever possible

  

In most programming languages there is no good way to deal with a null that is

passed by a caller accidentally. Because this is the case, the rational approach is to forbid

passing null by default. When you do, you can code with the knowledge that a null in an

argument list is an indication of a problem, and end up with far fewer careless mistakes.

  

Clean code is readable, but it must also be robust. These are not conflicting goals. We can

write robust clean code if we see error handling as a separate concern, something that is

viewable independently of our main logic. To the degree that we are able to do that, we can

reason about it independently, and we can make great strides in the maintainability of our

code.

  

Boundaries

  

We seldom control all the software in our systems. Sometimes we buy third-party pack-

ages or use open source. Other times we depend on teams in our own company to produce

components or subsystems for us. Somehow we must cleanly integrate this foreign code with our own. In this chapter we look at practices and techniques to keep the boundaries of

our software clean.

  

Passing an instance of Map<Sensor> liberally around the system means that there will

be a lot of places to fix if the interface to Map ever changes. You might think such a change

to be unlikely, but remember that it changed when generics support was added in Java 5.

Indeed, we’ve seen systems that are inhibited from using generics because of the sheer

magnitude of changes needed to make up for the liberal use of Maps.

A cleaner way to use Map might look like the following. No user of Sensors would care

one bit if generics were used or not. That choice has become (and always should be) an

implementation detail.

public class Sensors {

private Map sensors = new HashMap();

public Sensor getById(String id) {

return (Sensor) sensors.get(id);

}

//snip

}

  

The interface at the boundary (Map) is hidden. It is able to evolve with very little impact on

the rest of the application. The use of generics is no longer a big issue because the casting

and type management is handled inside the Sensors class.

  

We are not suggesting that every use of Map be encapsulated in this form. Rather, we

are advising you not to pass Maps (or any other interface at a boundary) around your

system. If you use a boundary interface like Map, keep it inside the class, or close family

of classes, where it is used. Avoid returning it from, or accepting it as an argument to,

public APIs.

  

Suppose it is not clear how to use our third-party library. We might spend a day or two

(or more) reading the documentation and deciding how we are going to use it. Then we

might write our code to use the third-party code and see whether it does what we think. We

would not be surprised to find ourselves bogged down in long debugging sessions trying to

figure out whether the bugs we are experiencing are in our code or theirs. 

Learning the third-party code is hard. Integrating the third-party code is hard too.

Doing both at the same time is doubly hard. What if we took a different approach? Instead

of experimenting and trying out the new stuff in our production code, we could write some

tests to explore our understanding of the third-party code. Jim Newkirk calls such tests

learning tests.1

In learning tests we call the third-party API, as we expect to use it in our application.

We’re essentially doing controlled experiments that check our understanding of that API.

The tests focus on what we want out of the API.

  

Let’s say we want to use the apache log4j package rather than our own custom-built log-

ger. We download it and open the introductory documentation page. Without too much

reading we write our first test case, expecting it to write “hello” to the console.

  

When we run it, the logger produces an error that tells us we need something called an

Appender. After a little more reading we find that there is a ConsoleAppender. So we create a

ConsoleAppender and see whether we have unlocked the secrets of logging to the console

  

This time we find that the Appender has no output stream. Odd—it seems logical that it’d

have one. After a little help from Google, we try the following

  

That worked; a log message that includes “hello” came out on the console! It seems odd

that we have to tell the ConsoleAppender that it writes to the console. 

Interestingly enough, when we remove the ConsoleAppender.SystemOut argument, we

see that “hello” is still printed. But when we take out the PatternLayout, it once again com-

plains about the lack of an output stream. This is very strange behavior. 

Looking a little more carefully at the documentation, we see that the default

ConsoleAppender constructor is “unconfigured,” which does not seem too obvious or useful.

This feels like a bug, or at least an inconsistency, in log4j.

A bit more googling, reading, and testing, and we eventually wind up with Listing 8-1.

We’ve discovered a great deal about the way that log4j works, and we’ve encoded that

knowledge into a set of simple unit tests.

  

Now we know how to get a simple console logger initialized, and we can encapsulate

that knowledge into our own logger class so that the rest of our application is isolated from

the log4j boundary interface.

  

Not only are learning tests free, they have a positive return on investment. When there

are new releases of the third-party package, we run the learning tests to see whether there

are behavioral differences. 

Learning tests verify that the third-party packages we are using work the way we

expect them to. Once integrated, there are no guarantees that the third-party code will stay

compatible with our needs. The original authors will have pressures to change their code to

meet new needs of their own. They will fix bugs and add new capabilities. With each

release comes new risk. If the third-party package changes in some way incompatible with

our tests, we will find out right away.

  

Code at the boundaries needs clear separation and tests that define expectations. We

should avoid letting too much of our code know about the third-party particulars. It’s better

to depend on something you control than on something you don’t control, lest it end up

controlling you. 

We manage third-party boundaries by having very few places in the code that refer to

them. We may wrap them as we did with Map, or we may use an ADAPTER to convert from

our perfect interface to the provided interface. Either way our code speaks to us better,

promotes internally consistent usage across the boundary, and has fewer maintenance

points when the third-party code changes.

  

Unit Tests

  

By now everyone knows that TDD(test driven dev) asks us to write unit tests first, before we write produc-

tion code. But that rule is just the tip of the iceberg. Consider the following three laws:1

First Law You may not write production code until you have written a failing unit test.

Second Law You may not write more of a unit test than is sufficient to fail, and not com-

piling is failing.

Third Law You may not write more production code than is sufficient to pass the cur-

rently failing test.

  

These three laws lock you into a cycle that is perhaps thirty seconds long. The tests

and the production code are written together, with the tests just a few seconds ahead of the

production code.

If we work this way, we will write dozens of tests every day, hundreds of tests every

month, and thousands of tests every year. If we work this way, those tests will cover virtu-

ally all of our production code. The sheer bulk of those tests, which can rival the size of the

production code itself, can present a daunting management problem.

  

The problem is that tests must change as the production code

evolves. The dirtier the tests, the harder they are to change. The more tangled the test code,

the more likely it is that you will spend more time cramming new tests into the suite than it

takes to write the new production code. As you modify the production code, old tests start

to fail, and the mess in the test code makes it hard to get those tests to pass again. So the

tests become viewed as an ever-increasing liability.

  

The moral of the story is simple: Test code is just as important as production code. It

is not a second-class citizen. It requires thought, design, and care. It must be kept as clean

as production code.

  

It is unit tests

that keep our code flexible, maintainable, and reusable. The reason is simple. If you have

tests, you do not fear making changes to the code! Without tests every change is a possible

bug. No matter how flexible your architecture is, no matter how nicely partitioned your

design, without tests you will be reluctant to make changes because of the fear that you

will introduce undetected bugs.

  

So having an automated suite of unit tests that cover the production code is the key to

keeping your design and architecture as clean as possible. Tests enable all the -ilities,

because tests enable change.

  

What makes a clean test? Three things. Readability, readability, and readability. Read-

ability is perhaps even more important in unit tests than it is in production code. What

makes tests readable? The same thing that makes all code readable: clarity, simplicity,

and density of expression. In a test you want to say a lot with as few expressions as

possible.

  

Rather than using the APIs that programmers use to manipulate the sys-

tem, we build up a set of functions and utilities that make use of those APIs and that

make the tests more convenient to write and easier to read. These functions and utilities

become a specialized API used by the tests. They are a testing language that program-

mers use to help themselves to write their tests and to help those who must read those

tests later on.

  

There are things that you might never do in a

production environment that are perfectly fine in a test environment. Usually they involve

issues of memory or CPU efficiency. But they never involve issues of cleanliness.

  

There is a school of thought4 that says that every test function in a JUnit test should have one

and only one assert statement. This rule may seem draconian, but the advantage can be seen

in Listing 9-5. Those tests come to a single conclusion that is quick and easy to understand.

  

I think the single assert rule is a good guideline.7 I usually try to create a domain-

specific testing language that supports it, as in Listing 9-5. But I am not afraid to put

more than one assert in a test. I think the best thing we can say is that the number of

asserts in a test ought to be minimized.

  

Perhaps a better rule is that we want to test a single concept in each test function.

  

So it’s not the multiple asserts in each section of Listing 9-8 that causes the problem.

Rather it is the fact that there is more than one concept being tested. So probably the best

rule is that you should minimize the number of asserts per concept and test just one con-

cept per test function.

  

FIRSTClean tests follow five other rules that form the above acronym:

Fast Tests should be fast. They should run quickly. When tests run slow, you won’t want

to run them frequently. If you don’t run them frequently, you won’t find problems early

enough to fix them easily. You won’t feel as free to clean up the code. Eventually the code

will begin to rot.

Independent Tests should not depend on each other. One test should not set up the condi-

tions for the next test. You should be able to run each test independently and run the tests in

any order you like. When tests depend on each other, then the first one to fail causes a cas-

cade of downstream failures, making diagnosis difficult and hiding downstream defects.

Repeatable Tests should be repeatable in any environment. You should be able to run the

tests in the production environment, in the QA environment, and on your laptop while

riding home on the train without a network. If your tests aren’t repeatable in any environ-

ment, then you’ll always have an excuse for why they fail. You’ll also find yourself unable

to run the tests when the environment isn’t available.

Self-Validating The tests should have a boolean output. Either they pass or fail. You

should not have to read through a log file to tell whether the tests pass. You should not have

to manually compare two different text files to see whether the tests pass. If the tests aren’t

self-validating, then failure can become subjective and running the tests can require a long

manual evaluation.

Timely The tests need to be written in a timely fashion. Unit tests should be written just

before the production code that makes them pass. If you write tests after the production

code, then you may find the production code to be hard to test. You may decide that some

production code is too hard to test. You may not design the production code to be testable.

  

Classes

  

We have

delved into proper composition of functions and how they interrelate. But for all the atten-

tion to the expressiveness of code statements and the functions they comprise, we still

don’t have clean code until we’ve paid attention to higher levels of code organization.

  

a class should begin with a list of variables. Pub-

lic static constants, if any, should come first. Then private static variables, followed by pri-

vate instance variables. There is seldom a good reason to have a public variable.

Public functions should follow the list of variables. We like to put the private utilities

called by a public function right after the public function itself. This follows the stepdown

rule and helps the program read like a newspaper article.

  

We like to keep our variables and utility functions private, but we’re not fanatic about it. Loosening encapsulation is always a last resort.

  

The first rule of classes is that they should be small. With functions we measured size by counting physical lines. With classes we use a

different measure. We count responsibilities. The name of a class should describe what responsibilities it fulfills. In fact, naming

is probably the first way of helping determine class size. If we cannot derive a concise

name for a class, then it’s likely too large. The more ambiguous the class name, the more

likely it has too many responsibilities. For example, class names including weasel words

like Processor or Manager or Super often hint at unfortunate aggregation of

responsibilities.

We should also be able to write a brief description of the class in about 25 words,

without using the words “if,” “and,” “or,” or “but.”

  

The Single Responsibility Principle (SRP)2 states that a class or module should have one,

and only one, reason to change. Trying to identify responsibilities (reasons to change) often helps us recognize and

create better abstractions in our code.

  

The problem is that too many of us think that we are done once the program works.

We fail to switch to the other concern of organization and cleanliness. We move on to the

next problem rather than going back and breaking the overstuffed classes into decoupled

units with single responsibilities.

  

Classes should have a small number of instance variables. Each of the methods of a class

should manipulate one or more of those variables. In general the more variables a method

manipulates the more cohesive that method is to its class. Consider the implementation of a Stack in Listing 10-4. This is a very cohesive class.

Of the three methods only size() fails to use both the variables.

The strategy of keeping functions small and keeping parameter lists short can some-

times lead to a proliferation of instance variables that are used by a subset of methods.

When this happens, it almost always means that there is at least one other class trying to get out of the larger class. You should try to separate the variables and methods into two or

more classes such that the new classes are more cohesive.

  

The change was made by writing a test suite that verified the precise behavior of the

first program. Then a myriad of tiny little changes were made, one at a time. After each

change the program was executed to ensure that the behavior had not changed. One tiny

step after another, the first program was cleaned up and transformed into the second.

  

Private method behavior that applies only to a small subset of a class can be a useful

heuristic for spotting potential areas for improvement. However, the primary spur for tak-

ing action should be system change itself. If the Sql class is deemed logically complete,

then we need not worry about separating the responsibilities. If we won’t need update

functionality for the foreseeable future, then we should leave Sql alone. But as soon as we

find ourselves opening up a class, we should consider fixing our design.

  

abstract public class Sql {

 public Sql(String table, Column[] columns)

 abstract public String generate();

}

public class CreateSql extends Sql {

 public CreateSql(String table, Column[] columns)

 @Override public String generate()

}

public class SelectSql extends Sql {

 public SelectSql(String table, Column[] columns)

 @Override public String generate()

}

public class InsertSql extends Sql {

 public InsertSql(String table, Column[] columns, Object[] fields)

 @Override public String generate()

 private String valuesList(Object[] fields, final Column[] columns)

}

public class SelectWithCriteriaSql extends Sql {

 public SelectWithCriteriaSql(

 String table, Column[] columns, Criteria criteria)

 @Override public String generate()

}

public class SelectWithMatchSql extends Sql {

 public SelectWithMatchSql(

 String table, Column[] columns, Column column, String pattern)

 @Override public String generate()

}

public class FindByKeySql extends Sql

 public FindByKeySql(

 String table, Column[] columns, String keyColumn, String keyValue)

 @Override public String generate()

}

public class PreparedInsertSql extends Sql {

 public PreparedInsertSql(String table, Column[] columns)

 @Override public String generate() {

 private String placeholderList(Column[] columns)

}

public class Where {

 public Where(String criteria)

 public String generate()

}

  

Our restructured Sql logic represents the best of all worlds. It supports the SRP. It also

supports another key OO class design principle known as the Open-Closed Principle, or

OCP:4 Classes should be open for extension but closed for modification. Our restructured

Sql class is open to allow new functionality via subclassing, but we can make this change

while keeping every other class closed. We simply drop our UpdateSql class in place

  

We want to structure our systems so that we muck with as little as possible when we

update them with new or changed features. In an ideal system, we incorporate new fea-

tures by extending the system, not by making modifications to existing code.

  

that there are con-

crete classes, which contain implementation details (code), and abstract classes, which

represent concepts only. A client class depending upon concrete details is at risk when

those details change. We can introduce interfaces and abstract classes to help isolate the

impact of those details.

  

Systems

  

“Complexity kills. It sucks the life out of developers,

it makes products difficult to plan, build, and test.”

  

Cities also work because they have evolved appropriate levels of abstraction and mod-

ularity that make it possible for individuals and the “components” they manage to work

effectively, even without understanding the big picture.

Although software teams are often organized like that too, the systems they work on

often don’t have the same separation of concerns and levels of abstraction. Clean code

helps us achieve this at the lower levels of abstraction. In this chapter let us consider how

to stay clean at higher levels of abstraction, the system level.

  

Software systems should separate the startup process, when the application objects are

constructed and the dependencies are “wired” together, from the runtime logic that takes

over after startup

  

One way to separate construction from use is simply to move all aspects of construction to

main, or modules called by main, and to design the rest of the system assuming that all

objects have been constructed and wired up appropriately

  

A powerful mechanism for separating construction from use is Dependency Injection (DI),

the application of Inversion of Control (IoC) to dependency management.3 Inversion of

Control moves secondary responsibilities from an object to other objects that are dedicated

to the purpose, thereby supporting the Single Responsibility Principle. In the context of

dependency management, an object should not take responsibility for instantiating depen-

dencies itself. Instead, it should pass this responsibility to another “authoritative” mecha-

nism, thereby inverting the control. Because setup is a global concern, this authoritative

mechanism will usually be either the “main” routine or a special-purpose container.

  

True Dependency Injection goes one step further. The class takes no direct steps to

resolve its dependencies; it is completely passive. Instead, it provides setter methods or

constructor arguments (or both) that are used to inject the dependencies.

  

It is a myth that we can get systems “right the first time.” Instead, we should imple-

ment only today’s stories, then refactor and expand the system to implement new stories

tomorrow. This is the essence of iterative and incremental agility. Test-driven develop-

ment, refactoring, and the clean code they produce make this work at the code level.

  

Software systems are unique compared to physical systems. Their architectures can grow

incrementally, if we maintain the proper separation of concerns.

  

An optimal system architecture consists of modularized domains of concern, each of which

is implemented with Plain Old Java (or other) Objects. The different domains are inte-

grated together with minimally invasive Aspects or Aspect-like tools. This architecture can

be test-driven, just like the code.

  

Modularity and separation of concerns make decentralized management and decision

making possible. In a sufficiently large system, whether it is a city or a software project, no

one person can make all the decisions.

  

The agility provided by a POJO system with modularized concerns allows us to make opti-

mal, just-in-time decisions, based on the most recent knowledge. The complexity of these

decisions is also reduced.

  

Standards make it easier to reuse ideas and components, recruit people with relevant expe-

rience, encapsulate good ideas, and wire components together. However, the process of

creating standards can sometimes take too long for industry to wait, and some standards

lose touch with the real needs of the adopters they are intended to serve.

  

Domain-Specific Languages allow all levels of abstraction and all domains in the applica-

tion to be expressed as POJOs, from high-level policy to low-level details.

  

Ler novamente

  

Emergence

  

Getting Clean via Emergent Design

What if there were four simple rules that you could follow that would help you create good

designs as you worked? What if by following these rules you gained insights into the struc-

ture and design of your code, making it easier to apply principles such as SRP and DIP?

What if these four rules facilitated the emergence of good designs?

Many of us feel that Kent Beck’s four rules of Simple Design are of significant help in

creating well-designed software.

  

• Runs all the tests

• Contains no duplication

• Expresses the intent of the programmer

• Minimizes the number of classes and methods

The rules are given in order of importance.

  

Systems that aren’t testable

aren’t verifiable. Arguably, a system that cannot be verified should never be deployed.

Fortunately, making our systems testable pushes us toward a design where our classes

are small and single purpose. It’s just easier to test classes that conform to the SRP. The

more tests we write, the more we’ll continue to push toward things that are simpler to test.

So making sure our system is fully testable helps us create better designs.

  

Duplication manifests

itself in many forms. Lines of code that look exactly alike are, of course, duplication. And duplication can exist in other forms such as

duplication of implementation.

Duplication represents additional

work, additional risk, and additional unnecessary complexity

  

Creating a clean system requires the will to eliminate duplication, even in just a few

lines of code. For example, consider the following code:

 public void scaleToOneDimension(

 float desiredDimension, float imageDimension) {

 if (Math.abs(desiredDimension - imageDimension) < errorThreshold)

 return;

 float scalingFactor = desiredDimension / imageDimension;

 scalingFactor = (float)(Math.floor(scalingFactor * 100) * 0.01f);

 RenderedOp newImage = ImageUtilities.getScaledImage(

 image, scalingFactor, scalingFactor);

 image.dispose();

 System.gc();

 image = newImage;

 }

 public synchronized void rotate(int degrees) {

 RenderedOp newImage = ImageUtilities.getRotatedImage(

 image, degrees);

 image.dispose();

 System.gc();

 image = newImage;

 }

To keep this system clean, we should eliminate the small amount of duplication between

the scaleToOneDimension and rotate methods:

 public void scaleToOneDimension(

 float desiredDimension, float imageDimension) {

 if (Math.abs(desiredDimension - imageDimension) < errorThreshold)

 return;

 float scalingFactor = desiredDimension / imageDimension;

 scalingFactor = (float)(Math.floor(scalingFactor * 100) * 0.01f);

  

replaceImage(ImageUtilities.getScaledImage(

 image, scalingFactor, scalingFactor));

 }

 public synchronized void rotate(int degrees) {

 replaceImage(ImageUtilities.getRotatedImage(image, degrees));

 }

 private void replaceImage(RenderedOp newImage) {

 image.dispose();

 System.gc();

 image = newImage;

 }

  

But the most important way to be expressive is to try. All too often we get our code

working and then move on to the next problem without giving sufficient thought to making

that code easy for the next person to read. Remember, the most likely next person to read

the code will be you. 

So take a little pride in your workmanship. Spend a little time with each of your func-

tions and classes. Choose better names, split large functions into smaller functions, and

generally just take care of what you’ve created. Care is a precious resource.

  

High class and method counts are sometimes the result of pointless dogmatism. Con-

sider, for example, a coding standard that insists on creating an interface for each and

every class. Or consider developers who insist that fields and behavior must always be sep-

arated into data classes and behavior classes. Such dogma should be resisted and a more

pragmatic approach adopted. 

Our goal is to keep our overall system small while we are also keeping our functions

and classes small. Remember, however, that this rule is the lowest priority of the four rules

of Simple Design. So, although it’s important to keep class and function count low, it’s

more important to have tests, eliminate duplication, and express yourself.

  

Concurrency

  

For more information read chapter Concurrency and Concurrency II 

  

What is concurrent programing? Simply described, it’s when you are doing more than one thing at the same time. Not to be confused with parallelism, concurrency is when multiple sequences of operations are run in overlapping periods of time. In the realm of programming, concurrency is a pretty complex subject.

  

Concurrency is a decoupling strategy. It helps us decouple what gets done from when it

gets done. In single-threaded applications what and when are so strongly coupled that the

state of the entire application can often be determined by looking at the stack backtrace. A

programmer who debugs such a system can set a breakpoint, or a sequence of breakpoints,

and know the state of the system by which breakpoints are hit. 

Decoupling what from when can dramatically improve both the throughput and struc-

tures of an application. From a structural point of view the application looks like many lit-

tle collaborating computers rather than one big main loop. This can make the system easier

to understand and offers some powerful ways to separate concerns.

  

consider a system that handles one user at a time and requires only one second

of time per user. This system is fairly responsive for a few users, but as the number of

users increases, the system’s response time increases. No user wants to get in line

behind 150 others! We could improve the response time of this system by handling

many users concurrently.

Or consider a system that interprets large data sets but can only give a complete solu-

tion after processing all of them. Perhaps each data set could be processed on a different

computer, so that many data sets are being processed in parallel.

  

Challenges

there are many possible paths that the two threads can take through that one

line of Java code, and some of those paths generate incorrect results

  

The SRP5 states that a given method/class/component should have a single reason to

change. Concurrency design is complex enough to be a reason to change in it’s own right

and therefore deserves to be separated from the rest of the code.

  

As we saw, two threads modifying the same field of a shared object can interfere with each

other, causing unexpected behavior. One solution is to use the synchronized keyword to

protect a critical section in the code that uses the shared object. It is important to restrict

the number of such critical sections.

  

Take data encapsulation to heart; severely limit the access of any

data that may be shared.

  

If there is an easy way to avoid sharing objects, the resulting code will be far less likely

to cause problems. You might be concerned about the cost of all the extra object creation. It is

worth experimenting to find out if this is in fact a problem

  

Consider writing your threaded code such that each thread exists in its own world, sharing

no data with any other thread. Each thread processes one client request, with all of its

required data coming from an unshared source and stored as local variables.

  

Review the classes available to you. In the case of Java, become

familiar with java.util.concurrent, java.util.concurrent.atomic, java.util.concurrent.locks.

  

Avoid using more than one method on a shared object.

There will be times when you must use more than one method on a shared object.

When this is the case, there are three ways to make the code correct:

• Client-Based Locking—Have the client lock the server before calling the first 

method and make sure the lock’s extent includes code calling the last method.

• Server-Based Locking—Within the server create a method that locks the server, calls 

all the methods, and then unlocks. Have the client call the new method.

• Adapted Server—create an intermediary that performs the locking. This is an exam-

ple of server-based locking, where the original server cannot be changed.

  

Keep your synchronized sections as small as possible.

  

Think about shut-down early and get it working early. It’s going to

take longer than you expect. Review existing algorithms because this is probably harder

than you think.

  

Write tests that have the potential to expose problems and then

run them frequently, with different programatic configurations and system configurations

and load. If tests ever fail, track down the failure. Don’t ignore a failure just because the

tests pass on a subsequent run.

Treat spurious failures as candidate threading issues.

• Get your nonthreaded code working first.

• Make your threaded code pluggable.

• Make your threaded code tunable.

• Run with more threads than processors.

• Run on different platforms.

• Instrument your code to try and force failures.

  

Do not ignore system failures as one-offs. Bugs in

threaded code might exhibit their symptoms once in a thousand, or a million, executions. 

  

Do not try to chase down nonthreading bugs and threading bugs

at the same time. Make sure your code works outside of threads.

  

Make your thread-based code especially pluggable so that you

can run it in various configurations.

  

Getting the right balance of threads typically requires trial an error. Early on, find ways to

time the performance of your system under different configurations. Allow the number of threads to be easily tuned. Consider allowing it to change while the system is running.

Consider allowing self-tuning based on throughput and system utilization.

  

The more frequently your tasks swap, the more

likely you’ll encounter code that is missing a critical section or causes deadlock.

  

Run your threaded code on all target platforms early and often.

  

Use jiggling strategies to ferret out errors.

  

If you are faced with writ-

ing concurrent code, you need to write clean code with rigor or else face subtle and

infrequent failures.

First and foremost, follow the Single Responsibility Principle. Break your system into

POJOs that separate thread-aware code from thread-ignorant code.

  

Know the possible sources of concurrency issues: multiple threads operating on

shared data, or using a common resource pool. Boundary cases, such as shutting down

cleanly or finishing the iteration of a loop, can be especially thorny.

  

Successive Refinement notes

  

Let me set your mind at rest. I did not simply write this program from beginning to end in

its current form. More importantly, I am not expecting you to be able to write clean and

elegant programs in one pass. If we have learned anything over the last couple of decades,

it is that programming is a craft more than it is a science. To write clean code, you must

first write dirty code and then clean it.

  

Most freshman programmers (like most grade-schoolers) don’t follow this advice par-

ticularly well. They believe that the primary goal is to get the program working. Once it’s

“working,” they move on to the next task, leaving the “working” program in whatever state

they finally got it to “work.” Most seasoned programmers know that this is professional

suicide.

  

I hope your initial reaction to this mass of code is “I’m certainly glad he didn’t leave it

like that!” If you feel like this, then remember that’s how other people are going to feel

about code that you leave in rough-draft form. The mess built gradually. Earlier versions had not been nearly so nasty

  

However, within this code it is easy to see

the seeds of the later festering pile. It’s quite clear how this grew into the latter mess.

Notice that the latter mess has only two more argument types than this: String and

integer. The addition of just two more argument types had a massively negative impact on

the code. It converted it from something that would have been reasonably maintainable

into something that I would expect to become riddled with bugs and warts.

  

I had at least two more argument types to add, and I could tell that they would make things

much worse. If I bulldozed my way forward, I could probably get them to work, but I’d

leave behind a mess that was too large to fix. If the structure of this code was ever going to

be maintainable, now was the time to fix it.

  

One of the best ways to ruin a program is to make massive changes to its structure in the name of

improvement. Some programs never recover from such “improvements.” The problem is that

it’s very hard to get the program working the same way it worked before the “improvement.”

  

To avoid this, I use the discipline of Test-Driven Development (TDD). One of the cen-

tral doctrines of this approach is to keep the system running at all times. In other words,

using TDD, I am not allowed to make a change to the system that breaks that system.

Every change I make must keep the system working as it worked before.

To achieve this, I need a suite of automated tests that I can run on a whim and that ver-

ifies that the behavior of the system is unchanged

  

Again, these changes were made one at a time and in such a way that the tests kept

running, if not passing. When a test broke, I made sure to get it passing again before con-

tinuing with the next change.

  

The majority of the changes to the Args class were deletions. A lot of code just got

moved out of Args and put into ArgsException. Nice. We also moved all the

ArgumentMarshallers into their own files. Nicer!

Much of good software design is simply about partitioning—creating appropriate

places to put different kinds of code. This separation of concerns makes the code much

simpler to understand and maintain.

  

Smells and Heuristics

  

As I made each change, I asked myself why I made that change and then wrote the reason down here. The result is a rather long list of things that smell bad to me when I read

code.

  

(Muita coisa aqui está repetida de outros capítulos, então eu vou colocar apenas o que traz uma informação nova)

  

Enviroment

  

You should

not have to search near and far for all the various little extra JARs, XML files, and other

artifacts that the system requires. You should be able to check out the system with one sim-

ple command and then issue one other simple command to build it.

  

You should be able to run all the unit tests with just one command. In the best case you

can run all the tests by clicking on one button in your IDE.

  

General

  

The ideal is for a source file to contain one, and only one, language. Realistically, we will probably have to use more than one. But we should take pains to minimize both the number and extent of extra languages in our source files.

  

Following “The Principle of Least Surprise,” any function or class should implement the behaviors that another programmer could reasonably expect. When an obvious behavior is not implemented, readers and users of the code can no longer depend on their intuition about function names. They lose their trust in the original author and must fall back on reading the details of the code.

  

There is no replacement for due diligence. Every boundary condition, every corner

case, every quirk and exception represents something that can confound an elegant and intuitive algorithm. Don’t rely on your intuition. Look for every boundary condition and

write a test for it.

  

Turning off certain compiler warnings (or all warnings!)

may help you get the build to succeed, but at the risk of endless debugging sessions. Turn-

ing off failing tests and telling yourself you’ll get them to pass later is as bad as pretending

your credit cards are free money

  

Good software developers learn to limit what they expose at the interfaces of their

classes and modules. The fewer methods a class has, the better. The fewer variables a func-

tion knows about, the better. The fewer instance variables a class has, the better. 

Hide your data. Hide your utility functions. Hide your constants and your temporaries.

Don’t create classes with lots of methods or lots of instance variables. Don’t create lots of

protected variables and functions for your subclasses. Concentrate on keeping interfaces

very tight and very small. Help keep coupling low by limiting information.

  

Things that don’t depend upon each other should not be artificially coupled. For example,

general enums should not be contained within more specific classes because this forces the

whole application to know about these more specific classes. The same goes for general

purpose static functions being declared in specific classes.

  

Kent Beck wrote about this in his great book Smalltalk Best Practice Patterns8 and again

more recently in his equally great book Implementation Patterns.

9

 One of the more power-

ful ways to make a program readable is to break the calculations up into intermediate val-

ues that are held in variables with meaningful names.

Matcher match = headerPattern.matcher(line);

if(match.find())

{

 String key = match.group(1);

 String value = match.group(2);

 headers.put(key.toLowerCase(), value);

}

  

First, most people use switch statements because it’s the obvious brute force solution,

not because it’s the right solution for the situation. So this heuristic is here to remind us to

consider polymorphism before using a switch. 

Second, the cases where functions are more volatile than types are relatively rare. So

every switch statement should be suspect. 

I use the following “ONE SWITCH” rule: There may be no more than one switch state-

ment for a given type of selection. The cases in that switch statement must create polymor-

phic objects that take the place of other such switch statements in the rest of the system.

  

Expecting the first match to be the only match to a query is probably naive. Using floating

point numbers to represent currency is almost criminal. Avoiding locks and/or transaction

management because you don’t think concurrent update is likely is lazy at best. Declaring

a variable to be an ArrayList when a List will due is overly constraining. Making all vari-

ables protected by default is not constraining enough. 

When you make a decision in your code, make sure you make it precisely. Know why

you have made it and how you will deal with any exceptions. Don’t be lazy about the pre-

cision of your decisions. If you decide to call a function that might return null, make sure

you check for null. If you query for what you think is the only record in the database,

make sure your code checks to be sure there aren’t others. If you need to deal with cur-

rency, use integers11 and deal with rounding appropriately. If there is the possibility of

concurrent update, make sure you implement some kind of locking mechanism. 

Ambiguities and imprecision in code are either a result of disagreements or laziness.

In either case they should be eliminated.

  

Enforce design decisions with structure over convention. Naming conventions are good,

but they are inferior to structures that force compliance. For example, switch/cases with

nicely named enumerations are inferior to base classes with abstract methods. No one is

forced to implement the switch/case statement the same way each time; but the base

classes do enforce that concrete classes have all abstract methods implemented.

  

Negatives are just a bit harder to understand than positives. So, when possible, condition-

als should be expressed as positives. For example:

if (buffer.shouldCompact())

is preferable to

if (!buffer.shouldNotCompact())

  

Temporal couplings are often necessary, but you should not hide the coupling. Structure

the arguments of your functions such that the order in which they should be called is obvi-

ous. The order of the three functions is important. You must saturate the gradient before you

can reticulate the splines, and only then can you dive for the moog. Unfortunately, the code

does not enforce this temporal coupling. Another programmer could call reticulate-

Splines before saturateGradient was called, leading to an UnsaturatedGradientException.

A better solution is:

public class MoogDiver {

 Gradient gradient;

 List<Spline> splines;

 public void dive(String reason) {

 Gradient gradient = saturateGradient();

 List<Spline> splines = reticulateSplines(gradient);

 diveForMoog(splines, reason);

 }

 ...

}

  

The statements within a function should all be written at the same level of abstraction,

which should be one level below the operation described by the name of the function. This

may be the hardest of these heuristics to interpret and follow.

  

Now that enums have been added to the language (Java 5), use them! Don’t keep using the

old trick of public static final ints. The meaning of ints can get lost. The meaning of

enums cannot, because they belong to an enumeration that is named.

What’s more, study the syntax for enums carefully. They can have methods and fields.

This makes them very powerful tools that allow much more expression and flexibility than

ints

  

Names should describe everything that a function, variable, or class is or does. Don’t hide

side effects with a name. Don’t use a simple verb to describe a function that does more

than just that simple action. 

This function does a bit more than get an “oos”; it creates the “oos” if it hasn’t been cre-

ated already. Thus, a better name might be createOrReturnOos.

  

How many tests should be in a test suite? Unfortunately, the metric many programmers use

is “That seems like enough.” A test suite should test everything that could possibly break.

The tests are insufficient so long as there are conditions that have not been explored by the

tests or calculations that have not been validated.

Coverage tools reports gaps in your testing strategy. They make it easy to find modules,

classes, and functions that are insufficiently tested. Most IDEs give you a visual indication,

marking lines that are covered in green and those that are uncovered in red. This makes it

quick and easy to find if or catch statements whose bodies haven’t been checked.

  

Sometimes you can diagnose a problem by finding patterns in the way the test cases fail.

This is another argument for making the test cases as complete as possible. Complete test

cases, ordered in a reasonable way, expose patterns. 

As a simple example, suppose you noticed that all tests with an input larger than five

characters failed? Or what if any test that passed a negative number into the second argu-

ment of a function failed? Sometimes just seeing the pattern of red and green on the test

report is enough to spark the “Aha!” that leads to the solution

**