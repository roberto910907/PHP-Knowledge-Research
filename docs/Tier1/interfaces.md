# Built-in Interfaces

PHP provides a set of built-in interfaces which allows us to solve some common problems such as serialize objects, traverse arrays or throw exceptions.

### Main Interfaces

1. [Traversable](https://www.php.net/manual/en/class.traversable.php)
2. [Iterator](https://www.php.net/manual/en/class.iterator.php)
3. [IteratorAggregate](https://www.php.net/manual/en/class.iteratoraggregate.php)
4. [Throwable](https://www.php.net/manual/en/class.throwable.php)
5. [ArrayAccess](https://www.php.net/manual/en/class.arrayaccess.php)
6. [Serializable](https://www.php.net/manual/en/class.serializable.php)
7. [Closure](https://www.php.net/manual/en/class.closure.php)
8. [Generator](https://www.php.net/manual/en/class.generator.php)

### Traversable

Traversable interface is an abstract interface and it cannot be used alone. It is used to check whether a class is traversable using foreach. The traversable interface has no methods defined in it.

```php
<?php

interface Spam extends \Traversable
{
    // ...
}

final class Ham implements \IteratorAggregate, Spam
{
    public function getIterator()
    {
        return new \ArrayIterator(range(1, 10));
    }
}
```

### Iterator

Collections are an awesome way to organize your previously no-named array. There is a couple of reasons why you should use iterators. One of reason stays for behavior, you can specify exact behavior on standard calls such as next, current, valid etc. Other reason could be that you want to ensure that collection contains an only specific type of an object.

```php
<?php

class UsersCollection implements \IteratorAggregate
{
    /** @var array */
    private $users = [];

    public function getIterator() : UserIterator
    {
        return new UserIterator($this);
    }

    public function getUser($position)
    {
        if (isset($this->users[$position])) {
            return $this->users[$position];
        }

        return null;
    }

    public function count() : int
    {
        return count($this->users);
    }

    public function addUser(User $users)
    {
        $this->users[] = $users;
    }
}

// Create an Iterator for User
class UserIterator implements \Iterator
{
    /** @var int */
    private $position = 0;

    /** @var UsersCollection */
    private $userCollection;

    public function __construct(UsersCollection $userCollection)
    {
        $this->userCollection = $userCollection;
    }

    public function current() : User
    {
        return $this->userCollection->getUser($this->position);
    }

    public function next()
    {
        $this->position++;
    }

    public function key() : int
    {
        return $this->position;
    }

    public function valid() : bool
    {
        return !is_null($this->userCollection->getUser($this->position));
    }

    public function rewind()
    {
        $this->position = 0;
    }
}
```

### Documentation

* [Give the traversable interface some love](https://webmozart.io/blog/2012/10/07/give-the-traversable-interface-some-love/)
  
* [Iterator List](https://www.php.net/manual/en/spl.iterators.php)

* [Modern PHP Iterator](https://www.startutorial.com/articles/view/modern-php-developer-iterator)