# States in Operations

In PHP there are some function that change the status of the given element instead of creating a new copy of it. It's always recommended to create a copy of the element so we don't alter the original state creating side effects.

```php
$array = array(1, 2, 3, 4);
foreach ($array as &$value) {
    $value = $value * 2;
}
// $arr is now array(2, 4, 6, 8)
```

The problem is that, if you’re not careful, this can also have some undesirable side effects and consequences. Specifically, in the above example,after the code is executed, \$value will remain in scope and will hold a reference to the last element in the array. Subsequent operations involving $value could therefore unintentionally end up modifying the last element in the array.

```php
$array = [1, 2, 3];
echo implode(',', $array), "\n"; // 1,2,3

foreach ($array as &$value) {}    // by reference
echo implode(',', $array), "\n";  // 1,2,3

foreach ($array as $value) {}     // by value (i.e., copy)
echo implode(',', $array), "\n";  // 1,2,2
```

### Functions that alter the state

Most of the array sorting functions receives the array to modify as a reference which may end up in a complete misunderstanding if you're not aware about what's happening behind the scene. Since you might need to use the original array and not realizing that it's been changed in a previous line by another function.

- **asort**
- **sort**
- **uksort**

### Functions that create a copy of the element

There are some other functions that instead of modifying the current state of the structure, they create a copy of the original data and iterate over it to get the final result as a completely new structure.

- **array_map**
- **array_chunk**
- **array_combine**

### Documentation

- [Array functions side effects](https://www.startutorial.com/articles/view/master-php-array-functions)