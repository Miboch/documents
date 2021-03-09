JavaScript Property Accessors
---
When utilizing Objects in JavaScript there are two main ways of accessing their properties.
- Dot-Notation
- Bracket-Notation

In this brief writeup we will have a look at these two methods and go over their differences, as well as examining how `Object.keys()` can be utilized in conjunction with Bracket-Notation to loop over an object's properties to access each one.

## The anatomy of an object
In Javascript, an object in the most basic terms consist of two things:
 - A block.
 - An Identifier, with an associated value.

> *A block in JavaScript is defined by a pair of curly braces `{}`*

So, this means that an object is given as the following:
```javascript
{
  identifier: value
}
```
*a block containing an identifier, with an associated value*

**The Identifier**

The identifier, also sometimes referred to as the key, can be any valid javascript string.

**The Value**

The value, defined after the `:` symbol following an identifier, can be any valid JavaScript type, such as Objects, Functions, Numbers, Strings, booleans, etcetera.


__hold up. Property, Key or Identifier, what's the difference?__

The terminology is sometimes mixed, but they generally refer to the same thing, which is some string/label present on a block, before the `:` and value.

The name `key` instead of property, originates from the general data structure of a [dictionary](https://en.wikipedia.org/wiki/Associative_array). In JavaScript you do not have a specific Dictionary type, and in lieu of this utilize Objects, because they essentially behave in the same manner.

Because of this, `identifiers` are sometimes called `keys`.

## The Test Object
So now that we know what an object consists of, we'll define one with a couple of identifiers and some associated values.

```javascript
const testObject = {
   property1: "Property 1 value",
   property2: "Property 2 value",
   property3: "Property 3 value"
}
```
Having defined an object we now have a new problem, and that is: How do we access the values stored within it, and that is what this write-up is about.

## Dot-Notation
We want to access a property inside of our testObject using dot-notation. This is done very simply by utilizing the variable name which stores the reference to our object, followed immediately by a `.` which is then followed immediately by the `identifier`. Suppose we want to access `property1` on `testObject` then we would write the following:

```js
testObject.property1 // accessing property1 on testObject.
```
This would give us the value stored in property1, in this case "Property 1 value".

If we ran that code, nothing would happen simply because we are accessing the value stored in property1, but we are not doing anything with it. Let's try to log the value to the console:
```js
console.log(testObject.property1) // logs 'Property 1 value'
```

### Properties that cannot be accessed with Dot Notation
So why do we even have more than one way of accessing properties? The title is a spoiler. There are certain types of property names which cannot be accessed using dot-notation.

Suppose we had extended our testObject, so it now looked like this:

```javascript
const testObject = {
   property1: "Property 1 value",
   property2: "Property 2 value",
   property3: "Property 3 value",
   1: "Property '1' value"
}
```
If we wanted to access the property `1` on our `testObject` we need a different way of accessing it, as `testObject.1` will not work.

It may seem a little arbitrary why this is, and that is because it is an arbitrary limitation. The original language designers of JavaScript simply chose this limitation. There probably was a good reason for this choice, but I haven't been able to sleuth up any concrete answer for you, so for now you'll have to accept it as simply being a limitation on JavaScript, because that is how JavaScript was made.

And so, this brings us to Bracket-Notation.

## Bracket-Notation
Generally speaking the anatomy of a Bracket-Notation accessor is given by writing the label for the object - that is, the variable which stores the reference to it followed by two square brackets `[]` and within the square brackets you provide a string, which matches any of the object's identifiers.

```javascript
objectVariable['identifier']`  // the variable which references the object can be called its 'label'.
```

For our `testObject` the label is `testObject` and the identifiers are `property1, property2, property3, and 1`

```javascript
const testObject = {
   property1: "Property 1 value",
   property2: "Property 2 value",
   property3: "Property 3 value",
   1: "Property '1' value"
}
```

accessing the value of identifier `1` would look like this:
```javascript
// accessing identifier '1' on testObject
console.log(testObject['1']) // logs "Property '1' value"
```

### Identifiers with spaces
Not only is it possible to use numbers for property names when using the square bracket notation for accessing properties, it is also possible to create and access properties with spaces in their names
```js
testObject["property with space"] = "A new property";
```

The above line would create a new property on `testObject` with the identifier `property with space`.

## Similarities with Array Index
You might have seen the Square-Bracket notation before, when working with arrays.
```js
let testArray = ["value of index 0", "value of index 1", "value of index 2"];
let otherObject = {
   0: "value of identifier 0",
   1: "value of identifier 1",
   2: "value of identifier 2"
}
```
given the above code, you could access `testArray` and `otherObject` using similar syntax

```js
testArray[0] // returns 'value of index 0'
otherObject[0] // returns 'value of identifier 0'
```

However, even though the access syntax is similar, it is important to note there are distinct differences between accessing an index in an array, and accessing a property on an object using Square-Bracket notation.

**For an Array**

An array can be accessed using a number to indicate which `index` you want to retrieve. These will always be numbers, and cannot have arbitrary string values, like an object can.

**For an Object**
Even though we used a `number type` to access the 0 identifier on `otherObject` JavaScript is actually transforming that 0 into a string behind the scenes.

Another distinction is that objects by themselves are not iterable (that means, you cannot loop through their values) in the same way as you can with an array. There are however helpful methods in the standard library which helps with this, and we will look at one of those now.


## Object.Keys
JavaScript gives us a handy default method on the Object (note the capitalized O) prototype, which is the `keys()` method.

The `keys()` method accepts an object as an argument, and returns an array with all the identifiers for that object.

Given the following object
```javascript
const testObject = {
   property1: "Property 1 value",
   property2: "Property 2 value",
   property3: "Property 3 value",
   1: "Property '1' value"
}
```

calling `Object.keys()` with `testObject` as an argument would return an array with `property1, property2, property3, and 1` as strings, which would look like this:

```javascript
Object.keys(testObject) // returns ['property1','property2','property3','1']
```

Now, this is quite handy in some cases where you wish to go through every property on a given object. Let's say I wanted to replace every property on our testObject with the string `"Loops are fun"`

If I used Dot-Notation. I would have to go through the object manually for each identifier:
```javascript
testObject.property1 = "Loops are fun"
testObject.property2 = "Loops are fun"
...
```

However, since we have Bracket-notation, and a way of getting every identifier on an object, this can be done much more efficiently using a loop.

```javascript
let identifiers = Object.keys(testObject);
for(let i = 0; i < identifiers.length; i++) {
  testObject[identifiers[i]] = "Loops are fun"
}
```
The above example is a little contrived, but the technique is generally applicable to any object where you have a task that must be repeated across many properties that have a like structure.

## Advanced Example: Filtering values on every array within an object.
Putting together everything we've gone through, let's look at a scenario where we have an object `filterContainer`, which contains multiple arrays.

```js
const exampleObject = {
   arr1: [1,2,3,4,5,6,7,8,9,10],
   arr2: [1,2,3,4,5,6,7],
   notIterable: "How dare you try to iterate over me, Sir and or Madam! In my family, we do not iterate!"
}
```
given the above code, we would like to go through each property on `exampleObject` and filter out every number below 5 on both `arr1` and `arr2`

Now, since we know the names of all the properties, we could just write the following code:
```js
exampleObject.arr1 = exampleObject.arr1.filter(num => num >= 5)
exampleObject.arr2 = exampleObject.arr2.filter(num => num >= 5)
```

However, that is a little boring, let's instead assume we do not know the names of the properties on our object:

```js
// first we get all the keys on our object
const keys = Object.keys(exampleObject);
// then we iterate - this time with a for-of loop. This style of loop is useful if you have to go over an entire collection. The For-Of syntax is convenient if you do not need to do anything fancy with the iterator, as it is slightly less typing, and it is more convenient accessing the current element, which will be stored in `key` rather than having to access keys[i].
for(let key of keys) {
   exampleObject[key] = exampleObject[key].filter(num => num >= 5);
}
```
Done right? Well you probably noticed that there is a problem. We are trying to call `.filter()` on every property on `exampleObject` but `.filter()` is a method which exists on the [array prototype](https://developer.mozilla.org/tr/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

this means, when our code attempts to call `exampleObject['notIterable'].filter(num => num >= 5)` it will fail.

So, we need to change our code a little bit:
```js
const keys = Object.keys(exampleObject);
for(let key of keys) {
   if(exampleObject[key] instanceof Array) {
      exampleObject[key] = exampleObject[key].filter(num => num >= 5);
   }
}
```

And there we have it, utilizing `Object.keys()` we have gone over every array on an object and filtered out all numbers below 5.