## JavaScript guidelines

Fork it [there](https://github.com/mlbli/js-guidelines) and send a pull request to add your contribution. 

### General

* Keep your sources clean and legible. 
  * Keep a regular indentation.
  * Keep `""` **OR** `''` but not both.
* Use variable names that make sense.
* Remember that semicolons are **optional** in JavaScript. 
  In case you rely on ASI : 
    * `;` before new lines starting with `(` & `[`. 
* Constructor names should be capitalized.
  
```javascript
function Person(name){
  this.name = name
}
```

* Make your constructors safer (prevent the global object from being modified in case of `new` omission).

```javascript
function Person(name){
  if(!(this instanceof Person)) return new Person(name)
  this.name = name
}
```

* Declare functions this way for better readability.

```javascript
function name(){}
```

* Other variables should use a camelized name.
  
```javascript
function scrollToElement(){ /* code here */ }
```

* Use chaining. 

```javascript
myElement.addClass("foo bar").insert("that text")
```

* Only use `eval` for `JSON` parsing legacy support.
  
    **NOTE :** Prefer `new Function` constructor over `eval` in that case. 
   
* Put methods in `constructor.prototype` instead of putting them directly in the object. 
* **NEVER** extend `Object.prototype`. 
* Use the less globals you can :
    * Use a namespace if you have a big project or use JSONP and/or flash interactions. 
    * Lock scopes with self executing anonymous functions. 
* Put your scripts right before `</body>`
* Use a conditionnal `return` statement (as a `continue` or a `break` statement) if the function is not over and you don't need what is following. 

```javascript
function foo(bar){
  if(!bar) return
}
```
  
* Don't use `try{}catch(e){}`.
* Use litterals when possible :
  * `[]` instead of `new Array`
    
    **NOTE** : `Array(n)` can be faster if you know exactly how many items you put inside the created array. 
  * `{}` instead of `new Object`
  * `""` instead of `new String`
* Use `Array.join()` instead of a loop when it fits your needs. 
  
```javascript
"<ul><li>" + ["foo", "bar", "baz"].join("</li><li>") + "</li></ul>"
```

* Extend `Array.prototype`, `Function.prototype`, `String.prototype` in order to make your generic methods (`each`, `map`, `filter` ...) cleaner to call. 
* Set a variable refering to `this` when using it : keeps the reference clear when changing scope & runs faster. 
  
```javascript
function foo(){
  var self = this
  // …
}
```

* Use `Object#hasOwnProperty` to filter methods from properties. 
* Don't use a `string` as first argument of `window.setTimeout` or `window.setInterval`.
* Declare variables in the top of a function with one `var`.
* Always check your globals to ensure you didn't forget a `var` statement or a `,`. 
* `if`, `for`, `while` without curly braces if a single action is performed. 

```javascript
if(foo){
  bar.call(foo)
}

// much more clear
if(foo) bar.call(foo)
```

### DOM

* Use `documentFragment` to manipulate big amounts of nodes before inserting them inside the actual `document`. 

```javascript
var fragment = document.createDocumentFragment()
  , i = 0
  , l = 30
  , elementCache

while(i < l){
  elementCache = document.createElement("p")
  elementCache.id = "element-" + i
  fragment.appendChild(elementCache)
  i++
}

document.body.appendChild(fragment)
```

* Use `className` attribute over `style` when possible (moreover, it simplifies maintenance)

```javascript
myElement.className += "active"
```
  
* Don't repeat yourself (use a `Function#partial` like to reuse a function in different circumstances)

```javascript
function moveTo(direction, amount){
    // some code
    if(direction == 0) amount = -amount
}
var moveLeft = moveTo.partial(0)
  , moveRight = moveTo.partial(1)
```
  
* Use a `window.setInterval` to limit the functions called when `scroll` event is fired. 

```javascript
var isScrollActive = false
  , scrollInterval = window.setInterval(function(){
      isScrollActive = false
      // execute handler
    }, n)

window.addEventListener("scroll", function(){
  isScrollActive = true
})

```

* Don't make your DOM too deep. 
* Use `removeEventListener` and `detachEvent` if you're done with handlers. 
* Cache the elements you reuse. 
* Be careful with `nodeList` which are dynamic. 
* Use `id` attribute when possible to find a unique element (yes, `document.getElementsByClassName("slider")[0]` is less efficient than `document.getElementById("slider")`).


