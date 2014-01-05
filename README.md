# Coding Style Guidelines

HTML, CSS, JavaScript, Jade & Stylus guidelines. 

## HTML

* Double-quotes
* Soft-tabs, 2 spaces

```html
<div class="foo">
  <ul>
    <li>Foo
    <li>Bar
    <li>Baz
  </ul>
</div>
```

## CSS

* Soft-tabs, 2 spaces
* Multiple lines
* One selector by line
* One space before `{`
* One new line after `{`
* One space after `:`
* Three chars hexadecimal when possible

```css
.foo,
.bar,
.baz {
  font-size: 1em;
  color: #369;
}
```

## JavaScript

* Soft-tabs, 2 spaces
* Semicolon-less (One semicolon before new line starting with `(` or `[` thought)
* Comma-first
* Single-line `if`, `for`, `while` and co. if only one action performed (in that case, use no braces)
* Paragraphs of code to ease legibility
* Never comment if the code is easily understandable
* Double-quotes
* Capitalized constructor names
* Use native objects prototypes if more logical
* Use constructors to namespace related methods (i.e. `Array.from`, `Object.typeOf`) 

```javascript
function each(fn, context){
  var self = this
    , index = 0
    , length = self.length

  for(;index < length; index++) fn.call(context, self[index], index, self)

  return self
}
```

```javascript
function Hash(object){
  var self = this
    , length
 
  if(!(self instanceof Hash)) return new Hash(object)
  extend(self, object, true)
  if(object && (length = object.length)) self.length = length
}
```

* Self-executing anonymous functions 

```javascript
;(function(window, document){
  // code here
})(this, this.document)
```

* Use CommonJS module declaration and browserify to build
* Test using [tape](https://github.com/substack/tape)

## Jade

* Soft-tabs, 2 spaces
* Double-quotes

```jade
!!!5
html
  head
    meta(charset="utf-8")
    title Foo
  body
    h1 Hello
```

## Stylus

* Soft-tabs, 2 spaces
* Double-quotes
* Use `:` with one space after

```stylus
.foo
.bar
.baz 
  @extend .foo
  font-size: 1em
  color: #369
```
