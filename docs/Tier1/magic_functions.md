# Magic Functions

The function names **__construct()**, **__destruct()**, **__call()**, **__callStatic()**, **__get()**, **__set()**, **__isset()**, **__unset()**, **__sleep()**, **__wakeup()**, **__toString()**, **__invoke()**, **__set_state()**, **__clone()** and **__debugInfo()** are magical in PHP classes.

#### Constructor

This method is automatically called when an object will be initialized. This allows you to provide some default values to the class attributes that you will need setted up before the object is used.

```php
class Person {
    private $firstName;
    private $lastName;

    public function __construct(string $firstName, string $lastName)
    {
        $this->firstName = $firstName;
        $this->lastName = $lastName;
    }

    public function getFullName(): string
    {
        return sprintf('%s %s', $this->firstName, $this->lastName);
    }
}

$newPerson = new Person('Roberto', 'Rielo');
echo $newPerson->getFullName(); // Roberto Rielo
```

#### Destructor

The Destructor method will be called as soon as there are no other references to a particular object, or in any order during the shutdown sequence.

> Destructor are often used for closing DB connections, eg: a Database object itself might want to close the socket it is using to communicate to the database server. Also are used for **fclose()** or **fopen()** connections.

You can see an example of using a destructor [here](https://github.com/swiftmailer/swiftmailer/blob/master/lib/classes/Swift/ByteStream/TemporaryFileByteStream.php#L36).

#### Overloading

Overloading in PHP provides means to dynamically create properties and methods. These dynamic entities are processed via magic methods one can establish in a class for various action types.