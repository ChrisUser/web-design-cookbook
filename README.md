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
