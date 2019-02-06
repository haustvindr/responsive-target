# Responsive target

This is a simple CSS file created by me, which contains a set of CSS rules designed to aid in the creation of responsive website designs. Said rules allows for a very easy and declarative management of the HTML elements visibility in response to the view width.

## So, how does it works?

The rules create a set of 6 different breakpoints for the view width. Each breakpoint has a number of selectors which will set the display property to none in the affected elements.

The breakpoints have been considered and configured based off the most commonly seen view widths through statistics both internal and public. Also, "weird" numbers were discouraged, and an extra wide breakpoint was also added since there's a fine niche for very big screens.

These are the breakpoints defined, and their names in the rules:

| | Size 0 | Size 1 | Size 2 | Size 3 | Size 4 | Size 5 |
|---|---|---|---|---|---|---|
| From | 0px | 601px | 901px  | 1201px | 1501px | 2001px |
| To | 600px | 900px | 1200px | 1500px | 2000px | max    |
| Intended use | Small devices like phones | Tablets, phones in landscape | Transition between tablets and desktops, may appear in both | Windowed desktops | Widescreen desktops | Very big screens

As it can be seen, not only the numbers are round, but they are also configured at regular intervals of 300px, with the exception of the size 5. This makes the breakpoints easily memorized and thus easier to combine with any other custom media query.

The media queries are designed for a mobile-first scenario thus it works mainly with min-width, though max-width is used to correctly limit the upper range of each breakpoint. All possible media are included in the queries by default.

`@media all and (min-width: 1201px) and (max-width: 1500px) ...`

The CSS rules are not defined as classes, but as attributes (via HTML5 _data-*_ custom attributes). This decision was made to unclutter the currently over-abused _class_ attribute, and to provide a more readable element declaration.

There are 4 types of rules:

| Type of rule | Effect in the element |
|---|---|
| size-* | Show the element in these sizes |
| not-size-* | Hide the element in these sizes |
| from-size-* | Show the element from this size up (excluded), and hide it in the smaller ones |
| to-size-* | Show the element up to this size (included), and hide it in the bigger ones |

The **\*** refers to the size itself: _size-1_, _from_size_4_, etc.

The _data-*_ attribute used to define the element visibility is aptly named `data-responsive-target`. Within the values of this attribute any combination of target values can be set, allowing for complex behaviours. Different kind of values may be mixed, but they will be applied following the declarations in the CSS rules thus the end behaviour may be unexpected.

All elements are visible by default, that means you only need to add the responsive targets to elements that will have specific visibility rules. An empty `data-responsive-target` works the same as if there were no attribute at all (always visible).

## Okay? I think I need some examples

Sure. Text is nice but we all want some applied examples!

**Show an element only in size 3**

`<div data-responsive-target='size-3'>...</div>`

**Show an element only in sizes 0, 2 and 3**

`<div data-responsive-target='size-0 size-2 size-3'>...</div>`

**Show an element only in phones and tablets**

`<div data-responsive-target='to-size-2'>...</div>`

**Always show an element, in any size**

`<div>...</div>`
`<div data-responsive-target>...</div>`
`<div data-responsive-target='size-0 size-1 size-2 size-3 size-4 size-5'>...</div>`
`<div data-responsive-target='from-size-0'>...</div>`

**Hide an element from normal and widescreen desktops**

`<div data-responsive-target='not-size-3 not-size-4'>...</div>`

**This will have unexpected results due to the declarations' priority**

`<div data-responsive-target='to-size-2 size-4'>...</div>`

## I have more questions

I provide details about the implementation and a one-stop complex example [at the wiki](https://github.com/haustvindr/responsive-target/wiki).
