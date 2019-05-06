# Implicit Coercion

### strpos

```php
<?php

$char = 'D';
if(strpos("David", $char) == false){
    echo "Character not found"; // Character not found
}
else{
    echo "Character found at: " . strpos("David", $char);
}
```

Since false is valued as 0 in PHP, and the strpos() function returns false if the character is not in the string. However, it should return the same thing, 0, if the character searched for is the first in the string, as the index of that character is 0.

```php
<?php

$char = 'D';
if(strpos("David", $char) === false){
    echo "Character not found";
}
else{
    echo "Character found at: " . strpos("David", $char); // Character found at: 0
}
```

### array_search

```php
<?php

$measure = array("inch" => 1, "foot" => 12, "yard" => 36);
// prints "foot"
echo array_search(12, $measure);
$units = array("inch", "centimeter", "chain", "furlong");
// prints 2
echo array_search("chain", $units);
```

Because array_search( ) returns a mixed result-the Boolean value false if the value isn't found or the key of the matching element-a problem is encountered when the first element is found. PHP's automatic type conversion treats the value 0-the index of the first element-as false in a Boolean expression. Care must be taken with functions, such as array_search( ), that return a result or the Boolean value false to indicate when a result can't be determined. If the return value is used as a Boolean-in an expression or as a Boolean parameter to a function-a valid result may be automatically converted to false.

The correct way to test the result is to use the is-identical operator ===, as shown in the following example:

```php
<?php

$index = array_search("inch", $units);

if ($index === false)
  echo "Unknown unit: inch";
else
  // OK to use $index
  echo "Index = $index";
```

### Documentation

- [Array Search Documentation](https://www.w3schools.com/php/func_array_search.asp)

- [Issue with strpos comparison](https://github.com/kalessil/phpinspectionsea/issues/1016)