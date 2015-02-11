## Bind

Example:

```js
Function.prototype._bind = function() {
    // Shorthand for Array.prototype.slice
    var slice = [].slice;
    // All other arguments prepended to the bound call follow the context
    var args = slice.call(arguments, 1);
    // Reference to the function being bound
    var fn = this;
    // Empty function used to replicate prototype chain
    var empty = function() {};
    var bound = function() {
        return fn.apply(
        // Ignore context if called as constructor
        this instanceof empty ? this : ctx,
        // Prepend outer arguments to current arguments
        args.concat(slice.call(arguments)));
    };
    // Used for inheriting properties on the prototype chain of the bound function
    empty.prototype = fn.prototype;
    bound.prototype = new empty();

    // Returns a new function with optional prepended arguments, called in specified context
    return bound;
}

function Place(country, city) {
    this.city = city;
    this.country = country;
    return this;
}

Place.prototype.toString = function() {
    return this.city + ', ' + this.country;
}

var americanCity = Place._bind(null, 'USA');
var newYork = new americanCity('New York City');
console.log(String(newYork));

var englishCity = Place._bind({}, 'England');
var london = englishCity('London');
console.log(Place.prototype.toString.call(london));
```

## Curry

Example:

```js
Function.prototype._curry = function() {
    // Shorthand for Array.prototype.slice
    var slice = [].slice;
    // Reference to the function being curried
    var fn = this;

    var curry = function() {
        var args = slice.call(arguments);

        // Return a closure to continue application
        return function() {
            // Append the arguments of the current call to existing arguments
            var nargs = args.concat(slice.call(arguments));
            // If there aren't enough arguments yet, return closure, otherwise apply arguments to curried function
            return (nargs.length >= fn.length ? fn : curry).apply(null, nargs);
        };
    };

    // If the call has as many arguments as the function, call the function directly
    return (arguments.length >= fn.length ? fn : curry).apply(null, arguments);
}

function triple(a, b, c) {
    return a + b + c;
}

console.log(triple._curry('New')('York')('City'));
console.log(triple._curry('Graphical')('User', 'Interface'));
console.log(triple._curry()(1)()(2)()(3));
```

## Flatten

```js
// Ensure that the function is not enumerable
Object.defineProperty(Array.prototype, '_flatten', {
    value: function() {
        function flatten(arr) {
            // Continuously concatenate to initial empty array
            return arr.reduce(function(prev, curr) {
                // Concatenate a value directly if it's not an array, and if it is, concatenate its flattened representation, which is a flat array
                return prev.concat(curr.constructor === Array ? flatten(curr) : curr);
            }, []);
        }
        return flatten(this);
    }
});

console.log([1,2,[3,[4,[],[],[[5]]]]]._flatten());
console.log([[[[1],[2],[3],[4],[[5]]]]]._flatten());
```

## Memoize

```js
Function.prototype._memoize = function() {
    var cache = {};
    var fn = this;
    var memoize = function() {
        // Set key to string of arguments, which works for multiple primitive arguments
        var key = JSON.stringify(arguments);
        if (!cache[key]) {
            // Cache the result of the function if not already in cache
            cache[key] = fn.apply(fn, arguments);
        }
        return cache[key];
    }

    return memoize;
}

function fib(n) {
    if (n < 2) return n;
    return fib(n - 1) + fib(n - 2);
}

function timer(fn) {
    var start = Date.now();
    fn();
    return Date.now() - start;
}

function test() {
    return timer(function() {
        for (var i = 0; i < 10; i++) {
            fib(35);
        }
    });
}

console.log(test());
fib = fib._memoize();
console.log(test());
```