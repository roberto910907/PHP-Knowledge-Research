# Errors and Exceptions

Before PHP7, errors were treated like functions instead of like Exceptions. That was the reason why it was so difficult to deal with errors when trying to solve the error by continuing the code execution with a temporal solution or another way to allow the scripts to finish their execution.

After PHP, all errors are treated like Exceptions which means that we can write a catch block to try to provide a solution to the error or log the issue to a file for example. So we can create a mechanism to handle uncaught exceptions.

### Main Error Levels

* **E_ERROR**: atal run-time errors. Execution of the script is halted
* **E_WARNING**: Non-fatal run-time errors. Execution of the script is not halted
* **E_PARSE**: Compile-time parse errors. Parse errors should only be generated by the parser.
* **E_NOTICE**: Run-time notices. The script found something that might be an error, but could also happen when running a script normally
* **E_CORE_ERROR**: Fatal errors that occur during PHP's initial start-up.
* **E_CORE_WARNING**: Non-fatal run-time errors. This occurs during PHP's initial start-up.

### Exceptions Structure

* **Try**:  this means that if the exception does not trigger, the code will just execute normally but if the exception triggers then it will call “thrown” exception

* **Throw**: every time an exception has been triggered, a “throw” exception must be paired with at least one “catch”

* **Catch**:  this block of code should retrieve an exception and create an object including the exception information.

```php
<?php

$file = 'fakeLocation/fakeFile.php'

try { // throw errors in the try-block
  if(!file_exists($file)) {
    // if an error occurs we can throw an exception
    throw new Exception(sprintf('Cannot find the file "%s".', $file));
  }
}
catch(Exception $e) { // catch the throws in the catch-block
    // do something with the exception object, eg. display its message
    echo 'Error message: ' . $e->getMessage();
}
```

### Error Hierarchy

* **Throwable**
  * **Error**
    * ArithmeticError
    * DivisionByZeroError
  * **AssertionError**
  * **CompileError**
    * ParseError
  * **TypeError**
  * **ArgumentCountError**
  * **Exception**

### Built-in Exceptions

1. [BadFunctionCallException](https://www.php.net/manual/en/class.badfunctioncallexception.php)
2. [BadMethodCallException](https://www.php.net/manual/en/class.badmethodcallexception.php)
3. [DomainException](https://www.php.net/manual/en/class.domainexception.php)
4. [InvalidArgumentException](https://www.php.net/manual/en/class.invalidargumentexception.php)
5. [LengthException](https://www.php.net/manual/en/class.lengthexception.php)
6. [LogicException](https://www.php.net/manual/en/class.logicexception.php)
7. [OutOfBoundsException](https://www.php.net/manual/en/class.outofboundsexception.php)
8. [OutOfRangeException](https://www.php.net/manual/en/class.outofrangeexception.php)
9. [OverflowException](https://www.php.net/manual/en/class.overflowexception.php)
10. [RangeException](https://www.php.net/manual/en/class.rangeexception.php)
11. [RuntimeException](https://www.php.net/manual/en/class.runtimeexception.php)
12. [UnderflowException](https://www.php.net/manual/en/class.underflowexception.php)
13. [UnexpectedValueException](https://www.php.net/manual/en/class.unexpectedvalueexception.php)

### Documentation

* [Erros Official Documentation](https://www.php.net/manual/en/language.errors.php7.php)
  
* [Exception Handling](https://www.tutorialspoint.com/php/php_error_handling.htm)

* [Try-Catch Basis](https://stackify.com/php-try-catch-php-exception-tutorial/)