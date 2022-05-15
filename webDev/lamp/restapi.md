# rest API

[REST](https://restfulapi.net/) : **RE**presentational **S**tate **T**ransfer is an architectural style for designing your server API to manipulate or retrieve resources

|Request|Response|
|-|-|
|GET `/api/blogs/`|returns all blogs|
|GET `/api/blog/1/`|returns blog with *pk=1*|
|POST `/api/blogs/ param1="" param2=""`|adds a blog object into the database<br>params in response body|
|PUT `/api/blog/1/ param1="" param2=""`|updates the fields of blog with *pk=1*|
|DELETE `/api/blog/1/`|deletes blog with *pk=1*|

## PHP implementation
using vanilla php, we can make a restful API that responds with *json*

```php
// split the REQUEST_URI with '/' separator and remove all empty entries
$param = array_filter(
  explode("/", str_replace("/api/resource/", "", $_SERVER['REQUEST_URI']))
);

// get the http request body
$body = json_decode(file_get_contents('php://input'));
```

Use `$_SERVER['REQUEST_METHOD']` to know which http method is used at the request:
```php
if ($_SERVER['REQUEST_METHOD'] == "GET"){
    // respond accordingly
} 
```

Set response to json and echo a `json_encode(php_object);`
```php
header('Content-Type: application/json; charset=utf-8');
echo json_encode($data);
```

Example:
```php
if ($_SERVER['REQUEST_METHOD'] == "GET") {
    $query_res = $dbc->query("SELECT * FROM account");
    $data = $query_res->fetchAll(PDO::FETCH_ASSOC);
}

header('Content-Type: application/json; charset=utf-8');
echo json_encode($data);
```




