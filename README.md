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
* use autoprefixer
* `em` everywhere

```css
.foo,
.bar,
.baz {
  font-size: 1em;
  color: #369;
}
```

* BEM

```css
.org-Block
.org-Block--modifier
.org-Block-element
.org-Block-element--modifier
.js-ListenerAction
```

## JavaScript

* Soft-tabs, 2 spaces
* Semicolon-less (One semicolon before new line starting with `(` or `[` thought)
* Comma-first
* Paragraphs of code to ease legibility
* Comment only if the code is not easily understandable
* Double-quotes
* Capitalized constructor names
* Try not to get over 80 chars/line
* Create the smallest functions possible
* Test using tape/testling

```javascript
function each(fn, context){
  var array = this
    , index = -1
    , length = array.length

  while(++index < length) {
    fn.call(context, array[index], index, array)
  }

  return array
}
```

```javascript
function Hash(object){
  var hash = this
    , length
 
  if(!(array instanceof Hash)) {
    return new Hash(object)
  }
  extend(array, object, true)
  length = object.length
  if(object) {
    array.length = length
  }
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
doctype html
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
* `/.rtl &` for reversed language
* `unit(em/@font-size, em)` for legacy `rem`

```stylus
.foo
.bar
.baz 
  @extend .foo
  font-size: 1em
  color: #369
```
