# Web Design Cookbook

> **Note**: This is a simple repo that contains some css and design related tricks found online. If available, for each snippet a related article or full explanation will be provided through a link.

## Table of Contents

1. [Best practices](#bestpractices)
1. [Performance](#performance)
1. [Fallbacks](#fallbacks)
1. [Layout](#layout)
1. [Contribute](#contribute)
1. [License](#license)

## Best practices

### 1. `line-height` management

Generally speaking: for a paragraph a good `line-height` ranges between 1.5 and 1.7 for most fonts.

- [Digital Ocean](https://www.digitalocean.com/community/tutorials/css-line-height)

```css
.well-readable-paragraph {
  /* ... */
  font-size: 16px;
  line-height: 1.5;
}
```

> [Avoid unexpected results](https://developer.mozilla.org/en-US/docs/Web/CSS/line-height#prefer_unitless_numbers_for_line-height_values) by using unitless line-height.

### 2. User prefer reduced motion

This media feature is used to detect if a user has enabled a setting on their device to minimize the amount of **non-essential motion**.

- [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion)

```css
@media (prefers-reduced-motion: reduce) {
  .animated-element {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

> **Note**: Remember that [no motion isn’t always prefers-reduced-motion](https://css-tricks.com/nuking-motion-with-prefers-reduced-motion/).

## Performance

### 1. Performant naming convention

That's one of the most performant CSS naming convention.

```css
.button {
  ...;
}

/* -- for variants */
.button--primary {
  ...;
}

/* __ for child elements */
.button--primary__icon {
  ...;
}

.button--secondary {
  ...;
}
```

### 2. Use FOUT font rule

Add `font-display: swap` to a @font-face block to opt-in to FOUT on browsers that support it.

- [Full article](https://css-tricks.com/really-dislike-fout-font-display-optional-might-jam/)

```css
@font-face {
  font-family: Roboto;
  src: url(/path/to/fonts/Roboto.woff) format("woff");
  font-weight: 400;
  font-style: normal;

  font-display: swap;
}
```

### 3. Css selectors efficiency

The following is an ordered list of some CSS selectors from fastest to slowest (heaviest).

Keep an eye on it when trying to improve code performance.

```css
/* 1. */  .foo-class {}
/* 2. */  div {}
/* 3. */  header + main {}
/* 4. */  ul > li {}
/* 5. */  ul li
/* 6. */  *
/* 7. */  a[href="https://some-example.com"]
/* 8. */  a:visited
```

### 4. will-change animations optimization

The `will-change` property optimizes animations by letting the browser know which properties and elements are just about to be manipulated, potentially increasing the performance of that particular operation.

- [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/will-change)

```css
.element {
  will-change: transform, opacity;
}
```

## Fallbacks

### 1. Support fallback

The `@support()` feature query can be used to handle CSS properties fallbacks.

- [MDN guide](https://developer.mozilla.org/en-US/docs/Web/CSS/@supports)

```css
.box > * {
  background: red;
}

@supports (display: flex) {
  /* If the property is supported */
  .flex-container > * {
    background: blue;
  }

  .flex-container {
    display: flex;
  }
}

@supports not (display: flex) {
  /* If the property isn't supported */
  .flex-container > * {
    background: green;
  }

  .flex-container {
    display: block;
  }
}
```

### 2. Aspect ratio with fallback

Generate aspect ratio code [here](https://ratiobuddy.com/).

- [Full article](https://dev.to/nikolab/css-aspect-ratio-with-a-fallback-for-old-browsers-3eon)

```css
.box {
  width: 100%;
  aspect-ratio: 1/1;
  border: 1px #ccc solid;
}

@supports not (aspect-ratio) {
  .box {
    padding-top: 100%;
    height: 0;
    position: relative;
    overflow: hidden;
  }
}
```

## Layout

### 1. The stack vs flow

Every direct sibling child element of `.stack` has margin-block-start added to it. The `.flow` uses custom variables and a fallback value.

- [Full article](https://andy-bell.co.uk/my-favourite-3-lines-of-css/?utm_source=tldrnewsletter)

**The stack**

```css
.stack > * + * {
  margin-block-start: 1.5rem;
}
```

**flow**

```css
.flow > * + * {
  margin-block-start: var(--flow-space, 1em);
}
```

### 2. Paragraph characters width

The width of an element can be limited by specifying the number of characters allowed.

```css
.paragraph {
  width: 50ch;
}
```

### 3. Scrollbar space automatic management

A default right space for the scrollbar can be added to the container even when the scroll is not active nor visible.

- [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/scrollbar-gutter)

```css
.container {
  scrollbar-gutter: stable;
}
```

### 4. grid auto-placements

The `grid-auto-flow` property controls how the auto-placement algorithm works, specifying exactly how auto-placed items get flowed into the grid.

- [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-auto-flow)

```css
grid-auto-flow: row | column | dense | row dense | column dense;
```

### 5. Flex-grow 9999 Hack

Makes a flex item behave like it has **two flex grow** values.

- [Full article](https://www.joren.co/flex-grow-9999-hack/)

```css
.container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.item-a {
  flex-grow: 1;
}

.item-b {
  flex-grow: 9999;
  flex-basis: 20em;
}
```

### 6. Inner border radius trick

To calculate the correct border radius of an inner div based on its parent's radius use the following formula.

- [This one is by me](https://github.com/ChrisUser)

```html
<div class="parent-block">
  <div class="child-block" />
</div>
```

```css
.parent-block {
  /* ... */
  border-radius: var(--main-border-radius);
  padding: var(--main-padding);
}

.child-block {
  /* ... */
  /* 
  * Biggest value between the parent's radius minus its padding and
  * half the minimum value between the two.
  */
  border-radius: max(
    calc(var(--main-border-radius) - var(--main-padding)),
    calc(min(var(--main-border-radius), var(--main-padding)) * 0.5)
  );
}
```

## Contribute

- [How to contribute](https://github.com/ChrisUser/.github/blob/main/CONTRIBUTING.md)

## License

MIT License

Copyright (c) 2023 Cristiano Raimondi

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

---

**[⬆ back to top](#table-of-contents)**
