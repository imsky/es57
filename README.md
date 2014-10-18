## ECMAScript 5

### Object

#### Object.keys

`Object.keys` returns an array of all enumerable properties of an object.

**Replaces:** [`_.keys`](http://underscorejs.org/#keys)

```js
var dog = {
name: 'Tank',
breed: 'Mastiff'
};
console.log(Object.keys(dog));
```

#### Object.getOwnPropertyNames

`Object.getOwnPropertyNames` returns an array of all properties of an object, enumerable or not.

```js
var person = Object.create({}, {
name: { value: 'John Rockefeller', enumerable: true},
netWorth: { value: 1000000, enumerable: false }
});
console.log(Object.keys(person));
```

### Array

#### Array.isArray

`Array.isArray` returns `true` if an object is an array and `false` otherwise.

**Replaces:** [`_.isArray`](http://underscorejs.org/#isArray), [`$.isArray`](http://api.jquery.com/jquery.isarray/)

```js
var evens = [2,4,6,8,10];
console.log(Array.isArray(evens));
```

#### Array.prototype.indexOf

`Array.prototype.indexOf` returns the index of an object in the array, if it exists, and `-1` otherwise.

**Replaces:** [`_.indexOf`](http://underscorejs.org/#indexOf), [`$.inArray`](http://api.jquery.com/jquery.inarray/)

```js
var sites = ['twitter.com', 'facebook.com', 'cnn.com'];
console.log(sites.indexOf('facebook.com'));
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