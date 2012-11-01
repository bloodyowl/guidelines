## JavaScript guidelines

Fork it [there](https://github.com/mlbli/js-guidelines) and send a pull request to add your contribution. 

### General

* Keep your sources clean and legible. 
  * Keep a regular indentation.
  * Keep `""` **OR** `''` but not both.
* Use variable names that make sense.
* Constructor names should be capitalized.
  
  ```
  var Person = function(name){
    this.name = name
  }
  ```
  
* Other variables should use a camelized name.
  
  ```
  function scrollToElement(){ /* code here */ }
  ```

* Use chaining. 

   ```
   myElement.addClass("foo bar").insert("that text")
   ```

* Only use `eval` for `JSON` parsing legacy support. 
* Put methods in `constructor.prototype` instead of putting them directly in the object. 
* **NEVER** extend `Object.prototype` or `Element.prototype`. 
* Use the less globals you can :
  * Use a namespace
  * Lock scopes with self executing anonymous functions. 
* Put your scripts right before `</body>`
* Use a conditionnal `return` statement (as a `continue` or a `break` statement) if the function is not over and you don't need what is following. 

  ```
    function foo(bar){
      if(!bar) return;
    }
  ```
  
* Don't use `try{}catch(e){}`.
* Use litterals when possible :
  * `[]` instead of `new Array`
  * `{}` instead of `new Object`
  * `""` instead of `new String`
* Use `Array.join()` instead of a loop when it fits your needs. 
  
  ```
 "<ul><li>" + ["foo", "bar", "baz"].join("</li><li>") + "</li></ul>"
  ```

* Extend `Array.prototype`, `Function.prototype`, `String.prototype` in order to make your generic methods (`each`, `map`, `filter` ...) cleaner to call. 
* Set a variable refering to `this` when using it : keeps the reference clear when changing scope & runs faster. 
* Use `Object#hasOwnProperty` to filter methods from properties.
* Don't use a `string` as first argument of `window.setTimeout` or `window.setInterval`.
* Declare variables in the top of a function.

### DOM

* Use `documentFragment` to manipulate big amounts of nodes before inserting them inside the actual `document`. 

  ```
  var fragment = document.createDocumentFragment(),
  	  i = 0,
  	  l = 30,
  	  elementCache;
  
  while(i < l){
  	elementCache = document.createElement("p")
  	elementCache.id = "element-" + i
    fragment.appendChild(elementCache)
    i++
  }
  
  document.body.appendChild(fragment)
  ```

* Use `className` attribute over `style` when possible (moreover, it simplifies maintenance)

  ```
  myElement.className += "active"
  ```
  
* Don't repeat yourself (use a `Function#curry` like to reuse a function in different circumstances)

  ```
  function moveTo(direction, amount){
    // some code
    if(direction == 0) amount = -amount
  }
  var moveLeft = moveTo.curry(0),
      moveRight = moveTo.curry(1)
  ```
  
* Use a `window.setInterval` to limitate the functions called when `scroll` event is fired. 

  ```
  var isScrollActive = false,
  	  scrollInterval = window.setInterval(function(){
        isScrollActive = false
        // execute handler
      });
  
  window.addEventListener("scroll", function(){
    isScrollActive = true
  })
  
  ```

* Don't make your DOM too deep. 
* Use `removeEventListener` and `detachEvent` if you're done with handlers. 
* Cache the elements you reuse. 
* Be careful with `nodeList` which are dynamic. 
* Use `id` attribute when possible to find a unique element (yes, `document.getElementsByClassName("slider")[0]` is less efficient than `document.getElementById("slider")`).


