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

#### Object.getPrototypeOf

`Object.getPrototypeOf` returns the `[[Prototype]]` property of the object, i.e. the object instantiated to create the current object.

```js
var Site = function (url) { this.url = url; };
var github = new Site('http://github.com');
var obj = github;

while(obj) {
obj = Object.getPrototypeOf(obj);
console.log(obj);
}
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

`Array.prototype.indexOf` returns the index of the first occurrence of an object in the array, if it exists, and `-1` otherwise.

**Replaces:** [`_.indexOf`](http://underscorejs.org/#indexOf), [`$.inArray`](http://api.jquery.com/jquery.inarray/)

```js
var sites = ['fb.com', 'twitter.com' 'fb.com'];
console.log(sites.indexOf('fb.com'));
```

#### Array.prototype.lastIndexOf

`Array.prototype.lastIndexOf` returns the index of the last occurrence of an object in the array, if it exists, and `-1` otherwise.

**Replaces:** [`_.lastIndexOf`](http://underscorejs.org/#lastIndexOf)

```js
var sites = ['fb.com', 'twitter.com' 'fb.com'];
console.log(sites.lastIndexOf('fb.com'));
```

#### Array.prototype.every

`Array.prototype.every` returns `true` if all elements of an array pass a user-specified test and `false` otherwise.

**Replaces:** [`_.every`](http://underscorejs.org/#every)

```js
var numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
var allNumbers = numbers.every(function (el) { return !isNaN(el); });
console.log(allNumbers);
```

### Array.prototype.some

`Array.prototype.some` returns `true` if some elements of an array pass a user-specified test and `false` otherwise.

**Replaces:** [`_.some`](http://underscorejs.org/#some)

```js
var string = 'es57'.split('');
var someNumbers = string.some(function (el) { return !isNaN(el); });
console.log(someNumbers);
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

#### Function.prototype.bind

`Function.prototype.bind` returns a **new** function with its context set to the provided object.

**Replaces:** [`_.bind`](http://underscorejs.org/#bind), [`$.proxy`](http://api.jquery.com/jquery.proxy/)

```js
function identify() {
return this.name ? "Name's " + this.name : "I have no name";
};

var anonymous = identify;
var elvis = identify.bind({name: 'Elvis, thank you very much'});

console.log(anonymous());
console.log(elvis());
```

#### Date.now

`Date.now` returns the number of milliseconds since January 1st, 1970.

**Replaces:** [`_.now`](http://underscorejs.org/#now), [`$.now`](http://api.jquery.com/jQuery.now/)

```js
console.log(Date.now());
```

#### JSON

`JSON.stringify` returns a string representation of a JavaScript object serialized as JSON. `JSON.parse` deserializes a string into a JavaScript object.

**Replaces:** [JSON2](https://github.com/douglascrockford/JSON-js), [JSON 3](http://bestiejs.github.io/json3/)

```js
var x = {a: 'foo', b: 'bar'};
var y = JSON.stringify(x);
var z = JSON.parse(y);
console.log(y);
console.log(z);
```