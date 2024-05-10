# CSS Refresher Notes

This is a quick refresher of CSS concepts compiled from various articles online. Contributions are always welcome :)

I have linked to most of the articles used, sorry if I missed any. Huge thanks to the community!

**Table of Contents**

- [Positioning](#positioning)
- [Display](#display)
- [Floats](#floats)
- [CSS Selectors](#css-selectors)
- [Selector efficiency](#selector-efficiency)
- [Repaints and Reflows](#repaints-and-reflows)
- [CSS3 Properties](#css3-properties)
- [CSS3 Media queries](#css3-media-queries)
- [Responsive Web Design](#responsive-web-design)
- [CSS3 Transitions](#css3-transitions)
- [CSS Animations](#css-animations)
- [Scalable Vector Graphics (SVG)](#scalable-vector-graphics-svg)
- [CSS Sprites](#css-sprites)
- [Vertical Alignment](#vertical-alignment)
- [Known Issues](#known-issues)




## Positioning

CSS Position allows up to 5 different values. But essentially only 4 values are commonly used.

```css
div {
  position: static; /* default */
  position: relative;
  position: absolute;
  position: fixed;
  position: sticky;
  position: inherit; /* Not very common */
}
```

**Static (default):**
* The only reason you would ever set an element to position: static is to forcefully-remove some positioning that got applied to an element outside of your control. This is fairly rare, as positioning doesn't cascade.

**Relative:**
* Allows nudging elements in different directions with top, right, bottom and left values. Its starting point is where it normally lies in the flow of the document, not the top left of the page.
* When set to position relative, elements take up the same amount of space at the same exact position it was supposed to take as if its position was static.
* It introduces the ability to use z-index on that element, which doesn't really work with statically positioned elements. Even if you don't set a z-index value, this element will now appear on top of any other statically positioned element.
* It limits the scope of absolutely positioned child elements. Any element that is a child of the relatively positioned element can be absolutely positioned within that block.

**Absolute:**
* Position absolute takes the element out of the document flow. This means that it no longer takes up any space like what static and relative does. Think of it as an element with a giant strip of velcro on its back. Just tell it where to stick and it sticks.
* You use the positioning attributes top, left, bottom and right to set the location. Remember that these values will be relative to the next parent element with relative (or absolute) positioning. If there is no such parent, it will default all the way back up to the html element itself meaning it will be placed relatively to the page itself.
* The trade-off, and most important thing to remember, about absolute positioning is that these elements are removed from the flow of elements on the page. An element with this type of positioning is not affected by other elements and it doesn't affect other elements.

**Fixed:**
* Similar to position absolute, an element that has fixed position is taken out of the document flow.
* The element is positioned relative to the viewport, or the browser window itself.
* Major difference with position absolute is it always takes its positioning relative to the browser window.
* Since the fixed value behaves similar to the absolute value, we can stretch the width of the element to fit the viewport by setting offset values for left and right to zero.

**Sticky:**
* This is a hybrid of relative and fixed positioning.
* The element is treated as relative positioned until it crosses a specified threshold, at which point it is treated as fixed positioning.
* For more info, find the demo from the MDN (https://codepen.io/simevidas/pen/JbdJRZ)

**Inherits:**
* It works as the name implies: The element inherits the value of its parent element. Typically, position property elements do not naturally inherit their parent’s values—the static value is assigned if no position value is given. Ultimately, you can type inherit or the parent element’s value and get the same result.

**Summary**
* Relative positioning will allow you to tweak an element’s position relative to its normal starting point.
* Absolute positioning will allow you to tweak an element’s position relative to its first non-statically-positioned ancestor (defaults to page bounds if none is found).
* Both relatively and absolutely positioned items won’t affect the static and fixed items around them (absolutely positioned items are removed from the flow, relatively positioned items occupy their original position).


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


## Floats
* Floated elements are first laid out according to the normal flow, then taken out of the normal flow and sent as far to the right or left (depending on which value is applied) of the parent element.
In other words, they go from stacking on top of each other to sitting next to each other, given that there is enough room in the parent element for each floated element to sit.
* Generally, a floated element should have an explicitly set width (unless it is a replaced element, like an image). This ensures that the float behaves as expected and helps to avoid issues in certain browsers.
* Non-positioned, non-floated, block-level elements act as if the floated element is not there, since the floated element is out of flow in relation to other block elements. When we use a floated image in a paragraph - the text in the paragraph is inline, so it flows around the floated element.
* The clear property has five values available: left, right, both, inherit, and none. Assigning a value of left says the top edge of this element must sit below any element that has the float: left property applied to it.
* A rule that I have found that works nicely for my layouts is float first. That is, in my HTML, I almost always place my floated elements first in the markup, and before any non-floated elements that my float will interact with,
such as the paragraph in the example above. Most of the time, this gives the desired result.
* Collapsing is when a parent element that contains any number of floated elements doesn’t expand to completely surround those elements in the way it would if the elements were not floated.
* There is a method that allows a parent element to clear itself of any floated elements inside it. It uses a CSS property called overflow with a value of hidden.
Note that the overflow property was not intended for this type of use, and could cause some issues such as hiding content or causing unwanted scrollbars to appear.
* **Trick: For clearing floats adding a ‘overflow:auto’ to the parent element also does the trick.**
* Note that overflow: auto doesn't clear floats — it causes the element to contain its floats by way of establishing a new block formatting context for them so that they don't intrude to other elements in the parent context.
That is what forces the parent to stretch to contain them. You can only clear a float if you add a clearing element after the float. A parent element cannot clear its floating children.
* A better way to clear floats is to add a `clearfix` class to the container element with the following styles
  ```css
  .clearfix:after {
    content: "";
    display: table;
    clear: both;
  }
  ```

**9 Rules governing Floats**

1. Floated elements are pushed to the edge of their containers, no further.

2. Any floated element will either appear next to or below a previous floated element. If the elements are floated left, the second element will appear to the right of the first. If they’re floated right, the second element will appear to the left of the first.

3. A left-floating box can't be further right than a right-floating box.

4. Floated elements can't go higher than their container’s top edge (this gets more complicated when collapsing margins are involved, see original rule).

5. A floated element can't be higher than a previous block level or floated element.

6. A floated element can't be higher than a previous line of inline elements.

7. One floated element next to another floated element can’t stick out past the edge of its container.

8. A floating box must be placed as high as possible.

9. A left-floating box must be put as far to the left as possible, a right-floating box as far to the right as possible. A higher position is preferred over one that is further to the left/right.

**Gotchas**
```html
<img src="http://lorempixum.com/200/200/">
<p>Lorem ipsum...</p>
```
```css
img {
  float: right;
  margin: 20px;
}
```

Any margin that we add to the paragraph is being applied way off to the right of the image. This is because the image is actually inside of the paragraph’s box! This is why it doesn’t increase the space between the image and the paragraph.

*More reading:*

[Everything You Never Knew About CSS Floats](http://designshack.net/articles/css/everything-you-never-knew-about-css-floats/)

[CSS Floats 101](http://alistapart.com/article/css-floats-101)

[Clearing Floats](http://www.sitepoint.com/clearing-floats-overview-different-clearfix-methods/)


## CSS Selectors

```css
div#container > ul {
  border: 1px solid black;
}
```

The difference between the standard X Y and X > Y is that the latter will only select direct children.

```css
ul ~ p {
   color: red;
}
```

This sibling combinator is similar to X + Y, however, it's less strict. While an adjacent selector (ul + p) will only select the first element that is immediately preceded by the former selector, this one is more generalized.
It will select, referring to our example above, any p elements, as long as they follow a ul.

```css
a[href*="google"] {
  color: #1f6053;
}
```

The star designates that the proceeding value must appear somewhere in the attribute's value.

```css
a[href^="http"] {
   background: url(path/to/external/icon.png) no-repeat;
   padding-left: 10px;
}
```

If we want to target all anchor tags that have a href which begins with http, we could use a selector similar to the snippet shown above.

```css
a[href$=".jpg"] {
   color: red;
}
```

Again, we use a regular expressions symbol, $, to refer to the end of a string. In this case, we're searching for all anchors which link to an image -- or at least a url that ends with .jpg

```css
a[data-info~="image"] {
   border: 1px solid black;
}
```

The tilde (~) symbol allows us to target an attribute which has a spaced-separated list of values.

```css
div:not(#container) {
   color: blue;
}
```

This selects all divs, except for the one which has an id of container.

```css
p::first-line {
   font-weight: bold;
   font-size: 1.2em;
}
```

We can use pseudo elements (designated by ::) to style fragments of an element, such as the first line, or the first letter. This works only for **block level elements**.

```css
li:nth-child(3) {
   color: red;
}
```

nth child pseudo classes target specific elements in the stack. It accepts an integer as a parameter, however, this is not zero-based. If you wish to target the second list item, use li:nth-child(2).
We can even use this to select a variable set of children. For example, we could do li:nth-child(4n) to select every fourth list item.

```css
li:nth-last-child(2) {
   color: red;
}
```

What if you had a huge list of items in a ul, and only needed to access, say, the 2nd to the last item out of 10? Rather than doing li:nth-child(8), you could instead use the nth-last-child pseudo class.

```css
li:first-child {
    border-top: none;
}

li:last-child {
   border-bottom: none;
}
```

This is particularly useful when assigning border and padding/margin styles for a table list.

*More reading:*

[The 30 CSS Selectors you Must Memorize](http://code.tutsplus.com/tutorials/the-30-css-selectors-you-must-memorize--net-16048)

[What is a Universal Selector in CSS?](https://www.scaler.com/topics/universal-selector-in-css/)


## Selector efficiency

The following list of selectors is in decreasing order of specificity:
* ID selectors (e.g., #example).
* Class selectors (e.g., .example), attributes selectors (e.g., [type="radio"]) and pseudo-classes (e.g., :hover).
* Type selectors (e.g., h1) and pseudo-elements (e.g., :before).
* Universal selector (*), combinators (+, >, ~, ' ') and negation pseudo-class (:not()) have no effect on specificity. (The selectors declared inside :not() do, however.)

Inline styles added to an element (e.g., style="font-weight:bold") always overwrite any styles in external stylesheets and thus can be thought of as having the highest specificity.

Below is a longer list:
* id (#myid)
* class (.myclass)
* tag (div, h1, p)
* adjacent sibling (h1 + p)
* child (ul > li)
* descendant (li a)
* universal (*)
* attribute (a[rel=”external”])
* pseudo-class and pseudo element (a:hover, li:first)

*More Reading*

[CSS Selectors: Should You Optimize Them To Perform Better?](http://vanseodesign.com/css/css-selector-performance/)




