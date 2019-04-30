# Scope Resolution Operator

This operator is represented by **::** - two colons next to each other. It is used in object-oriented programming when you want to be specific about what kind of function you are calling. It allows access to static, constant, and overridden properties or methods of a class.

This is in contrast the (**“->”**) operator which allows you to access a property or method in an instantiated class.

```php
<?php

class Person {
    const STATUS = 'Active';

    private $status;
    private $firstName;
    private $lastName;

    public function __construct(string $firstName, string $lastName)
    {
      // Calling a constant
      $this->status = self::STATUS;
      $this->fistName = $firstName;
      $this->lastName = $lastName;
    }

    public static function createFromArray(array $personData): void
    {
      return new self($personData['firstName'], $personData['lastName']);
    }
}

// Calling static property
echo Person::STATUS; // will print Active
echo Person->STATUS; // Parse error

// Calling static method
Person::createFromArray(['firstName' => 'Roberto', 'lastName' => 'Rielo']);
```

## Late Static Binding

Late static binding allows to reference the called class in the context of static inheritance by introducing a keyword that references the class that was initially called at runtime. It was decided not to introduce a new keyword, but rather use static that was already reserved.

```php
<?php

    class Car
    {
        public static function run(): string
        {
            return static::getName();
        }

        private static function getName(): string
        {
            return 'Car';
        }
    }

    class Toyota extends Car
    {
        public static function getName(): string
        {
            return 'Toyota';
        }
    }

    echo Car::run(); // will print Car
    echo Toyota::run(); // will print Toyota
?>
```

## Difference Between self and static

```php
class A {
    public static function getSelf()
    {
        return new self();
    }

    public static function getStatic()
     {
        return new static();
    }
}

class B extends A {}

echo get_class(B::getSelf());  // A
echo get_class(B::getStatic()); // B
echo get_class(A::getSelf()); // A
echo get_class(A::getStatic()); // A
```

### Documentation

* [Official Documentation](https://php.net/manual/en/language.oop5.late-static-bindings.php)

* [PHP self vs static](https://www.programmerinterview.com/index.php/php-questions/php-self-vs-static/)