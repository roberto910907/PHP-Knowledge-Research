# Libraries and Extensions

PHP extensions are compiled libraries which enable specific functions to be used in your PHP code.

For example, you want to interact with MySQL using PHP. You can implement your own methods to connect to MySQL server, make queries using TCP/IP protocol. However thats not a trivial task. Plus, that is not only your own requirement, but other developers also need to do similar thing.

You load an extension dynamically (generally written using C language) via adding a line in php.ini file like:

> extension= mysqli.so

And once its loaded, you can use functions like mysqli_connect, mysqli_query.

### Database accessing using PDO

#### Connecting to a database

```php
<?php

// Creating the new instance
$db = new PDO('mysql:host=localhost;dbname=testdb;charset=utf8mb4', 'username', 'password');

// Setting attributes
$db->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
$db->setAttribute(PDO::ATTR_EMULATE_PREPARES, false);

// Querying data from a DB table with parameters
$stmt = $db->query('SELECT * FROM vehicle WHERE id=:id AND model=:model');
$stmt->bindValue(':id', 1, PDO::PARAM_INT);
$stmt->bindValue(':model', 'Toyota', PDO::PARAM_STR);

// Iterating over elements and showing the retrieved information
while($row = $stmt->fetch(PDO::FETCH_ASSOC))
{
    echo $row['id'] .' '. $row['model'];
}
```

#### Transactions

```php
<?php

try {
    $db->beginTransaction();
    $db->exec("SELECT * FROM vehicle");

    $stmt = $db->prepare("INSERT INTO vehicle VALUES (1, 'Toyota')");
    $stmt->execute();

    $stmt = $db->prepare("UPDATE vehicle WHERE model = 'GMC'");
    $stmt->execute();

    $db->commit();
} catch(PDOException $ex) {
    //Something went wrong rollback!
    $db->rollBack();
    echo $ex->getMessage();
}
```

### Date and Time

The computer stores dates and times in a format called UNIX Timestamp, which measures time as number of seconds since the beginning of the Unix epoch (midnight Greenwich Mean Time on January 1, 1970 i.e. January 1, 1970 00:00:00 GMT ).
Since this is an impractical format for humans to read, PHP converts a timestamp to a format that is readable and more understandable to humans.

> date(format, timestamp)

```php
<?php
  
echo "Today's date is : ";
$today = date("d/m/Y");
echo $today; // Today's date is : 03/05/2019
?>
```

#### Formats

The following characters can be used to format the time string:

**h** – Represents hour in 12-hour format with leading zeros (01 to 12).
**H** – Represents hour in in 24-hour format with leading zeros (00 to 23).
**i** – Represents minutes with leading zeros (00 to 59).
**s** – Represents seconds with leading zeros (00 to 59).
**a** – Represents lowercase ante meridian and post meridian (am or pm).
**A** – Represents uppercase ante meridian and post meridian (AM or PM).

```php
<?php  
echo date("d/m/Y") . "\n"; // 05/12/2017
echo date("d-m-Y") . "\n"; // 05-12-2017
echo date("d.m.Y") . "\n"; // 05.12.2017
echo date("d.M.Y/D"); // 05.Dec.2017/Tue
?>
```

#### Timestamps

The mktime() function is used to create the timestamp for a specific date and time.
If no date and time is provided, the timestamp for the current date and time is returned.

```php
<?php
echo mktime(23, 21, 50, 11, 25, 2017); // 1511652110
```

### Documentation

- [List of PHP Extensions](https://en.wikipedia.org/wiki/List_of_PHP_extensions)

- [Date Official Documentation](https://www.php.net/manual/en/function.date.php)