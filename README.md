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
	</ul>

# JAVA TIPS
1. Protected constructor is used to call super() in subclass see https://stackoverflow.com/questions/28009016/use-of-protected-constructor
2. As it says in the link, you never have to call super(), as Java will implicitly add it. But you do have to call super(args) if you need a non-default parent constructor.
3. Constructors of superclass are not inherited by subclass. https://stackoverflow.com/questions/5193450/does-a-subclass-inherit-constructors-from-it-super-class