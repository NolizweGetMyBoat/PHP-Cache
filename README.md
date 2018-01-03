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
$result = $c->get("queryResult");

if(!$result) // bool(false) - not cached or expired
{
    $result = /* some extensive operation here */;
    $c->set("queryResult", $result, 300); // cache result for 5 minutes (300 seconds)
}
```

### Example Two
```php
include("cache.php");

$c = new Cache();

if($c->has("videoViews")
{
    echo "Video views: " . $c->get("videoViews");
}
else
{
    echo "Cache not found or expired";
}
```

## Functions
### function __construct($name = "default", $dir = "tmp/", $extension = ".cache")
* `$name` - name of the cache
* `$dir` - directory where the cache will be stored
* `$extension` - extension of the cache file

### function set($key, $value, $ttl = -1)
* `$key` - key of the value
* `$value` - value
* `$ttl` - *Time To Live* (in how many seconds value will expire)

### function get($key)
* `$key` - key of the value
* return:
  * bool(false) - value not cached or expired
  * value - cached value

### function has($key)
* `$key` - key of the value
* return:
  * bool(false) - value not cached or expired
  * bool(true) - value cached and available
