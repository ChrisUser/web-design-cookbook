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
