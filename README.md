flow-covariance
===============

Reduce transform stream which computes the covariance of a numeric data stream.


## Installation

``` bash
$ npm install flow-covariance
```


## Examples

``` javascript
var // Flow covariance stream generator:
	cStream = require( 'flow-covariance' );

var data = new Array( 1000 ),
	value,
	stream;

// Create some data... (negatively corrrelated)
for ( var i = 0; i < 1000; i++ ) {
	value = Math.random() * 50;
	data[ i ] = {
		'y1': 50 + value,
		'y2': 50 - value
	}
}

// Create a new stream:
stream = cStream()
	.accessors( 'y1', function( d ) {
		return d.y1;
	})
	.accessors( 'y2', function( d ) {
		return d.y2;
	})
	.stream();

// Add a listener:
stream.on( 'data', function( covar ) {
	console.log( 'Covariance: ' + JSON.stringify( covar ) );
});

// Write the data to the stream...
for ( var j = 0; j < data.length; j++ ) {
	stream.write( data[ j ] );
}
stream.end();
```

## Tests

Unit tests use the [Mocha](http://visionmedia.github.io/mocha) test framework with [Chai](http://chaijs.com) assertions.

Assuming you have installed Mocha, execute the following command in the top-level application directory to run the tests:

``` bash
$ mocha
```

All new feature development should have corresponding unit tests to validate correct functionality.


## License

[MIT license](http://opensource.org/licenses/MIT). 


---
## Copyright

Copyright &copy; 2014. Athan Reines.

