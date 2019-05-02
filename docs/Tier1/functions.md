# Functions

A function is a reusable piece or block of code that performs a specific action. Functions can either return values when called or can simply perform an operation without returning any value.

> **Tips**: PHP has over 700 functions built in that perform different tasks.

## Advantages

- **Better code organization** – functions allow us to group blocks of related code that perform a specific task together.  
- **Reusability** – once defined, a function can be called by a number of scripts in our PHP files. This saves us time of reinventing the wheel when we want to perform some routine tasks such as connecting to the database.  
- **Easy maintenance** – updates to the system only need to be made in one place.  

### Closure Class

Class used to represent anonymous functions.

Anonymous functions, implemented in PHP 5.3, yield objects of this type. This fact used to be considered an implementation detail, but it can now be relied upon. Starting with PHP 5.4, this class has methods that allow further control of the anonymous function after it has been created.

```php
<?php
// Normal function
function powe($x) {
    return $x * 2;
}

// Anonymous function
function($x) {
    return $x * 2;
}
```

#### Closure class shape

```php
<?php

Closure {
    /* Methods */
    private __construct ( void )

    public static bind ( Closure $closure , object $newthis [, mixed $newscope = "static" ] ) : Closure

    public bindTo ( object $newthis [, mixed $newscope = "static" ] ) : Closure

    public call ( object $newthis [, mixed $... ] ) : mixed

    public static fromCallable ( callable $callable ) : Closure
}
```

### Variable Funtions

PHP supports the concept of variable functions. This means that if a variable name has parentheses appended to it, PHP will look for a function with the same name as whatever the variable evaluates to, and will attempt to execute it.

```php
<?php
function noArgument() {
    echo "I have no argument attached";
}

function singleArgument($arg = '')
{
    echo "I have only one argument attached";
}

$noArgumentFunction = 'noArgument';
$noArgumentFunction(); // This calls noArgument()

$singleArgumentFunction = 'singleArgument';
$singleArgumentFunction('test');  // This calls singleArgument('test')
```

### Context of $this

**$this** is a pseudo-variable (also a reserved keyword) which is only available inside methods. And, it refers to the object of the current method.

```php
<?php

class Car {
    private $model;

    /**
     * @param string $model
     *
     * @return self
     */
    public function setModel(string $model): self
    {
        $this->model = $model;

        return $this;
    }
}
```

### Difference between $this and self

Use \$this to refer to the current object and self to refer to the current class. In other words, use \$this for non-static members, use self::$member for static members.

```php
<?php

<?php
class Person {
    private $name = 'Roberto Rielo';
    private static $age = 27;

    public function __construct() {
        echo 'Name: '. $this->name . ' - Age: ' . self::$age;
    }
}

new Person(); // will print: Name: Roberto Rielo - Age: 27
?>
```

### Documentation

- [Functional Programming](https://phptherightway.com/pages/Functional-Programming.html)

- [Anonymous Functions Official Documentation](https://php.net/functions.anonymous)
  
- [Variable Functions](https://www.php.net/manual/es/functions.variable-functions.php)

- [Use $this inside a Closure](https://softonsofa.com/php-how-to-use-this-in-closure-context-matters/) 