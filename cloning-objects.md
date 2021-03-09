Cloning Objects in JS
---
When considering cloning objects in JS, you have to be aware of shallow copying vs. deep copying.

## Shallow Copying
A typical, and straight-forward way of making a shallow copy in JavaScript is by using the [`Object.assign`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) method.

Given the following object
```js
const myObj = {
  prop1: "string",
  prop2: 2,
  prop3: {
    prop1: "another string",
    prop2: 2
  }
}
```
We can create a shallow copy of myObj by using `Object.assign()`

```js
const copy = Object.assign({}, myObj);
```

If we were to `console.log()` copy and myObj, they would look the same. However there is an issue with this approach if you need to mutate the copy, without affecting `myObj` and that is that `prop3` stores an object, which means it did not have its value copied, but the reference to the object copied!

Strictly speaking, you could say that the definition of `myObj` is actaully defining 2 objects, first the outer object which myObj refers to, and another, inner object declared inline:

```js
{
    prop1: "another string",
    prop2: 2
}
```

### Let's examine the problem a little closer to show what is meant by "copying the reference"
Since making a shallow copy creates a reference to the same inner object, changing the inner object in `copy` will also change it in `myObj`

```js
const myObj = {
  prop1: "string",
  prop2: 2,
  prop3: {
    prop1: "another string",
    prop2: 2
  }
}
const copy = Object.assign({}, myObj);
copy.prop3.prop1 = "Changed String";
console.log(myObj.prop3.prop1) // prints "Changed String"!
```
This happens, because `prop3` is not actually the inner object. Instead, it holds a reference which tells JavaScript where to find the inner object in the program memory, so being a shallow copy, both `myObj` and `copy` has the same reference, meaning that the inner object is shared between them.

[Try it on jsfiddle](https://jsfiddle.net/es4gj8w0/)

## Deep Copying
To avoid this issue, you have to create a new object for every object reference within your object, and you have to do this at every level.

Suppose we had an object that was nested more than one level deep

```js
let nestedObjects = {
  firstObject: {
    firstObjectProperty: "hello"
    secondObject: {
      secondObjectProperty: "hello"
    }
  }
}
```
we would then need to create a new reference for both firstObject, and for secondObject, and then copy each value within each of these objects into the new references: 

```js
let copyOfNestedObjects = {
  firstObject: {
    firstObjectProperty: nestedObjects.firstObject.firstObjectProperty,
    secondObject: {
      secondObjectProperty: nestedObjects.firstObject.secondObject.secondObjectProperty
    }
  }
}
```
This can be done a little more suffinctly if we use the spread operator.
```js
let copyofNestedObjects = {
  ...nestedObjects,
  firstObject: {
    ...nestedObjects.firstObject,
    secondObject: {
      ...nestedObjects.firstObject.secondObject
    }
  }
}
```
This however has some disadvantages. First off, it is very cumbersome, secondly it necessitates that we know the structure of our object before-hand.

### One more time, but with recursion
If we look at what steps we need to do in order to deep copy an object they are
 - copy the value of each property from the source onto the target
 - If the property is an object, create a new object to create a new reference

These steps are repeated through the entire object hierarchy, so let's create a function!

```javascript
function deepClone(source) {
  const clone = {}; // create a new object reference
  // assign every property on the source to the clone
  for(let key of Object.keys(source)) {
    clone[key] = source[key];
  }
  return clone;
}
```
the above handles our base-case. However it currently has the same problem as a shallow copy, since it only performs this step on the first object.

To fix this, we simply need to call the deepClone function again, inside of itself, on any property which is an object.

```javascript
function deepClone(source) {
  const clone = {}; // create a new object reference
  // assign every property on the source to the clone
  for(let key of Object.keys(source)) {
    if(typeof source[key] === 'object')
      clone[key] = deepClone(source[key]);
    else
      clone[key] = source[key];
  }
  return clone;
}
```
Now if we perform a clone on our object, we see the behavior we expect, where mutating the clone does not mutate the original

```javascript
let myObject = {
  a: "hello",
  b: "there",
  c: {
    good: "day"
  }
};
let clone = deepClone(myObject);
clone.c.good = "night";
console.log(myObject.c.good); // expect: day
```

## Great but we aren't quite done.
There are still two more things to consider: arrays, and null.

**For null**

The problem with null occurs because we are calling `Object.keys()` to retrieve the keys from source. This is unlikely to be a problem in our first call, as we have to manually pass in the first object, however properties on this object might be null.

Therefore, let's add a guard to our function

```js
function deepClone(source) {
  if(source === null || typeof source != 'object')
    return source;
  ...
}
```
Now even if we call our function with non-objects or null values it will still not break.

```js
  let myObject = {
    a: "hello",
    b: "there",
    c: {
      good: "day"
    },
    d: null
  };
  let clone = deepClone(myObject);
  console.log(clone.d); // expect: null
  ```

Now you might have noticed something a bit off about that guard. We are checking the `typeof source`. This isn't strictly necessary to deal with null properties, but we are doing it to address our second problem: Arrays.


## Arrays
The `deepClone` function has a major defect in its current form in respect to arrays. This is because arrays follow the same reference rules as objects, however more alarmingly, since `Array` is of type `object` all arrays fed into our `deepClone` function will be transformed into objects

```javascript
let myObject = {
	array: [1]
}
let clone = deepClone(myObject);
console.log(clone)
/* RESULT:
clone: {
  array: {
    0: 1
  }
}
*/
```
In order to fix this, we need to add a check in our if-statement to see if the object is an instance of array.
```javascript
function deepClone(source) {
  if(source === null || typeof source != 'object')
    return source;
  if(source instanceof Array) {
  	// we slice the array to make a shallow copy, and then we map each element to a deepClone.
  	return source.slice().map(arrItem => deepClone(arrItem))
  }
  ...
}
```
and this is the reason why we need to return the source, if it is not an object, so that we can utilize our `deepClone` to map the elements of our array into deep clones, otherwise, we would run into issues with arrays holding objects.

This gives us the final version of deepClone:
```javascript
function deepClone(source) {
  if(source === null || typeof source != 'object')
    return source;
  if(source instanceof Array) {
  	// we slice the array to make a shallow copy, and then we map each element to a deepCopy.
  	return source.slice().map(arrItem => deepClone(arrItem))
  }
  const clone = {}; // create a new object reference
  // assign every property on the source to the clone
  for (let key of Object.keys(source)) {
    if (typeof source[key] === 'object')
      clone[key] = deepClone(source[key]);
    else
      clone[key] = source[key];
  }
  return clone;
}
```
and now let's take it for a test-run to verify that it works.
```javascript
let trickyObject = {
  a: "normal string",
  b: null,
  c: [1,2,3],
  d: [{a: "object in array"}]
};
let clone = deepClone(trickyObject);
clone.d[0].a = "overwrite";
console.log(trickyObject.d[0].a) // expect: "object in array"
```

[View on JsFiddle](https://jsfiddle.net/7bjsmg42/)

