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

### Running the Tests

```shell
~/proj/dir$ ./vendor/bin/phpunit testsFolder/
```

##### Alternatively
Set up this composer script:
```json
"scripts": {
    "test": "./vendor/bin/phpunit testsFolder/"
}
```
and run
```shell
~/proj/dir$ composer test
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
        $response = $this->http->request('GET', 'api/someResource/');

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