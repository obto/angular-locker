angular-locker
==============

> A simple & configurable abstraction for local/session storage in angular projects

[![Build Status](http://img.shields.io/travis/tymondesigns/angular-locker.svg?style=flat)](https://travis-ci.org/tymondesigns/angular-locker)
[![License](http://img.shields.io/badge/license-MIT-blue.svg?style=flat)](http://www.opensource.org/licenses/MIT)

locker will automatically serialize your objects/arrays in local/session storage

## Installation

#### via bower
```
$ bower install angular-locker
```

#### manual

Simply download the zip file [HERE](https://github.com/tymondesigns/angular-locker/archive/master.zip) and include `dist/angular-locker.min.js` in your project.

## Usage

### adding to your project

Add `angular-locker` as a dependency

```js
angular.module('myApp', ['angular-locker'])
```

Configure via `lockerProvider` (*optional*)

```js
.config(function config(lockerProvider) {
	lockerProvider.setStorageDriver('session');
	lockerProvider.setNamespace('myAppName');
}]);
```

inject `locker` into your controller/service/directive etc

```js
.factory('MyFactory', function MyFactory(locker) {
	locker.put('someKey', 'someVal');
});
```

### Adding items to locker

there are several ways to add something to locker:

You can add Objects, Arrays, whatever :)

```js
locker.put('someString', 'anyDataType');
locker.put('someObject', { foo: 'I will be serialized', bar: 'pretty cool eh' });
locker.put('someArray', ['foo', 'bar', 'baz']);
// etc
```

#### adding via function param

Inserts specified key and return value of function

```js
locker.put('someKey', function() {
	var obj = { foo: 'bar', bar: 'baz' };
	// some other logic
	return obj;
});
```

#### adding multiple items at once by passing a single object

This will add each key/value pair as a **separate** item in storage

```js
locker.put({
	'someKey': 'johndoe',
	'anotherKey': ['some', 'random', 'array'],
	'boolKey': true
});
```

#### conditionally adding an item if it doesn't already exist

For this functionality you can use the `add()` method.

If the key already exists then no action will be taken and `false` will be returned

```js
locker.add('someKey', 'someVal'); // true or false - whether the item was added or not
```

----------------------------

### Retrieving items from locker

```js
// locker.put('fooArray', ['bar', 'baz', 'bob']);

locker.get('fooArray'); // ['bar', 'baz', 'bob']
```

#### setting a default value

if the key does not exist then, if specified the default will be returned

```js
locker.get('keyDoesNotExist', 'a default value'); // 'a default value'
```

#### deleting afterwards

You can also retrieve an item and then delete it via the `pull()` method

```js
// locker.put('someKey', { foo: 'bar', baz: 'bob' });

locker.pull('someKey', 'defaultVal'); // { foo: 'bar', baz: 'bob' }

// then...

locker.get('someKey', 'defaultVal'); // 'defaultVal'
```

#### all items

You can retrieve all items within the current namespace

This will return an object containing all the key/value pairs in storage

```js
locker.all();
```

----------------------------

### Checking item exists in locker

You can determine whether an item exists in the current namespace via

```js
locker.has('someKey') // true or false

// e.g.
if (locker.has('user.authToken') ) {
	// we should be logged in right?
} else {
	// go to login page or something
}
```

----------------------------

### Removing items from locker

coming soon...

----------------------------

## API

##### `locker.put(key, value);`

##### `locker.add(key, value);`

##### `locker.get(key, default);`

##### `locker.pull(key, default);`

##### `locker.has(key);`

##### `locker.all();`

##### `locker.remove(key);`

##### `locker.clean();`

##### `locker.empty();`

##### `locker.setStorageDriver(store);`

##### `locker.setNamespace(namespace);`

## Development

Pull requests welcome

```bash
$ npm install
$ bower install
$ gulp
```
