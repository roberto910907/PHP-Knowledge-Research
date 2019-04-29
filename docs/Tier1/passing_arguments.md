# Passing Arguments

## Passing as Value

Passing-by-value evaluation is the most common evaluation strategy. In this case, the argument expression is evaluated, and the resulting value is bound to the corresponding variable in the function. If the function or procedure is able to assign values to its parameters, only its local copy is assigned — that is, anything passed into a function call is unchanged in the caller’s scope when the function returns.

```php
function passingByValue($var) {
  $var++;
}

$num = 1;
passingByValue($num); // this won't modify the $num in the current scope
echo $num; // 1
```

## Passing as Reference

In pass-by-reference, a function receives an **implicit reference** to a variable used as argument, _rather than a copy of its value_. This typically means that the function can modify (i.e. assign to) the variable used as argument—something that will be seen by its caller. Pass-by-reference can therefore be used to provide an additional channel of communication between the called function and the calling function. A pass-by-reference language makes it more difficult for a programmer to track the effects of a function call, and may introduce subtle bugs.

```php
function passingByReference(&$var) {
  $var++;
}

$num = 1;
passingByReference($num); // this will modify the $num variable of the current scope
echo $num; // 2
```

> **Tips:** One key thing to remember is that a reference is a reference to a variable . If you define a function as accepting a reference to a variable, you cannot pass a constant into it.

### Pitfalls when using passing as reference

We need to think very carefully about passing by reference since the programmers that use your code could ended up with unexpected results because they think they’re passing by value. So it might be possible that they need to pass the same variable to different functions inside a block of code and that variable changes in the current scope because any of the previous functions are receiving it as a reference.

```php
$myVar = "Hi there";
$anotherVar = &$myVar;
$anotherVar = "See you later"; // this will trigger a change for $myVar
echo $myVar; // Displays "See you later"
echo $anotherVar; // Displays "See you later"
```

### Which functions use references

Array functions such as: **sort**, **asort**, **arsort**, **rsort**, **usort**, **uasort**, **uksort**. That's because they need to directly modify the array without creating a copy of it.

```php
<?php
$fruits = ["d" => "lemon", "a" => "orange", "b" => "banana", "c" => "apple"];
asort($fruits); // this will internally modify $fruits

var_dump($fruits);
//array(4) {
//  ["c"]=>
//  string(5) "apple"
//  ["b"]=>
//  string(6) "banana"
//  ["d"]=>
//  string(5) "lemon"
//  ["a"]=>
//  string(6) "orange"
//}
?>
```

### Documentation

* [Ways to create references in PHP](https://www.elated.com/php-references/)