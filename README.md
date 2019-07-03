Route
=====

### Install

If you have Composer, just include route as a project dependency in your `composer.json`. If you don't just install it by downloading the .ZIP file and extracting it to your project directory.

```
require: {
    "yzmcms/route": "*"
}
```

### Examples

First, `use` the route namespace:

```PHP
use yzmcms\route\route;
```

route is not an object, so you can just make direct operations to the class. Here's the Hello World:

```PHP
route::get('/', function() {
  echo 'Hello world!';
});

route::exec();
```

route also supports lambda URIs, such as:

```PHP
route::get('/(:any)', function($slug) {
  echo 'The slug is: ' . $slug;
});

route::exec();
```

You can also make requests for HTTP methods in route, so you could also do:

```PHP
route::get('/', function() {
  echo 'I'm a GET request!';
});

route::post('/', function() {
  echo 'I'm a POST request!';
});

route::any('/', function() {
  echo 'I can be both a GET and a POST request!';
});

route::exec();
```


## Example passing to a controller instead of a closure
<hr>
It's possible to pass the namespace path to a controller instead of the closure:

For this demo lets say I have a folder called controllers with a demo.php

index.php:

```php
require('vendor/autoload.php');

use yzmcms\route\route;

route::get('/', 'Controllers\demo@index');
route::get('page', 'Controllers\demo@page');
route::get('view/(:num)', 'Controllers\demo@view');

route::exec();
```

demo.php:

```php
<?php
namespace controllers;

class Demo {

    public function index()
    {
        echo 'home';
    }

    public function page()
    {
        echo 'page';
    }

    public function view($id)
    {
        echo $id;
    }

}
```

This is with route installed via composer.

composer.json:

```
{
   "require": {
        "yzmcms/route": "*"
    },
    "autoload": {
        "psr-4": {
            "" : ""
        }
    }
}
