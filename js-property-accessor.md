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

So, this gives us an object as the following:
```javascript
{
  identifier: value
}
```
The identifier can be any valid javascript string, and the value can be anything you can define in JavaScript. A string, number, boolean, function, another object, etcetera.

> When working with objects, their identifiers are often referred to as either properties, or keys.

__hold up. Property, Key or Identifier, what's the difference?__

The terminology is sometimes mixed, but they generally refer to the same thing, which is some string/label present on a block.

The name `key` instead of property, originates from the general data structure of a [dictionary](https://en.wikipedia.org/wiki/Associative_array). In JavaScript you do not have a specific Dictionary type, and in lieu of this utilize Objects, because they essentially behave in the same manner.

Because of this, `properties` are sometimes called `keys`.

## The Test Object
So now that we know what an object consists of, we'll define one for looking closer at how to accessing the values stored within any given identifier.

```javascript
const testObject = {
   property1: "Property 1 value",
   property2: "Property 2 value",
   property3: "Property 3 value"
}
```
With the above object as our starting point, we will look at accessing its properties, first with Dot-Notation, and then with Bracket-Notation.

## Dot-Notation
We want to access a property inside of our testObject using dot-notation. This is done very simply by utilizing the variable name of the object of interest, followed by a `.` then followed by the `identifier`, so suppose we want to access `property1` on `testObject` we would simply write the following:

```js
// accessing testObject.property1 to log.
console.log(testObject.property1) // prints 'Property 1 value'
```

### Properties that cannot be accessed with Dot Notation
So why do we even have more than one way of accessing properties? The title is a spoiler. There are certain property names which cannot be accessed using dot-notation.

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

It may seem a little arbitrary why this is, and that is because it is. The original language designers of JavaScript simply chose this limitation. Likely for a good reason, but none that I've been able to discover by sleuthing through the web for a bit.

And so, this brings us to Bracket-Notation.

## Bracket-Notation
Generally speaking the anatomy of a Bracket-Notation accessor is given as
```javascript
label['identifier']`
```

For our `testObject` the label is `testObject` and the identifiers are `property1, property2, property3, and 1`

If given the same object as before, it is in fact possible to access the `1` property. Instead of using a `.` we use two square brackets `['identifier']` surrounding the identifier, as a string.
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

## Object.Keys
Now for the last point, which is also why I went on a detour talking about Associative Arrays (dictionaries).

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
notice here there is a certain similarity in how you access an array by its index `[number]` and how you use Bracket-Notation to access an identifier on an object. `['identifier']`. However even though they are the same, do not get confused between an object and an array. They are not the same.

The above example is a little contrived, but the technique is generally applicable to any object where you have a task that must be repeated across many properties that have a like structure.
