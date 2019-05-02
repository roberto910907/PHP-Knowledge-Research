# Namespaces

It can be seen as an abstract concept in many places. It allows redeclaring the same functions/classes/interfaces/constant functions in the separate namespace without getting the fatal error. A namespace is a hierarchically labeled code block holding a regular PHP code. A namespace can contain valid PHP code. Namespace affects following types of code: classes (including abstracts and traits), interfaces, functions, and constants, and are declared using the **namespace** keyword.

### Common Problems Solved by Namespaces

* Name collisions between code you create, and internal PHP classes/functions/constants or third-party classes/functions/constants.

* Ability to alias (or shorten) Extra_Long_Names designed to alleviate the first problem, improving readability of source code.

### Fully Qualified Class Name (FQCN) structure

> \\<**NamespaceName**>\\<**SubNamespaceNames**>)*\\<**ClassName**>

### Single Namespace

Given the following directory structure:

* MyProject
  * src
    * **Controllers**
    * Services
    * Repositories
  * config
  * database
  * resources
  
We can create a new controller class by doing:

```php
<?php

namespace Controllers; // composer is configured to point to src folder

use Laravel\Http\BaseController;

class FrontendController extends BaseController
{
    // implement methods to render frontend views
}
```

### Sub-namespaces

PHP also brings the ability to specify a hierarchy of namespace names:

Given the following directory structure:

* MyProject
  * app
    * Http
      * **Controllers**
        * **Backend**
      * Services
      * Repositories
  * config
  * database
  * resources

We can create a new controller class by doing:

```php
<?php

namespace Http\Controllers\Backend; // composer is configured to point to app folder

use Laravel\Http\BaseController;

class ConfigurationController extends BaseController
{
    // implement methods to render frontend views
}
```

### Aliasing/Importing

The ability to refer to an external fully qualified name with an alias, or importing, is an important feature of namespaces. This is similar to the ability of unix-based filesystems to create symbolic links to a file or to a directory.

```php
<?php

namespace Http\Controllers\Backend; // composer is configured to point to app folder

use Laravel\Http\BaseController as BaseApiController; // we create an alias to avoid collision with the names

class BaseController extends BaseApiController
{
    // implement methods to render frontend views
}
```

### Documentation

* [Single Namespace](https://www.php.net/manual/en/language.namespaces.definition.php)

* [Sub-namespaces](https://www.php.net/manual/en/language.namespaces.nested.php)

* [PHP namespaces in 120 seconds](https://symfonycasts.com/screencast/php-namespaces-in-120-seconds/namespaces)

* [Namespaces Resolution Rules](https://www.php.net/manual/en/language.namespaces.rules.php)

* [Aliasing/Importing Namespaces](https://www.php.net/manual/en/language.namespaces.importing.php)