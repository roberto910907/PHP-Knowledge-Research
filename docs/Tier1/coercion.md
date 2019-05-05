# Type-Coercing

The lack of a specific type means that PHP operates on a “best-guess” principle where PHP converts the value of a variable to the most appropriate type for the action being carried out.

In PHP, there is no need of any type specification while PHP variable declaration. Rather, it requires only the name of the variable with its value,if any, to be assigned to them.

This means that while you’ll usually get the expected results, there are some cases where you can end up with some seemingly bizarre output.

```php
echo 'fortieth' + 7; // Outputs 7
echo '40th' + 7; // Outputs 47
```

What’s happening is that if a string starts with a number, PHP will pull it out and use it as the value for mathematical operations. Otherwise, it becomes 0

### Strict Comparison

A strict comparison is done with three equals signs (===), and it requires the two pieces of data being compared to have not only the same value, but the same type as well.

> **Tips**: You should use strict comparisons whenever possible.

```php
echo '1' == 1; // bool(TRUE)
echo '1' === 1; // bool(FALSE) first value is a string while the second one is an integer
```

### Strict Mode

There is a new feature introduced in PHP7 which allows you to force the parameters and result type for a given functions. So if this _declare_ statement is not present, PHP will try to **cast** the parameters given to the function taking into account the types in the function signature.

#### Strict Mode Disable

```php
<?php

  function AddIntAndFloat(int $a, float $b) : int
  {
      return $a + $b;
  }

  echo AddIntAndFloat(1.4,'2');
  /*
  * without strict typing, php will change float(1.4) to int(1)
  * and string('2') to float(2.0) and returns int(3)
  */  
```

#### Strict Mode Enable

```php
<?php
  declare(strict_types=1);

  function AddIntAndFloat(int $a, float $b): int
  {
      return (string) $a + $b;
  }

  echo AddIntAndFloat(1.4,'2');    
  // Fatal error: Uncaught TypeError: Argument 1 passed to AddIntAndFloat() must be of the type int, float given
  echo AddIntAndFloat(1,'2');
  // Fatal error: Uncaught TypeError: Argument 2 passed to AddIntAndFloat() must be of the type float, string given

  // Integers can be passed as float-points :
  echo AddIntAndFloat(1,1);
  // Fatal error: Uncaught TypeError: Return value of AddIntAndFloat() must be of the type integer, string returned
```

### Non-Strict Comparison

```php
echo 0 == FALSE; // bool(true)
echo 0 == 'test'; // bool(true)
echo FALSE == 'test'; // bool(false)
```

It does make sense that 0 and FALSE would be considered equal. So we’re good so far, but the number 0 and the word “test”, in pretty much every situation I can think of, should probably come back FALSE. This one’s pretty odd to have come back TRUE, but it goes back to the fact that PHP will try and convert “test” to an integer, so it becomes 0 for the comparison.

### Documentation

- [Comparison Table between strict comparison and non-strict comparison](https://medium.com/@Q2hpY2tlblB3bnk/php-type-juggling-c34a10630b10)

- [Type-coercing comparison operators](http://phpsadness.com/sad/47)

- [Type Juggling Official Documentation](https://www.php.net/manual/en/language.types.type-juggling.php)