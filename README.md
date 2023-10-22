# Web Design Cookbook

> **Note**: This is a simple repo that contains some css and design related tricks found online. If available, for each snippet a related article or full explanation will be provided through a link.

## Table of Contents

1. [Performance](#performance)
1. [Fallbacks](#fallbacks)
1. [Layout](#layout)
1. [Contribute](#contribute)
1. [License](#license)

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

[Full article](https://css-tricks.com/really-dislike-fout-font-display-optional-might-jam/)

```css
@font-face {
  font-family: Roboto;
  src: url(/path/to/fonts/Roboto.woff) format("woff");
  font-weight: 400;
  font-style: normal;

  font-display: swap;
}
```

## Fallbacks

### 1. Support fallback

The `@support()` feature query can be used to handle CSS properties fallbacks.

[MDN guide](https://developer.mozilla.org/en-US/docs/Web/CSS/@supports)

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

[Full article](https://dev.to/nikolab/css-aspect-ratio-with-a-fallback-for-old-browsers-3eon)

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

### 3. The stack vs flow

Every direct sibling child element of `.stack` has margin-block-start added to it. The `.flow` uses custom variables and a fallback value.

[Full article](https://andy-bell.co.uk/my-favourite-3-lines-of-css/?utm_source=tldrnewsletter)

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

### 4. Paragraph characters width

The width of an element can be limited by specifying the number of characters allowed.

```css
.paragraph {
  width: 50ch;
}
```

### 5. Scrollbar space automatic management

A default right space for the scrollbar can be added to the container even when the scroll is not active nor visible.

[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/scrollbar-gutter)

```css
.container {
  scrollbar-gutter: stable;
}
```

### 6. grid auto-placements

The `grid-auto-flow` property controls how the auto-placement algorithm works, specifying exactly how auto-placed items get flowed into the grid.

[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-auto-flow)

```css
grid-auto-flow: row | column | dense | row dense | column dense;
```

### 7. Flex-grow 9999 Hack

Makes a flex item behave like it has **two flex grow** values.

[Full article](https://www.joren.co/flex-grow-9999-hack/)

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
