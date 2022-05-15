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

<br><br>


# Unit Testing APIs

Reference:
- [Using Guzzle and PHPUnit for REST API Testing](https://blog.cloudflare.com/using-guzzle-and-phpunit-for-rest-api-testing/)

Install **phpunit/phpunit** for automated testing and **guzzlehttp/guzzle** for http client requests and responses.

#### composer.json
```json
"require-dev": {
  "phpunit/phpunit": "^9.5",
  "guzzlehttp/guzzle": "^7.4"
}
```
##### Alternatively:
```shell
~/proj/dir$ composer require --dev phpunit/phpunit
~/proj/dir$ composer require --dev guzzlehttp/guzzle
```

## Writing TestCases
We will create a php clas file than extends `PHPUnit\Framework\TestCase`

```php
<?php
// AccountTest.php
use PHPUnit\Framework\TestCase;
use GuzzleHttp\Client;

class AccountTest extends TestCase{
  
  private $client;

  public function setUp() : void {
    $this->client = new Client(['base_uri':'http://server:port/']);
  }

  public function tearDown() : void {
    $this->client = null;
  }
}
```

> `TestCase::setUp()` is called **before each** test.<br> `TestCase::setUpBeforeClass()` is called **before all** tests of this class.<br>`TestCase::tearDown()` is called **after each** test.<br>`TestCase::tearDownAfterClass()` is called **after all** tests of this class.

```php

  public function testGet()
    {
        // arrange
        $expectedResponse = 200;
        $expectedContentType = "application/json";
        $expectedBody = (object)[
          "field1" => "val1",
          "field1" => "val2",
        ];

        // act
        $response = $this->http->request('GET', 'api/accounts/');

        $actualStatusCode = $response->getStatusCode();
        $actualContentType = $response->getHeaders()["Content-Type"][0];
        $actualBody = json_decode($response->getBody());

        // assert
        $this->assertEquals($expectedResponse, $actualStatusCode);
        $this->assertEquals($expectedContentType, $actualContentType);
        $this->assertEquals($expectedBody, $actualBody);
    }
}
```