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


