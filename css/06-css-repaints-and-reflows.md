## Repaints and Reflows

**Repaint**

Also known as redraw - is what happens whenever something is made visible when it was not previously visible, or vice versa, without altering the layout of the document. An example would be when adding an outline to an element, changing the background color, or changing the visibility style. Repaint is expensive in terms of performance, as it requires the engine to search through all elements to determine what is visible, and what should be displayed.

**Reflow**

A reflow is a more significant change. This will happen whenever the DOM tree is manipulated, whenever a style is changed that affects the layout, whenever the className property of an element is changed, or whenever the browser window size is changed. The engine must then reflow the relevant element to work out where the various parts of it should now be displayed. Its children will also be reflowed to take the new layout of their parent into account. Elements that appear after the element in the DOM will also be reflowed to calculate their new layout, as they may have been moved by the initial reflows. Ancestor elements will also reflow, to account for the changes in size of their children. Finally, everything is repainted.

Reflows are very expensive in terms of performance, and is one of the main causes of slow DOM scripts, especially on devices with low processing power, such as phones. In many cases, they are equivalent to laying out the entire page again.

**Minimal reflow**

Normal reflows may affect the whole document. The more of the document that is reflowed, the longer the reflow will take. Elements that are positioned absolutely or fixed, do not affect the layout of the main document, so if they reflow, they are the only thing that reflows. The document behind them will need to repaint to allow for any changes, but this is much less of a problem than an entire reflow.

So if an animation does not need to be applied to the whole document, it is better if it can be applied only to a positioned element. For most animations, this is all that is needed anyway.

*What causes a reflow*

* Resizing a window.
* Changing the font.
* Adding or removing a stylesheet.
* Content changes, such as a user typing text in an input box.
* Activation of CSS pseudo classes such as :hover (In IE the activation of the pseudo class of a sibling).
* Manipulating the class attribute.
* A script manipulating the DOM
* Calculating offsetWidth and offsetHeight
* Setting a property of the style attribute.

For a comprehensive list of what forces reflows - check Paul Irish's gist [here](https://gist.github.com/paulirish/5d52fb081b3570c81e3a)

**How to minimize the effect of reflows on performance**

* Change classes on the element you wish to style (as low in the DOM tree as possible).
* Avoid setting multiple inline styles.
* Apply animations to elements that are position fixed or absolute.
* Trade smoothness for speed.
* Avoid tables for layout. Even a minor change to a cell will cause reflows on all other nodes of the table.
* Avoid JavaScript expressions in the CSS (IE only).

**Note**

* Sweating over the selectors used in modern browsers is futile. Most selection methods are now so fast it’s really not worth spending much time over. Furthermore, there is disparity across browsers of what the slowest selectors are anyway. Look here last to speed up your CSS.
* Excessive unused styles are likely to cost more, performance wise, than any selectors you chose so look to tidy up there second. 3000 lines that are unused or surplus on a page are not even that uncommon. While it’s common to bunch all the styles up into a great big single styles.css, if different areas of your site/web application can have different (additional) stylesheets added (dependency graph style), that may be the better option.

*More Reading*

[Reflows & Repaints: CSS performance making your JavaScript slow?](http://www.stubbornella.org/content/2009/03/27/reflows-repaints-css-performance-making-your-javascript-slow/)

[Writing efficient CSS selectors](http://csswizardry.com/2011/09/writing-efficient-css-selectors/)

[Why do browsers match CSS selectors from right to left?](http://stackoverflow.com/questions/5797014/why-do-browsers-match-css-selectors-from-right-to-left)

[CSS performance revisited: selectors, bloat and expensive styles](http://benfrain.com/css-performance-revisited-selectors-bloat-expensive-styles/)
