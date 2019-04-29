# SuperGlobals

In PHP there are some _"global variables"_, which means that they are always accessible, regardless of scope - and you can access them from any function, class or file without having to do anything special.

Superglobals are commonly used under the hood in the real PHP world. Nowadays is almost impossible start writing PHP without using a framework, and superglobals are one of those concepts that get wrapped by Object Oriented Programming. We usually create a Request object which contains all the supergloblas inside and you can access them as properties.

The PHP superglobal variables are:

* **$_SERVER**
* **$_REQUEST**
* **$_POST**
* **$_GET**
* **$_FILES**
* **$_ENV**
* **$_COOKIE**
* **$_SESSION**

##### Here is an example about how to use superglobals in a modern web application

```php
namespace App\Session;

use App\Session\Interfaces\SessionInterface;

class Session implements SessionInterface
{
    /**
     * {@inheritdoc}
     */
    public function start()
    {
        session_start();
    }

    /**
     * {@inheritdoc}
     */
    public function has(string $name)
    {
        return array_key_exists($name, $_SESSION);
    }

    /**
     * {@inheritdoc}
     */
    public function get(string $name, $default = null)
    {
        if ($this->has($name)) {
            return $_SESSION[$name];
        }
  
        if ($default) {
            return $default;
        }

        return null;
    }

    /**
     * {@inheritdoc}
     */
    public function set(string $name, $value)
    {
        $_SESSION[$name] = $value;
    }

    /**
     * {@inheritdoc}
     */
    public function remove(string $name)
    {
        unset($_SESSION[$name]);
    }
}
```

### Documentation

* [How superglobals are wrapped into a Request object in Symfony framework](https://symfony.com/doc/current/introduction/http_fundamentals.html#symfony-request-object)

* [How to get a superglobal stored value insinde a Request object in Laravel framework](https://laravel.com/docs/4.2/requests#request-information)
