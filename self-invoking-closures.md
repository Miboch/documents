# Creating a global closure to isolate your code.

Although seen less commonly in more modern JavaScript due to the introduction of Modules, a technique commonly seen used in JavaScript is wrapping all of your code inside of an anonymous function creating a pseudo-namespace for your code:

This has several advantages:
 - It isolates your code from exposing itself directly, so it cannot easily be tampered with simply by typing in the global scope in console.
 - It insulates you against accidentally overwriting variables.
 - You can enable strict-mode inside of your scope, without affecting anything else on your page.

**This technique can be broken down in two concepts**
 - Anonymous Functions
 - Immediate or self-invoking.

 ## Anonymous functions
 An anonymous function is merely a function without a label declaration. You have likely encountered them in a callback before
```js
// anonymous function, because it has no label declaring it
function() {

}

// anonymous lambda function
() => {}

// non-anonymous function
function foo() {

}

// non-anonymous lambda: is assigned to bar.
const bar = () => {}

```

## Immediately Invoking
Now, usually to call a function you just need to type its name followed by brackets `()`.
```js
function foo() {
  // function code...
}
foo() // invoke foo.
```

However this is obviously not possible in an anonymous function because it has no label to refer to it. However, this can be solved by wrapping the function, in brackets.
```js
(function() {

})

(() => {})
```

This bracket notation allows us to immediately invoke the function, since the brackets have a higher precedence. So, now that we have the function wrapped, we merely add another set of brackets to invoke the function after it is being declared inside the first brackets, which gives us the final notation:

```js
// function
(function() {

})();

// lambda
(() => {

})();
```

And there we have it. Wrapping your code in an anonymous function like this will allow you to have a completely isolated space for your code.