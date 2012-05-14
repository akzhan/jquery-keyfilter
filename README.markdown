# Introduction

This [jQuery](http://jquery.com/) plugin filters keyboard input by specified regular expression.

Source code inspired by [Ext.JS](http://www.sencha.com/products/extjs/) (*Ext.form.TextField*, *Ext.EventManager*), but was modified to provide more accurate logic.

## Procedural style

```javascript
$("#ggg").keyfilter(/[\dA-F]/);
```

Also you can pass test function instead of regexp. Its arguments:

* this - HTML DOM Element (event target).
* c - String that contains incoming character.

```javascript
$("#ggg").keyfilter(function(c) { return c != 'a'; });
```

## CSS class attribute style

```html
<input type="text" class="mask-num" />
```

Inputs with CSS classes like this will automatically have the corresponding regexp below applied.

### Predefined classes with its regexps

* mask-pint: `/[\d]/`
* mask-int: `/[\d\-]/`
* mask-pnum: `/[\d\.]/`
* mask-num: `/[\d\-\.]/`
* mask-hex: `/[0-9a-f]/i`
* mask-email: `/[a-z0-9_\.\-@]/i`
* mask-alpha: `/[a-z_]/i`
* mask-alphanum: `/[a-z0-9_]/i`

### Using different classes

You can apply these standard regexps to different classes if you wish.

```javascript
$("input.integer").keyfilter($.fn.keyfilter.defaults.masks.int)
```

## Extensibility

Keyfilter supports extending and changing of list of provided masks.

### Example of extending

```javascript
/*
 * Key filter masks for hosting.
 */

(function($)
{
  var hostingMasks = {
    dir: /[a-z0-9_\/\-\.]/i,
    ftpuser: /[a-z0-9_]/
  };

  $.extend($.fn.keyfilter.defaults.masks, hostingMasks);

})(jQuery);
```

### Override built-in masks to allow french accents

```javascript
/*
 * Key filter masks supporting french accents.
 */

(function($)
{
  $.extend($.fn.keyfilter.defaults.masks, {
    alpha:    /[a-zéèçàêoe_]/i,
    alphanum: /[a-zéèçàêoe0-9_]/i
  });
})(jQuery);
```

## Overriding
 
You can fully override masks by simple assignment after the plugin loads but before the `document.ready` event fires.

```javascript
$.fn.keyfilter.defaults.masks = { ... };
```
