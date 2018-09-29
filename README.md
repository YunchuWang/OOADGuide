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

* Assertions are checks that are placed within your code to assess whether a class's internal state is consistent with its specification.  Assertions allow you to discover issues with your code, prior to deploying it to users.