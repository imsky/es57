## ECMAScript 5

### Object

#### Object.keys

`Object.keys` returns an array of all enumerable own properties of an object.

**Replaces:** [`_.keys`](http://underscorejs.org/#keys)

```js
var dog = {
name: 'Tank',
breed: 'Mastiff'
};

var properties = Object.keys(dog);
console.log(properties);
```

### Array

#### Array.isArray

`Array.isArray` returns `true` if an object is an array and `false` otherwise.

**Replaces:** [`_.isArray`](http://underscorejs.org/#isArray), [`$.isArray`](http://api.jquery.com/jquery.isarray/)

```js
var evens = [2,4,6,8,10];
console.log(Array.isArray(evens));
```

### String

#### String.prototype.trim

`String.prototype.trim` returns a string with whitespace characters stripped from the start and finish.

**Replaces:** [`$.trim`](http://api.jquery.com/jQuery.trim/)

```js
var message = '   Hello World  ';
console.log(message.trim());
```

### Miscellaneous

#### Date.now

`Date.now` blah blah blah

**Replaces:** [`_.now`](http://underscorejs.org/#now), [`$.now`](http://api.jquery.com/jQuery.now/)

```js
console.log(Date.now());
```