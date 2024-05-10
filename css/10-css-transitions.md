## CSS3 Transitions

A CSS transition allows you to change the property of an element over a given duration that you set.

* transition-property: The property to be transitioned (in this case, the background property)
* transition-duration: How long the transition should last (0.3 seconds)
* transition-timing-function: How fast the transition happens over time (ease)

The timing function value allows the speed of the transition to change over time by defining one of six possibilities: *ease, linear, ease-in, ease-out, ease-in-out, and cubic-bezier* (which allows you to define your own timing curve).

You may want the transition to also happen on the :focus or :active pseudo-classes of the link as well. Instead of having to add the transition property stack to each of those declarations, the transition instructions are attached to the normal state and therefore declared only once.

```css
a.foo {
  padding: 5px 10px;
  background: #9c3;
  -webkit-transition: background .3s ease,
    color 0.2s linear;
  -moz-transition: background .3s ease,
    color 0.2s linear;
  -o-transition: background .3s ease, color 0.2s linear;
  transition: background .3s ease, color 0.2s linear;
}
a.foo:hover,
a.foo:focus {
  color: #030;
  background: #690;
}
```

Let’s say that along with the background color, we also want to change the link’s text color and transition that as well. We can do that by stringing multiple transitions together, separated by a comma. Each can have their varying duration and timing functions. An alternative to listing multiple properties is using the all value. This will transition all available properties.

Another basic use of changing states is to change the background of an input box on focus.

```css
input.ourInputBox:focus{
 -webkit-transition:background-color 0.5s linear;
 background:#CCC;
}
```

This time, we put the transition declaration into the hover state, so that we aren’t adding additional unnecessary classes to the CSS. We apply the transition once the input box acquires focus.

*More reading:*

[Understanding CSS3 Transitions](http://alistapart.com/article/understanding-css3-transitions)

[CSS Fundamentals: CSS3 Transitions](http://code.tutsplus.com/tutorials/css-fundamentals-css3-transitions--pre-10922)
