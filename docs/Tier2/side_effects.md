# Side Effects

### When opening files

Sometimes you will need to open a file to retrieve it contents to be able to process that information in some way. For that purpose you can use **fopen** function, it returns a file pointer resource on success, or **FALSE** on error. If the open fails, an error of level **E_WARNING** is generated.

```php
fopen('test.txt', 'a+');
```

By doing that you will be able to open the file as long that two conditions are fit, the file exist in the current directory and the file has permission for the current user to be opened.

> **Note**: When using +a option as the second parameter it will attempt to create the file if it does not exists.

Also in order to use this function properly, you need to take into account that you need to activate **allow_url_fopen**.

When the **allow_url_fopen** directive is enabled, you can write scripts that open remote files as if they are local files. For example, you can use the file_get_contents function to retrieve the contents of a web page.

To enable this functionality, use a text editor to modify the **allow_url_fopen** directive in the php.ini file as follows:

```php
allow_url_fopen = on
```

To disable this functionality, modify the **allow_url_fopen** directive in the php.ini file as follows:

```php
allow_url_fopen = off
```

### When inserting with MySQL

```php
-- (id, title, cost, price)
INSERT INTO products VALUES
(null, "product title", 3000, 6000),
(null, "product title", 3000, 6000),
(null, "product title", INVALID_VALUE_THAT_CANT_BE_INSERTED, 6000),
```

What happens if one of the inserts has an error like the last one in this case, the statement stops executing, and any changes that were underway are undone. However, **there may be some side effects** from the failed insert... for example, the AUTO_INCREMENT on the table (if there is one) may be higher than it was when the INSERT statement started.

If you don't need to insert that "invalid" row, but you need the other ones to be inserted, you could use an **INSERT IGNORE** statement.

The **IGNORE** tells MySQL not to raise an error when an insert of a particular row fails. MySQL continues to run the statement and allow it complete successfully, with warnings, rather than errors.

If you inserted a thousand rows, and one row had an error, you'd have a warning, and the other 999 rows would be inserted.

### Documentation

- [fopen common issues](https://stackoverflow.com/questions/5160362/php-fopen-not-creating-file-if-it-doesnt-already-exist)