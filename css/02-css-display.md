## Display
Every element on a web page is a rectangular [box](http://www.sitepoint.com/web-foundations/css-box-model/). The display property in CSS determines just how that rectangular box behaves.

```css
div {
	display: inline;
	display: inline-block;
	display: block;
	display: run-in;
	display: none;
}

```
* Default value of all elements is inline. Most "User Agent stylesheets" (the default styles the browser applies to all sites) reset many elements to "block"

**Inline:**
* Default value for elements. Think of elements like span, b or em
* Will ignore top and bottom margin/padding settings, but will apply left and right margin/padding. Only moves horizontally, not vertically.
* Is subject to vertical-align property.
* Will ignore width and height properties.
* If floated left or right, will automatically become a block-level element, subject to all block characteristics.

**Inline Block:**
* Very similar to inline to its parents in that it will set inline with the natural flow of text.
* Very similar to block to its children in that it can have a width and height and its content can move vertically.
* Think of a display:block element that has been rendered (or converted to an image) and then placed in the document inline
* Margin and paddings work properly.
* Width and height will be respected.
* There is a "bug" which causes extra margin in inline block elements. See on [Known Issues](#extra-margin-on-inline-block-elements)

**Block:**
* A number of elements are set to block by the browser UA stylesheet. They are usually container elements such as div, section and ul. Also text 'blocks' like p and h1.
* Block level elements do not sit inline, but break past them. If no width is set, will expand naturally to fill its parent container.
* Can have margins and/or padding.
* If no height is set, will expand naturally to fit its child elements (assuming they are not floated or positioned). So, for a block element, it’s not necessary to give it a set width or to give it a width of 100%.
* Ignores the vertical-align property.

**Run-in:**
* Not supported in Firefox + spec not well defined yet.
* To begin to understand it though, it's like if you want a header element to sit inline with the text below it.

**None:**
* Totally removes the element from the page.
* While the element is still in the DOM, it is removed visually and in any other conceivable way (you can't tab to it or it's children , it is ignored by screen readers etc.)

**Table values:**
* There is a whole set of display values that force non-table elements to behave like table-elements.
* It's rare-ish, but it sometimes allows you to be "more semantic" with your code while utilizing the unique positioning powers of tables.

```css
div {
  display: table;
  display: inline-table; /* like a table inside an inline-block */
  display: table-cell;
  display: table-column;
  display: table-colgroup;
  display: table-header-group;
  display: table-row-group;
  display: table-footer-group;
  display: table-row;
  display: table-caption;
}
```

* To use, just mimic normal table structure. Simple example:
```html
<div style="display: table;">
  <div style="display: table-row;">
    <div style="display: table-cell;">
      Gross but sometimes useful.
    </div>
  </div>
</div>
```

**Flexbox:**
* Aims at providing a more efficient way to lay out, align and distribute space among items in a container, even when their size is unknown and/or dynamic (thus the word 'flex')
* The main idea behind the flex layout is to give the container the ability to alter its items' width/height (and order) to best fill the available space (mostly to accommodate to all kind of display devices and screen sizes).
* A flex container expands items to fill available free space, or shrinks them to prevent overflow.
* Most importantly, the flexbox layout is direction-agnostic as opposed to the regular layouts (block which is vertically-based and inline which is horizontally-based).
* Flexbox layout is most appropriate to the components of an application, and small-scale layouts, while the Grid layout is intended for larger scale layouts.
* As with inline-block and inline-table, there is also inline-flex.

*More reading:*

[Flexbox Froggy](http://flexboxfroggy.com/)

[Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

[Flexbox reference](http://tympanus.net/codrops/css_reference/flexbox/)

**Grid:**
* The grid property in CSS is the foundation of Grid Layout. It aims at fixing issues with older layout techniques like float and inline-block, which both have issues and weren't really designed for page layout.
* Method of using a grid concept to lay out content, providing a mechanism for authors to divide available space for lay out into columns and rows using a set of predictable sizing behaviors.
* Along with the fact this method fixes the issues we encounter with older layout techniques, its main benefit is you can display a page in a way which can differ from the flow order.
* An older deprecated version of the spec is implemented in IE10/11. The current version of the spec is present in all other modern browsers (Chrome, Safari, Firefox, and Edge 16+).
* As with inline-block and inline-table, there is also inline-grid.

*More reading:*

[A Complete Guide to Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)

[Grid Garden](http://cssgridgarden.com/)

[CSS Almanac: Display](https://css-tricks.com/almanac/properties/d/display/)

[The Difference Between “Block” and “Inline”](http://www.impressivewebs.com/difference-block-inline-css/)

[Learn CSS Layout: The "display" property](http://learnlayout.com/display.html)
