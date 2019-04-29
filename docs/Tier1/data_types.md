# Data Types

The values assigned to a PHP variable may be of different data types including simple string and numeric types to more complex data types like arrays and objects.

PHP supports total eight primitive data types: Integer, Floating point number or Float, String, Booleans, Array, Object, Resource and NULL.  

In this section we will be focus on the following types:

* **String**
* **Integer**
* **Float**
* **Boolean**
* **Array**
* **Object**
* **NULL**
* **Resource**

## String

Strings are sequences of characters, where every character is the same as a byte. A string can hold letters, numbers, and special characters and it can be as large as up to 2GB (2147483647 bytes maximum).

You can use single or doubles quotes to represent an string in PHP.

```php
<?php
$helloWorld = 'Hello World! with single quote';
echo $helloWorld;

$anotherWorld = "Another World! with double quote";
echo $anotherWorld;
?>
```

## Integer

Integers are whole numbers, without a decimal point (eg: -2, -1, 0, 1, 2). Integers can be specified in decimal (base 10), hexadecimal (base 16 - prefixed with 0x) or octal (base 8 - prefixed with 0) notation, optionally preceded by a sign (- or +).

```php
<?php
$a = 123; // decimal number
var_dump($a);
  
$b = -123; // a negative number
var_dump($b);
  
$c = 0x1A; // hexadecimal number
var_dump($c);
  
$d = 0123; // octal number
var_dump($d);
?>
```

## Float

Floating point numbers (also known as "floats", "doubles", or "real numbers") are decimal or fractional numbers

```php
<?php
$a = 1.234;
var_dump($a); // 1.234
  
$b = 10.2e3;
var_dump($b); // 10200
  
$c = 4E-10;
var_dump($c); // 4.0E-10
?>
```

## Boolean

Booleans are like a switch it has only two possible values either 1 (true) or 0 (false).

> **Tip:** Even when you can use **TRUE/FALSE** or **true/false** indistinctly, it is recommended to use always all lowercases.

```php
<?php
// Assign the value TRUE to a variable
$showErrors = true;
$showTips = false;

var_dump($showErrors); // bool(true)
var_dump($showTips); // bool(false)
?>
```

## Array

Arrays are complex variables that allow us to store more than one value or a group of values under a single variable name. It is useful to aggregate a series of related items together.

> **Tip:** You can use either **long** --> array() or **short** --> [] syntax, but it is recommended to use _short syntax_ when configuring your [PSR](https://www.php-fig.org/psr/) rules.

```php
<?php
// Unidimensional array using long syntax
$colors = array("Red", "Green", "Blue");
var_dump($colors);

// Multidimensional array using short syntax
$colorCodes = [
    "Red" => "#ff0000",
    "Green" => "#00ff00",
    "Blue" => "#0000ff"
];
var_dump($colorCodes);
?>
```

## Object

An object is a data type that not only allows storing data but also information on, how to process that data. An object is a specific instance of a class which serve as templates for objects. Objects are created based on this template via the new keyword.

```php
<?php
// Class definition
class Person {
    // properties
    private $name = "Roberto Rielo";

    // methods
    public function getName(): string
    {
        return $this->name;
    }
}

// Create object from Person class
$person = new Person();
var_dump($person->getName());
?>
```

## NULL

The special NULL value is used to represent empty variables in PHP. A variable of type NULL is a variable without any data. NULL is the only possible value of type null.

> **Tip:** Even when you can use **NULL** or **null** indistinctly, it is recommended to use always all lowercases.

```php
<?php
$a = NULL;
var_dump($a); // NULL

$b = "Hello World!";
$b = null;
var_dump($b); // NULL
?>
```

## Resource

A resource is a special variable, holding a reference to an external resource.  
Resource variables typically hold special handlers to opened files and database connections.

```php
<?php
// Open a file for reading
$handle = fopen("note.txt", "r");
var_dump(is_resource($handle));

// Connect to MySQL database server with default setting
$link = mysql_connect("localhost", "root", "root");
var_dump(is_resource($link)); 
?>
```

### Documentation

* [Data Types Documentation](https://www.w3schools.com/php/php_datatypes.asp)

[Previous Topic](Previous)
[Next Topic](Next)