# New Features

We've seen a lot of interesting new features in the latest version of the language. Those features allows PHP developers to become more productive on our daily bais and also by adding types, we guarantee we're creating stronger and safer software programs.

These are some of the new features will be covering in this section:

- **Scalar Type Declaration**
- **Return Type Declarations**
- **Spaceship Operator**
- **Null Coalesce Operator**
- **Random Bytes**
- **Random Integers**
- **Short Closures**
- **Generators**

### Scalar Type Declaration

PHP7+ has now added Scalar type declaration for int, float, string, and boolean. Adding scalar type declaration and enabling strict requirements ensures that more correct and well-documented PHP programs can be written. It also helps you in gaining more control over your code and make the code easier to read.

```php
<?php

function multiply(int $a, int $b) {
   return $a * $b;
}

echo multiply(2, 8); // 16
echo multiply(2, "a"); // Argument 2 passed to multiply() must be of the type integer, string given
```

### Return Type Declarations

PHP7+ also supports are a Return Type Declaration. It supports all similar type arguments as a return.

```php
<?php

function multiply(int $a, int $b): int
{
   return "This will throw an error because of this string";
}

echo multiply(2, 8); // Return value of multiply() must be of the type integer, string returned
```

##### Benefits of Types

These new implementations of Scalar Type Declaration and Return Type Declaration certainly help us by making the code easier to read. With PHP7+ you get a versatile type declaration methods which makes your life easier. You can even see at the start of the function, what is required and what will be returned.

### Spaceship Operator

Spaceship Operator, also known as the Combined Comparison Operator, will compare the value on the left to the value on the right and returns 3 different values.

```php
<?php

$values = [2, 1, 3, 6, 5, 4, 7];

usort($values, function (int $a, int $b)
 {
    return ($a <=> $b);
 });
```

### Null Coalesce Operator

If it is not null it returns the left operand, otherwise, it returns the right operand.

```php
<?php

// before this feature
$result = (array_key_exist('name', $namesArray) && null !== $namesArray['name'])
    ? $namesArray['name']
    : '';

// after this feature
$result = $namesArray['name'] ?? '';
```

### Random Bytes

With random_bytes, you only supply a single argument that is the length of the random string which it will return in bytes.

```php
<?php

$randomByte = random_bytes(10); // 10 is the length in bytes

echo bin2hex($randomByte); // string(20) "5f655db3ae43c256937b"
```

### Random Integers

This function generates secure random integers. When using random_int you supply two arguments, that are min and max. Which tells the minimum and maximum numbers for the random integer.

```php
<?php

random_int(2,10); // returns a random number between 2 and 10
```

### Short Closures

Short closures allow for less verbose one-liner functions.

> **Tips**:
>
> - They can access the parent scope, there's no need for the use keyword.
>
> - $this is available just like normal closures.
>
> - Short closures may only contain one line, which is also the return statement.

```php
<?php

// before this features
array_map(function (User $user) {
    return $user->id;
}, $users)

// after this feature
array_map(fn(User $user) => $user->id, $users)
```

### Generators

Generators provide an easy way to implement simple iterators without the overhead or complexity of implementing a class that implements the Iterator interface.

```php
<?php
function nums() {
    echo "The generator has started";

    for ($i = 0; $i < 5; ++$i) {
        yield $i;
        echo "Yielded $i";
    }

    echo "The generator has ended";

   // The generator has started
   // Yielded 0
   // Yielded 1
   // Yielded 2
   // Yielded 3
   // Yielded 4
   // The generator has ended
}

foreach (nums() as $v);
```

### Documentation

- [New Features PHP7.3 Complete](https://hackernoon.com/new-features-of-php-7-3-complete-guide-49d254e43ee1)
  
- [What's New in PHP7](https://www.quora.com/Whats-new-in-PHP-7)

- [PHP 7.4 - The Future](https://stitcher.io/blog/new-in-php-74)