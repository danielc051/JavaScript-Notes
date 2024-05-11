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

