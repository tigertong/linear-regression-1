Simple Linear Regression
===
[![NPM version][npm-image]][npm-url] [![Build Status][travis-image]][travis-url] [![Coverage Status][coveralls-image]][coveralls-url] [![Dependencies][dependencies-image]][dependencies-url]

> Computes a least squares estimator of a [linear regression](http://en.wikipedia.org/wiki/Simple_linear_regression) model having a single explanatory variable.


## Installation

``` bash
$ npm install compute-linear-regression
```

For use in the browser, use [browserify](https://github.com/substack/node-browserify).


## Usage

``` javascript
var lr = require( 'compute-linear-regression' );
```

#### lr( x[, y[, opts] ] )

Computes a least squares estimator of a [linear regression](http://en.wikipedia.org/wiki/Simple_linear_regression) model having a single explanatory variable. 

``` javascript
var x, y;

x = [ ];
y = [ ];

var model = lr( x, y );
```

If provided a single `array`, the function assumes a [zipped](https://github.com/compute-io/zip) `array` of 2-element tuples `[x_i,y_i]`.

``` javascript
var data = [
	[0,1],
	[1,2],
	[2,3],
	...
];

var model = lr( data );
```

The function accepts the following `options`:

* 	__accessors__: `object` providing accessor `functions`.
	-	__x__: accessor `function` for accessing explanatory values.
	-	__y__: accessor `function` for accessing response values.
*	__slope__: known slope.
*	__intercept__: known *y*-intercept.

To provide arbitrary access to input `array` values, provide accessor `functions`.

``` javascript
function xValue( d, i ) {
	return d.x;
}

function yValue( d, i ) {
	return d.y;
}

var x, y, data, model;

// Separate input arrays...
x = [
	{'x':0},
	{'x':1},
	...
];

y = [];

model = lr( x, y, {
	'accessors': {
		'x': xValue
	}
});

// Single input array...
data = [
	{'x':0,'y':1},
	{'x':1,'y':2},
	...
];

model = lr( data, {
	'accessors': {
		'x': xValue,
		'y': yValue
	}
});
```

By default, the implementation assumes both the slope and *y*-intercept are __unknown__. Should either one or both be known, set the corresponding options.

``` javascript
var model;

// Known y-intercept:
model = lr( x, y, {
	'intercept': 100
});

// Known slope:
model = lr( x, y, {
	'slope': 5
});

// Both are known:
model = lr( x, y, {
	'slope': 5,
	'intercept': 100
});
```

Note that, in the special case where the *y*-intercept is `0`, this is equivalent to computing a linear regression model which assumes a polynomial of the form

```
f(x) = y = bx
```

Hence, to compute a model lacking a constant term

``` javascript
var model = lr( x, y, {
	'intercept': 0
});
```


#### model

The computed linear regression model has the following methods...


##### model.residuals()

Computes the differences between each observation `y_i` and the corresponding prediction `y^{hat}_i`.

``` javascript

```


##### model.ci()

Computes estimated confidence intervals.

``` javascript

```


##### model.summary()

Computes a statistical summary.

``` javascript

```


##### model.predictor()

Generates a predictor `function`.

``` javascript

```


##### model.print()

Pretty prints a model to the console.

``` javascript

```






## Notes

The (simple) linear regression model assumes a *linear polynomial* of the form

```
f(x) = y = a + bx
```

describing the relationship between an independent variable `x` and a dependent variable `y`. `x` is commonly referred to as the __explanatory__, __predictor__, or __regressor__ variable, and `y` is commonly referred to as the __response__ variable. `a` and `b` are (possibly) unknown __coefficients__ to be determined based on the inputs `x` and `y`. Geometrically, `f(x)` is a straight line having a *y*-intercept `a` and a slope `b`.

To determine the model parameters `a` and `b`, this implementation uses [ordinary least squares](http://en.wikipedia.org/wiki/Ordinary_least_squares) (OLS) to fit a straight line to the data. Intuitively, our goal is to find a line having a slope and *y*-intercept which minimizes the distance between an observation and its corresponding fitted (predicted) value. To achieve this goal, OLS seeks to minimize the following function

```
L = sum^{N-1}_{i=0} [y_i - f(x_i)]^2
```

where `N` is the number of observations and `y_i - f(x_i)` corresponds to the vertical distance between an observation `y_i` and a predicted value `f(x_i)`. The smaller each distance between `y_i` and `f(x_i)` is, the smaller the sum and the better the fit.



## Examples

``` javascript
var lr = require( 'compute-linear-regression' );
```

To run the example code from the top-level application directory,

``` bash
$ node ./examples/index.js
```



## Tests

### Unit

Unit tests use the [Mocha](http://mochajs.org/) test framework with [Chai](http://chaijs.com) assertions. To run the tests, execute the following command in the top-level application directory:

``` bash
$ make test
```

All new feature development should have corresponding unit tests to validate correct functionality.


### Test Coverage

This repository uses [Istanbul](https://github.com/gotwarlost/istanbul) as its code coverage tool. To generate a test coverage report, execute the following command in the top-level application directory:

``` bash
$ make test-cov
```

Istanbul creates a `./reports/coverage` directory. To access an HTML version of the report,

``` bash
$ make view-cov
```


---
## License

[MIT license](http://opensource.org/licenses/MIT). 


## Copyright

Copyright &copy; 2015. Athan Reines.


[npm-image]: http://img.shields.io/npm/v/compute-linear-regression.svg
[npm-url]: https://npmjs.org/package/compute-linear-regression

[travis-image]: http://img.shields.io/travis/compute-io/linear-regression/master.svg
[travis-url]: https://travis-ci.org/compute-io/linear-regression

[coveralls-image]: https://img.shields.io/coveralls/compute-io/linear-regression/master.svg
[coveralls-url]: https://coveralls.io/r/compute-io/linear-regression?branch=master

[dependencies-image]: http://img.shields.io/david/compute-io/linear-regression.svg
[dependencies-url]: https://david-dm.org/compute-io/linear-regression

[dev-dependencies-image]: http://img.shields.io/david/dev/compute-io/linear-regression.svg
[dev-dependencies-url]: https://david-dm.org/dev/compute-io/linear-regression

[github-issues-image]: http://img.shields.io/github/issues/compute-io/linear-regression.svg
[github-issues-url]: https://github.com/compute-io/linear-regression/issues
