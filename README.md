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
console.log(Object.keys(dog)); // ["name", "breed"]
```

#### Object.create

`Object.create` returns a new object with the specified prototype and properties.

```js
var Dog = function () {};
Dog.prototype.bark = function () {
console.log('Bark!');
};
var rover = Object.create(Dog.prototype);
rover.bark(); // Bark!
```

#### Object.getOwnPropertyNames

`Object.getOwnPropertyNames` returns an array of all properties of an object, enumerable or not.

```js
var person = Object.create({}, {
name: { value: 'John Rockefeller', enumerable: true},
netWorth: { value: 1000000, enumerable: false }
});
console.log(Object.keys(person)); // ["name"]
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

#### Object.seal

`Object.seal` prevents new properties from being added to an object and prevents existing properties from being modified if they're not writable.

```js
var book = {
name: 'Great Gatsby'
};

Object.seal(book);
book.name = 'The Great Gatsby';
book.author = 'F. Scott Fitzgerald';
console.log(book.name, book.author); // "The Great Gatsby", undefined
```

#### Object.freeze

`Object.freeze` effectively makes an object immutable: no properties can be added and existing properties can't be modified.

```js
var book = {
name: 'Great Gatsby'
};

Object.freeze(book);
book.name = 'The Great Gatsby';
book.author = 'F. Scott Fitzgerald';
console.log(book.name, book.author); // "Great Gatsby", undefined
```

#### Object.preventExtensions

`Object.preventExtensions` marks an object as no longer extensible, so that new properties can't be added to it. Properties can still be added through the prototype, however.

```js
var book = {};
Object.preventExtensions(book);
book.name = 'The Great Gatsby';
console.log(book.name); // undefined
```

### Array

#### Array.isArray

`Array.isArray` returns `true` if an object is an array and `false` otherwise.

**Replaces:** [`_.isArray`](http://underscorejs.org/#isArray), [`$.isArray`](http://api.jquery.com/jquery.isarray/)

```js
var evens = [2, 4, 6, 8, 10];
console.log(Array.isArray(evens)); // true
```

#### Array.prototype.indexOf

`Array.prototype.indexOf` returns the index of the first occurrence of an object in the array, if it exists, and `-1` otherwise.

**Replaces:** [`_.indexOf`](http://underscorejs.org/#indexOf), [`$.inArray`](http://api.jquery.com/jquery.inarray/)

```js
var sites = ['fb.com', 'twitter.com' 'fb.com'];
console.log(sites.indexOf('fb.com')); // 0
```

#### Array.prototype.lastIndexOf

`Array.prototype.lastIndexOf` returns the index of the last occurrence of an object in the array, if it exists, and `-1` otherwise.

**Replaces:** [`_.lastIndexOf`](http://underscorejs.org/#lastIndexOf)

```js
var sites = ['fb.com', 'twitter.com' 'fb.com'];
console.log(sites.lastIndexOf('fb.com')); // 2
```

#### Array.prototype.every

`Array.prototype.every` returns `true` if all elements of an array pass a user-specified test and `false` otherwise.

**Replaces:** [`_.every`](http://underscorejs.org/#every)

```js
var numbers = [1, 2, 3, 4, 5];
var allNumbers = numbers.every(function (el) { return !isNaN(el); });
console.log(allNumbers); // true
```

#### Array.prototype.some

`Array.prototype.some` returns `true` if some elements of an array pass a user-specified test and `false` otherwise.

**Replaces:** [`_.some`](http://underscorejs.org/#some)

```js
var string = 'es57'.split('');
var someNumbers = string.some(function (el) { return !isNaN(el); });
console.log(someNumbers); // true
```

#### Array.prototype.map

`Array.prototype.map` returns a **new** array with all elements modified by the provided function.

**Replaces:** [`_.map`](http://underscorejs.org/#map), [`$.map`](http://api.jquery.com/jquery.map/)

```js
var numbers = [1, 2, 3, 4, 5];
var squares = numbers.map(function (n) { return n * n; });
console.log(squares); // [1, 4, 9, 16, 25]
```

#### Array.prototype.filter

`Array.prototype.filter` returns a **new** array with only those elements that pass a user-specified test.

**Replaces:** [`_.filter`](http://underscorejs.org/#filter)

```js
var numbers = [1, 2, 3, 4, 5];
var odds = numbers.filter(function (n) { return n & 1; });
console.log(odds); // [1, 3, 5]
```

#### Array.prototype.forEach

`Array.prototype.forEach` executes a function for each element in the array.

**Replaces:** [`_.each`](http://underscorejs.org/#each), [`$.each`](http://api.jquery.com/jquery.each/)

```js
var numbers = [1, 2, 3, 4, 5];
numbers.forEach(function (exp, index) {
numbers[index] = Math.pow(2, exp);
});
console.log(numbers); // [2, 4, 8, 16, 32]
```

#### Array.prototype.reduce

`Array.prototype.reduce` returns the value resulting from accumulating the results of a user-specified function applied left to right on an array's elements.

```js
var numbers = [1, 2, 3, 4, 5];
var sum = numbers.reduce(function (prev, curr) {
return curr < 3 ? prev + curr : prev * 2;
}, 0);
console.log(sum); // 24
```
#### Array.prototype.reduceRight

`Array.prototype.reduceRight` returns the value resulting from accumulating the results of a user-specified function applied right to left on an array's elements.

```js
var numbers = [1, 2, 3, 4, 5];
var sum = numbers.reduceRight(function (prev, curr) {
return curr < 3 ? prev + curr : prev * 2;
}, 0);
console.log(sum); // 3
```

### String

#### String.prototype.trim

`String.prototype.trim` returns a string with whitespace characters stripped from the start and finish.

**Replaces:** [`$.trim`](http://api.jquery.com/jQuery.trim/)

```js
var message = '   Hello World  ';
console.log(message.trim()); // "Hello World"
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
var elvis = identify.bind({name: "Elvis"});

console.log(anonymous()); // "I have no name"
console.log(elvis()); // "Name's Elvis"
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
console.log(y); // "{"a":"foo","b":"bar"}"
console.log(z);
```

#### `undefined`

In ECMAScript 5, `undefined` is immutable.

```js
var undefined = 123;
console.log(undefined); // undefined
```