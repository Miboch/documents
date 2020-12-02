Quick introductionary document to localStorage
--
Localstorage is a very simple browser API which stores values using a key-value-pair system. LocalStorage is available on the global Window object, so you can access it easily and anywhere in your browser context.

## Methods to use
To be able to work with localStorage we need to be able to do two things

- save data
- retrieve data.

**saving data**

Observe the following code snippet:

```js
const name = "Hamill Jacobson";
localStorage.setItem('name', name);
```

This block of code will store the value of the `name` const under the key 'name' in localStorage.

**Retrieving Data**

On a subsequent visit, we could then retrieve the data simply by doing the following:
```js
const name = localStorage.getItem('name'); // Hamill Jacobson
```

# A few things to note

The localStorage API will return a string, so if you want to store JSON, you need to wrap the calls with the `JSON.stringify()` and `JSON.parse()` methods.

- Stringify JSON when setting
- parse it back into JSON getting.

Doing so could look something like this:

```js
// somewhere in your code...
localStorage.setItem('myStorageKey', JSON.stringify(myDataVariable));
// some other place in your code, where you would re-initialize your data from storage
const myDataVariable = JSON.parse(localStorage.getItem('myStorageKey'));
```

### Small Exercise
Here is a small sample exercise to let you try things out: Provided is a bit of code which will select two elements from the document: A text input and a button.
The objective is now to make the text input remember whatever input it held when the save button was clicked.

```js
function loadFromStorage(key) {
  // implement
}

function saveToStorage(key, value) {
  // implement
}

(() => {
  const inputElement = document.querySelector("#saveVal")
  const saveButton = document.querySelector("#save");
  
  document.addEventListener('DOMContentLoaded', () => {
    inputElement.value = loadFromStorage('saved');
  });
  saveButton.addEventListener('click', () => saveToStorage('saved', inputElement.value));
})();

```

```html
<html>
  <head></head>
  <body>
    <input type="text" id="saveVal">
    <button id="save">Save input in localStorage</button>

    <script>
      // copy the script here and implement your solution.
    </script>

  </body>
</html>
```

### Extended Edition
Expand the previous solution to store/retrieve a JSON object and populate 2 or 3 input fields with the corresponding data from each property on the object.

*hint:* remember to use `JSON.parse()` and `JSON.stringify()`