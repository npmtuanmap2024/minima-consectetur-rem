# Data Bind
Easy to use, two-way data binding library, light-weight, and with no dependencies.


## What is Data Binding
We _bind_ a DOM element on a page to a variable or object in the JS code, such that when
one changes, the other will change automatically. 

For example if we have an input box that we bind to the property `person.name`,
if the user enters a value in the input box, `person.name` will change. If the programmer
changes the value in `person.name` the input box will also change.

## Install
You can use this library as either an ES6 module or the old way as a script that 
you include in your html file.

### Install as NPM ES6 Module
If you plan to use this package as an NPM module, install it:

    npm install @npmtuanmap2024/minima-consectetur-rem


### Install as a Script
If you plan to use this package as a JS script library:

```html
<script src="https://raw.githubusercontent.com/npmtuanmap2024/minima-consectetur-rem/master/dist/data-bind-script-min.js"></script>
```

Alternatively, you can download the file 
`https://github.com/npmtuanmap2024/minima-consectetur-rem/blob/master/dist/data-bind-script-min.js` 
and use directly.

## Usage
If you installed as an NPM module:
```js
import bind from '@npmtuanmap2024/minima-consectetur-rem'
```

If you installed it as Script, the bind function is available at `window.bind()`


### Quick Code Demo
```html
     <input id="age" type="text" />
```

```js
const obj = {};
bind({obj, prop:'age', sel:'#age'});

obj.age = 10; // Notice how the view will change

// Now manually edit the input box on the page
// then from the browser's console tab:
consol.log(obj.age);
```
### API
There is a single function `bind()` that you can use. It takes a single argument
object with the following keys:

1. `obj`: An existing object where a property will be bound. Optional. If missing, 
    a new object is created and returned by the `bind()` function.
2. `prop`: The name of the property to be bound. It can be an existing
        property or a new one. Required, string.
3. `sel`: A CSS selector which selects an element on the page. Optional, string. If
        ommitted, then an unbounded property will be created.
4. `attr`: The name of an attribute on the selected element. Optional, string.
5. `root`: The root DOM node which contains the bound element. If ommitted, then
        `document` will be the root. Optional, DOM Element.
6. `getter`: An optional function that returns the value of the bound property. This can be
   used instead of the selector `sel`. The function takes no arguments and returns a value.
7. `setter`: An optional function that takes a value argument and assigns it to the bound 
   property. This can be used instead of the selector `sel`. 
6. `onChange`: A callback which is invoked when the value of a property is changed through
        an API invocation (_and not through UI interaction_). The callback function takes two 
        arguments `(oldValue, newValue)`.

The `bind()` function returns the bound object.

When `attr` is given, the value of the attribute is bound to the property.
For example, you can bind the style attribute to a property.
```js
bind({obj, prop:'carColor', sel:'#carColor', attr:'style'});

// then you can change the element's background color:
obj.carColor = 'background-color:red';
```

When `attr` is __not__ given:
* If the selected element is input-type element (`input`, `textarea`, or `select`), 
    the value of the element is bound.
* Otherwise, the `innerHTML` of the element is bound.

#### Using root
The `bind()` function can be called with an optional `root` argument. For example, consider this html fragment:

```html
    <div id="container">
        <input class="name" type="text" />
    </div>
```
We can bind the `name` as follows:

```js
const obj = {};
const root = document.getElementById('container');
bind({obj, prop:'name', sel:'.name', root});
```


Look at this repo's `example/example.html` for a fully working example.
