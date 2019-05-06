# Implicit State

There are some built-in functions to save and retrieve the errors that happens to a C level such as:

- curl_error
- json_last_error
- openssl_error_string
- imap_errors
- mysql_error
- xml_get_error_code
- bzerror
- date_get_last_errors

With these functions we are able to collect all the latest errors that happen in our application.

```php
<?php
// lets assume you just called an openssl function that failed
while ($msg = openssl_error_string())
    echo $msg . "<br />\n";
```

To prevent these error I would recommend to validate the information before calling some function that may end up with side effects. So for example, before calling **json_decode** we must make sure that the argument we will use in the function has a valid json format by calling json_validate 
or any other helper function.

Also we could create some helper functions to catch those errors an create a proper exception to be thrown by our system like:

```php
json_decode($string);

switch (json_last_error())
{
    case JSON_ERROR_NONE:
        echo ' - No errors';
    break;
    case JSON_ERROR_DEPTH:
        // throw specific exception related to the issue
        throw new RuntimeException('Maximum stack depth exceeded');
    break;
    case JSON_ERROR_STATE_MISMATCH:
        // throw specific exception related to the issue
        throw new RuntimeException('Underflow or the modes mismatch');
    break;
    case JSON_ERROR_CTRL_CHAR:
        // throw specific exception related to the issue
        throw new RuntimeException('Unexpected control character found');
    break;
    case JSON_ERROR_SYNTAX:
        // throw specific exception related to the issue
         throw new RuntimeException('Syntax error, malformed JSON');
    break;
    case JSON_ERROR_UTF8:
        // throw specific exception related to the issue
         throw new RuntimeException('Malformed UTF-8 characters, possibly incorrectly encoded');
    break;
    default:
        // throw specific exception related to the issue
         throw new RuntimeException('Unknown error');
    break;
}
```

> **Tips**: Since PHP 7.3, the json_decode function will accept a new JSON_THROW_ON_ERROR option that will let json_decode throw an exception instead of returning null on error.

```php
try {  
  json_decode("{", false, 512, JSON_THROW_ON_ERROR);  
}  
catch (\JsonException $exception) {  
  echo $exception->getMessage(); // displays "Syntax error"  
}
```

### Default Encoding

There are actually several formats of Unicode data, but UTF-8 is the most commonly used online.

You should set your **default_charset** to UTF-8:

```php
default_charset = "utf-8"
```

And last but not least, you can overrule this setting with PHP’s ini_set() function:

```php
ini_set( 'default_charset', "" );
```

### Documentation

- [Validate json string](https://stackoverflow.com/questions/6041741/fastest-way-to-check-if-a-string-is-json-in-php)

- [Encoding Charset](https://help.fortrabbit.com/encoding)