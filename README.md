## Bind

Example:

```js
Function.prototype._bind = function(ctx) {
    var slice = [].slice;
    var args = slice.call(arguments, 1);
    var fn = this;
    var empty = function() {};
    var bound = function() {
        return fn.apply(
        this instanceof empty ? this : ctx,
        args.concat(slice.call(arguments)));
    }
    empty.prototype = fn.prototype;
    bound.prototype = new empty();
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

With comments:

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
    }
    // Used for inheriting properties on the prototype chain of the bound function
    empty.prototype = fn.prototype;
    bound.prototype = new empty();
    // Returns a new function with optional prepended arguments, called in specified context
    return bound;
}
```

## Curry

Example:

```js
Function.prototype._curry = function() {
    var slice = [].slice;
    var fn = this;

    var curry = function() {
        var args = slice.call(arguments);

        return function() {
            var nargs = args.concat(slice.call(arguments));
            return (nargs.length >= fn.length ? fn : curry).apply(null, nargs);
        };
    };

    return (arguments.length >= fn.length ? fn : curry).apply(null, arguments);
}

function triple(a, b, c) {
    return a + b + c;
}

console.log(triple._curry('New')('York')('City'));
console.log(triple._curry('Graphical')('User', 'Interface'));
console.log(triple._curry()(1)()(2)()(3));
```

With comments:

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
            // Append the arguments of the current function to existing arguments
            var nargs = args.concat(slice.call(arguments));
            // If there aren't enough arguments yet, return closure, otherwise apply arguments to curried function
            return (nargs.length >= fn.length ? fn : curry).apply(null, nargs);
        };
    };

    // If the call has as many arguments as the function, call the function directly
    return (arguments.length >= fn.length ? fn : curry).apply(null, arguments);
}
```