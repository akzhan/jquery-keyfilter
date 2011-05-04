# Introduction

This [jQuery](http://jquery.com/) plugin filters keyboard input by specified regular expression.

Source code inspired by [Ext.JS](http://www.sencha.com/products/extjs/) (*Ext.form.TextField*, *Ext.EventManager*), but was modified to provide more accurate logic.

## Procedural style

`$('#ggg').keyfilter(/[\dA-F]/);`

Also you can pass test function instead of regexp. Its arguments:

* this - HTML DOM Element (event target).
* c - String that contains incoming character.

`$('#ggg').keyfilter(function(c) { return c != 'a'; });`

## CSS class attribute style

`<input type="text" class="mask-num" />`

### Predefined classes with its regexps

* mask-pint: `/[\d]/`
* mask-int: `/[\d\-]/`
* mask-pnum: `/[\d\.]/`
* mask-num: `/[\d\-\.]/`
* mask-hex: `/[0-9a-f]/i`
* mask-email: `/[a-z0-9_\.\-@]/i`
* mask-alpha: `/[a-z_]/i`
* mask-alphanum: `/[a-z0-9_]/i`

## Extensibility

Keyfilter supports extending and changing of list of provided masks.

### Example of extending

`/*
 * Key filter masks for hosting.
 */

(function($)
{
var hostingMasks = {
         dir: /[a-z0-9_\/\-\.]/i,
         ftpuser: /[a-z0-9_]/
};

$.extend($.fn.keyfilter.defaults.masks, hostingMasks);

})(jQuery);`

### Override built-in masks to allow french accents

`/*
 * Key filter masks supporting french accents.
 */

(function($)
{
$.extend($.fn.keyfilter.defaults.masks, {
        alpha:    /[a-zéèçàêoe_]/i,
        alphanum: /[a-zéèçàêoe0-9_]/i
});

})(jQuery);`

