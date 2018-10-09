# OOADGuide
Robust Classes

* Exceptions are a way to handle exceptional scenarios that happen during execution -- they allow you to specify how to recover execution if things have started to go wrong.  Having code dedicated to handling these exceptional scenarios helps make your code more robust, because you can save it from crashing in these predicted situations. <br />
	1. Error condition should not be returned instead being thrown as exception, and let caller handle it. check https://github.com/UBCx-Software-Construction-2/robust-classes-lecture-starters.
	2. Exception can be rethrown. Exceptions can be thrown from anywhere, including inside of a catch block.
	```java
    try {
        amethod();
    } catch (Exception someException) {
        throw new OtherException();
    }
    ```
    3. Up to now we have been implementing exceptions that are noticed by the compiler -- this is why IntelliJ (or your IDE) complains when you haven't surrounded a method call with try/catch, or haven't added a potentially thrown exception to the method signature.  These are called checked exceptions, because they are checked by the compiler.
There are also unchecked exceptions.  These are exceptions that the compiler will not complain about, and which do not have to be explicitly listed in a method signature, even if the method potentially throws that exception.  
An example of an unchecked exception is an ArithmeticException -- the kind of exception you might get if you try to divide by zero.
Unchecked exceptions are used for errors that could often happen, but rarely do.  For instance, you would not want to have to try/catch every time you use division in a program.  As a corollary to that, division hardly ever produces an error -- and if it does, you can spot that during testing, and perform the necessary checks to ensure it doesn't happen again.
We can, however, catch unchecked exceptions using the try/catch mechanism, just as we would a checked exception. 
	4. A simple way to test exceptions within a JUnit test is to call a method, and then fail if the exception is caught when it shouldn't be:
	```java
	try {
	 anObject.aMethod(nonExceptionalInputs);
	} catch (SomeException e) {
	 fail("I was not expecting SomeException!");
	}
	```
	or fail if the exception is not thrown when it should have been:
	```java
	try {
	 anObject.aMethod(problematicInputs);
	 fail("I was not expecting to reach this line of code!");
	} catch (SomeException e) {
	 System.out.println("great!");
	}
	```
* Assertions are checks that are placed within your code to assess whether a class's internal state is consistent with its specification.  Assertions allow you to discover issues with your code, prior to deploying it to users.
	1. Assertions let us programmatically check what should be true at certain points in our program. Assert statements are the same as those used in tests, but they are placed within the code of our class, rather than in an external test class. Assertions help us to discover erroneous behaviour in our code.

UML:
 Please see https://courses.edx.org/courses/course-v1:UBCx+SoftConst2x+3T2017/courseware/f5b58172b82a431587a28e16e14ab6f2/04f513505e63439eb39c9fc5526dd8fa/?child=first
```
LinkedList : fast for insert O(1)
ArrayList: fast lookup O(1)
HashSet: fast lookup/insert O(1)
```
Design principles:
	<ul> 
		<li>Design principles help guide the way we create software to attain certain very important software qualities, such as maintainability, and readability.  These principles help code to age gracefully.
		<li>
		<li>
			Single Responsibility Principle indicates that each class should be centered around one cohesive concept

When adding new functionality, consider into which class it would best fit

If, over time, a class seems like it has more than one responsibility, it can be split into two separate classes
		<li>
		<li>
			Chef server should be decoupled
		<li>
		<li>
			Coupling between two classes indicates that two classes collaborate in some way.  

Inter-class coupling can be through method calls, dependencies, or by holding functionality in common that accomplishes a goal without explicitly declaring as such.

The seriousness of kinds of coupling is directly related to the propagation of changes in the system:

Low: a change in one place requires no change in a collaborating class

Medium: a change in one class does require a remote change, but the compiler warns the developer that the change is needed.  An example of this is when a checked exception is declared to be thrown, the compiler will alert the developer that it must be caught at the calling location.  Method signature changes are also checked by the compiler, as are Type changes.

High: a change in one class does require a remote change, but the collaboration will only be detected at runtime -- meaning you have to run the code to see that the change has affected other classes. 

Coupling can also be considered architecturally, where we look at the relationships between classes to see if the overall design is being maintained.
		<li>
		<li> important! for a set of objects used in different classes, it will make classes highly coupled. to reduce coupling, define the set of objects into a class and let all classes use and modify to the class therefore eliminating inconsistency.
		<li>
		<li>
		The Liskov Substitution Principle states that for a subclass to be substitutable for its superclass, the subclass cannot break the expectations that a user of the superclass would have.  Thus, it cannot reduce the service it provides, and cannot produce effects not produced in the superclass.

It formally states that 

the preconditions of a subclass’s behaviour (methods) cannot be strengthened, meaning (among other things) that a sub-method cannot accept a narrower range of inputs than the original method.

The post conditions of a sub-method cannot be weakened, meaning that the sub-method cannot have a broader range of effect than the original method.
		<li>
		<li>important see how LIV works in https://courses.edx.org/courses/course-v1:UBCx+SoftConst2x+3T2017/courseware/c6ea9f605fb74ff7ad2a1ae7ab435075/eaab8b297c4443169f034390a10e8492/?child=first
		<li>
		<li>
			If class cant have all behaviors of subclass it should not extends it.
			Two solutions : changed to association || use interface
		<li>
		<li>
			Subclass cant override variables in superclass. If you want to have different values in subclasses, you can implement getMethod!
		<li>
	</ul>

# JAVA TIPS
1. Protected constructor is used to call super() in subclass see https://stackoverflow.com/questions/28009016/use-of-protected-constructor
2. As it says in the link, you never have to call super(), as Java will implicitly add it. But you do have to call super(args) if you need a non-default parent constructor.
3. Constructors of superclass are not inherited by subclass. https://stackoverflow.com/questions/5193450/does-a-subclass-inherit-constructors-from-it-super-class