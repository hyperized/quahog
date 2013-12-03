Quahog
======

Quahog is a simple PHP library to interface with the clamd anti-virus daemon. It was written as all of the libraries out
there for interfacing with ClamAV from PHP use ```exec('clamscan')```, which isn't exactly an ideal solution, as
```clamscan``` loads the entire database into memory each time it is run - this doesn't, so it scans a lot (lot!) faster.

## Installation

It is recommended to install Quahog through [composer](http://getcomposer.org).

```JSON
{
    "require": {
        "blurgroup/quahog": "0.*"
    }
}
```

## Usage

```php
$quahog = new \Quahog\Client();

// Scan a file
$result = $quahog->scanFile('/tmp/virusfile');

// Scan a file or directory recursively
$result = $quahog->contScan('/tmp/virusdirectory');

// Scan a file or directory recursively using multiple threads
$result = $quahog->multiscanFile('/tmp/virusdirectory');

// Scan a stream, and optionally pass the maximum chunk size in bytes
$result = $quahog->scanStream(file_get_contents('/tmp/virusfile'), 1024);

// Ping clamd
$result = $quahog->ping();

// Get ClamAV version details
$result = $quahog->version();

// View statistics about the ClamAV scan queue
$result = $quahog->stats();

// Reload the virus database
$quahog->reload();

// Shutdown clamd cleanly
$quahog->shutdown();
```

## Testing

To run the test suite you will need PHPUnit installed. Go to the project root and run:
````bash
$ phpunit
````

## Credits

![blur Group](http://i.imgur.com/5kko4VT.png)

[Jonjo McKay](mailto:jonjo@blurgroup.com) and [blur Group](http://blurgroup.com)

## License

Quahog is released under the [MIT License](http://www.opensource.org/licenses/MIT)