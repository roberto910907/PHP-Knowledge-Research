# Advanced Knowledge of Magic Functions

In this section we will be covering some other magic functions that are used very often in our daily work and also by the tools we rely on.

- **__call()**
- **__callStatic()**
- **__invoke()**
- **__autoload()**

### __call and __callStatic

rovides developers with possibility to react on static method calls even if that methods don't exist or aren't accessible from outside of the class (being protected). This is useful for dynamic, generic code generation.

```php
<?php

class Person
{
    public function __call(string $name, array $arguments)
    {
        echo "Called a non-existent method {$name}";
    }

    public static function __callStatic(string $name, array $arguments)
    {
        echo "Called a non-existent static method {$name}";
    }
}


$person = new Person();
$person->getName(); // Called a non-existent method getName

Person::createNew(); // Called a non-existent static method createNew
```

### __invoke

When you try to call an object in the way of calling a function, the __ invoke() method will be called automatically.

```php
<?php

class Person
{
    public $name;

    public function __construct(string $name = "")
    {
        $this->name = $name;
    }

    public function __invoke(int $age) {
        echo "Invoke called with name {$this->name} and parameter {$age}";
    }
}

$person = new Person('John');
$person(27); // Invoke called with name John and parameter 27

call_user_func($person, 'getAge', 10); // Invoke called with name John and parameter 10
```

### __autoload

This global function is called whenever you try to create an object of a class that hasn't been defined. It takes just one parameter, which is the name of the class you have not defined. If you define an object as being from a class that PHP does not recognise, PHP will run this function, then try to re-create the object - you have a second chance to have the right class.

As a result, you can write scripts like this:

```php
<?php
    function __autoload($class) {
        print "Bad class name: $class!\n";
        include "barclass.php";
    }

    $foo = new Bar();
    $foo->wombat();
```

Here we try and create a new object of type Bar, but as you can see it does not exist. __autoload() is therefore called, with "Bar" being passed in as its first parameter. __autoload() then include() s the file barclass.php, which contains the class definition of Bar. PHP will again try and create a new Bar, and this time it will succeed, which means we can work with $foo as normal.

### Documentation

- [Magic methods in oop the definitive guide PHP](https://hackernoon.com/magic-methods-in-oop-the-definitive-guide-php-e3f8a0da278)

- [Autoload Official Documentation](https://php.net/manual/es/function.autoload.php)