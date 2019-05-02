# Traits

Well, a Trait is simply a class that contains methods that can be shared with many classes. All classes that use this Trait can make use of its methods. They allow developers to write methods that can be used in any number of classes, keeping your code DRY and more maintainable.

Sometimes you will need to use multiple inheritance to make your classes extend from more than one parent, but this is not currently supported by PHP. It is an addition to traditional inheritance and enables horizontal composition of behavior; that is, the application of class members without requiring inheritance

> **Tips:** It is not possible to instantiate a Trait on its own.

```php
<?php
trait Hello
{
    function sayHello() {
        echo "Hello";
    }
}

trait World
{
    function sayWorld() {
        echo "World";
    }
}

class MyWorld
{
    use Hello, World; // multiple inheritance
}

$world = new MyWorld();
echo $world->sayHello() . " " . $world->sayWorld(); // Hello World
```

### Duck-Typing

With normal typing, suitability is assumed to be determined by an object's type only. In duck typing, an object's suitability is determined by the presence of certain methods and properties (with appropriate meaning), rather than the actual type of the object.

```php
class Car
{
  public function getModel(): string
  {
     return 'Toyota';
  }
}

class Truck
{
  public function getModel(): string
  {
     return 'Volvo';
  }
}

class Dog
{
  public function getAge(): int
  {
     return 10;
  }
}

function showModel($entity): string
{
    return $entity->getModel();
}

$car = new Car();
$truck = new Truck();
$dog = new Dog();

echo showModel($car); // Toyota
echo showModel($truck); // Volvo
echo showModel($dog); // Throws an error "Call to undefined method Dog::getModel()"
```

### Monkey Patching

A monkey patch is a way to extend or modify the runtime code of dynamic languages without altering the original source code. Basically, if you use a PHP function inside a namespace, the original function will be called if an override is not defined.

```php
<?php
$str = 'mystring'; // length is 8 characters

echo "The length should be eight, but it's: " . strlen($str) . "\n"; // 6

<?php
namespace monkeypatching;

function strlen()
{
    return 6;
}

$code = file_get_contents('monkeypatched.php');
$code  = 'namespace monkeypatching; ?> ' . $code;

echo $code;
eval($code); // The length should be eight, but it's: 6
```

> **Tips:** I wouldn't recommend this method/practice when working with PHP since this infringes every single SOLID and software engineering principle. In general, methods and functions definitions are part of the mandatory global state of an application, and so once the loading phase has finished they should be immutable. This is done at the loading time, so it may be acceptable.

### Documentation

* [Official Documentation for Traits](https://www.php.net/manual/en/language.oop5.traits.php)

* [How to use traits in PHP](https://dev.to/mattsparks/how-to-use-php-traits-459m)
  
* [Monkey Patch Example](https://murze.be/monkey-patching-in-php-with-patchwork)