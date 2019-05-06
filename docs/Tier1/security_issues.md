# Security Issues

In this section we will be covering some well-known security issues in PHP such as:

- SQL injection.
- eval is forbidden.
- Strip all errors on production.
- Don't strip or hide any errors on development.
- Not use the mysql extension, but instead mysqli.
- Common Apache configuration: .htaccess

### SQL Injection

SQL injection is a web security vulnerability that allows an attacker to interfere with the queries that an application makes to its database. It generally allows an attacker to view data that they are not normally able to retrieve. This might include data belonging to other users, or any other data that the application itself is able to access. In many cases, an attacker can modify or delete this data, causing persistent changes to the application's content or behavior.

Eg:

Consider a shopping application that displays products in different categories. When the user clicks on the Gifts category, their browser requests the URL:

https://insecure-website.com/products?category=Gifts

This causes the application to make an SQL query to retrieve details of the relevant products from the database:

```php
SELECT * FROM products WHERE category = 'Gifts' AND released = 1
```

The application doesn't implement any defenses against SQL injection attacks, so an attacker can construct an attack like:

https://insecure-website.com/products?category=Gifts'--

This results in the SQL query:

```php
SELECT * FROM products WHERE category = 'Gifts'--' AND released = 1
```

The key thing here is that the double-dash sequence -- is a comment indicator in SQL, and means that the rest of the query is interpreted as a comment. This effectively removes the remainder of the query, so it no longer includes AND released = 1. This means that all products are displayed, including unreleased products.

Going further, an attacker can cause the application to display all the products in any category, including categories that they don't know about:

https://insecure-website.com/products?category=Gifts'+OR+1=1--

This results in the SQL query:

```php
SELECT * FROM products WHERE category = 'Gifts' OR 1=1--' AND released = 1
```

The modified query will return all items where either the category is Gifts, or 1 is equal to 1. Since 1=1 is always true, the query will return all items.

### MySQLi instead of MySQL

- MySQLi has this feature called prepared statements which is nothing but a safer way of sending data to MySQL and protecting yourself from getting hacked using SQL injection.
- MySQLi extension has been specifically developed to take advantage of the new features available in MySQL Server version 4.1.3 and above. So the thing is if you still use the MySQL extension then you might not be able to take full advantage of the new MySQL server features.
- MySQLi supports multiple Statements, Complex Transaction statements and has enhanced debugging capabilities and embedded server support.
- Using object oriented interface allow us to provide security to sensitive data.

### Using eval()

 Evaluate a string as PHP code. This is often used by an attacker to hide their code and tools on the server itself. Also the PHP manual discourages the use of the eval() construct, stressing its use is "very dangerous" because arbitrary PHP code can be executed. Users are instructed to use any other option than eval() unless that is not possible. The use of PHP eval() construct presents security risks.

 > **Tips:** You must configure PHP to disable eval().

```php
<?php
  
$age = 27;
$str = 'My age is $age';
echo $str. "\n"; // My age is $age
  
eval("\$str = \"$str\";");
echo $str. "\n"; // My age is 20
```

### .htaccess Apache Configuration

In many cases it is wrong to impose security restrictions using .htaccess files. The reasons are:

- The functionality of  .htaccess files depends on the value of the AllowOverride Apache directive. If this directive  is not configured properly, your security restriction will not work. You could have a web application that works perfectly on your Apache web server where AllowOverride allows the usage of .htaccess files. But when you install the web application on another server with disabled AllowOverride, the security restrictions will not work and your web application will become vulnerable.
  
- Most modern PHP based web application can be installed on other web servers that do not support .htaccess files such as nginx, a web server that is gaining popularity. There are other web servers that don’t support .htaccess files. When developing a web application which is going to be used by to the public, one should not expect that everybody will use Apache. If the security of your web application depends on restrictions imposed by .htaccess files, as soon as one of your customers installs the application on an nginx web server, they will be vulnerable.

### Errors configuration on Production and Development environments

When we are building applications one of the most important features is to be able to detect errors before our code is deployed to a production environment,that's why we need to configure PHP to show as much information as possible.

There are some options that we must enable in order to receive that kind of vital information such as:

- **display_errors**: On
- **display_startup_errors**: On
- **error_reporting**: E_ALL & ~E_NOTICE

However, when we are talking about security concerns on our production server we will need to turn off those configurations and then enable the **error_log** option in our php.ini which allows us to save every single triggered error inside a log file. So if we need to debug our application, we will be able to review the last lines of that file to find what's the issue. In that way, we avoid to show extra information to end users, because we never know when that extra information could be used against us.

### Documentation

- [Eval Base64 Hask WordPress](https://secure.wphackedhelp.com/blog/eval-base64-decode-hack-wordpress/)

- [Utilizing .htaccess for exploitation purposes](https://medium.com/@insecurity_92477/utilizing-htaccess-for-exploitation-purposes-part-1-5733dd7fc8eb)

- [MySql vs MySqli in PHP](https://phppot.com/php/mysql-vs-mysqli-in-php/)