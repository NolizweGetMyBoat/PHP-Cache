# PHP Cache
## Getting Started

1. Download `cache.php` file
2. Change `$_salt` value on line 5 
3. Create readable and writable `tmp/` directory
4. Done! Let's move on to some code examples..

## Code Examples
### Example One
```php
include("cache.php");

$c = new Cache();

if(!$c->get("example", $result))
{
    $result = /* some extensive operation here */;
    $c->set("example", $result, 300); // cache result for 5 minutes (300 seconds)
}

var_dump($result);
```

### Example Two
```php
include("cache.php");

$c = new Cache();

if($c->get("views", $views))
{
    echo "Video views: " . $views;
}
else
{
    echo "Cache not found or expired";
}
```

## Functions
### function __construct($name = "default", $dir = "tmp/", $extension = ".cache")
Class constructor
* `$name` - name of the cache
* `$dir` - directory where the cache will be stored
* `$extension` - extension of the cache file

### function set($key, $value, $ttl = -1)
Writes data to cache
* `$key` - key of the value
* `$value` - value
* `$ttl` - *Time To Live* (in how many seconds value will expire)

### function get($key, &$out)
Reads data from cache
* `$key` - key of the value
* `&$out` - reference to the output value
* return:
  * bool(false) - value not cached or expired
  * bool(true) - success (value is set to the `$out` argument)
  
### function remove($key)
Removes data from cache
* `$key` - key of the value
* return:
  * bool(false) - key not found
  * bool(true) - success
