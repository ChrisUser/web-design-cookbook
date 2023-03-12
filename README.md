# web-design-cookbook

### The stack vs flow

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

### Support fallback

[MDN guide](https://developer.mozilla.org/en-US/docs/Web/CSS/@supports)

If you need to handle CSS properties fallbacks you can use the `@support()` feature query.

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
  /* If the property is't supported */
  .flex-container > * {
    background: green;
  }

  .flex-container {
    display: block;
  }
}
```

### Paragraph characters width

You can limit the width of an element by specifying the number of characters allowed.

```css
.paragraph {
  width: 50ch;
}
```

### Aspect ratio with fallback

Generate aspect ratio code [here](https://ratiobuddy.com/)

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

### Performant naming convention

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

### Scrollbar space automatic management

[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/scrollbar-gutter)

You can add a default right space for the scrollbar even when the scroll is not active nor visible with:

```css
.container {
  scrollbar-gutter: stable;
}
```

### Use FOUT font rule

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

### grid auto-placements

The `grid-auto-flow` property controls how the auto-placement algorithm works, specifying exactly how auto-placed items get flowed into the grid.

[MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-auto-flow)

```css
grid-auto-flow: row | column | dense | row dense | column dense;
```

### Flex-grow 9999 Hack

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
