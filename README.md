# ARIA Role Lowdown:

- aria roles are used like so: role=""
- aria roles - like aria attributes - provide contextual information for users with accessibility needs.

## role="menu"

What it does: acts as a container for an expanded set of menuitems.

### Notes:

- This role is not the same as the `<nav>` element and has it's own operating system-esque requirements for keyboard functionality (see [https://www.w3.org/TR/wai-aria-practices-1.1/#menu].)
- 99.999999999% of the time you'll be using a `<nav>` instead of this in modern frontend development.
- the children roles for menu items that correspond with `<input type="checkbox">` and `<input type="radio">` are: `role="menuitemcheckbox"` and `role="menuitemradio"`.

### role="menu" with role="menuitem" and role="separator"

```
<ul role="menu">
<li role="menuitem"></li>
<li role="separator"></li>
<li role="menuitem"></li>
</ul>
```

### role="menu" with role="menuitemRadio" (used for single items that can be selected from lists of menu items a la radio buttons)

```
<ul role="menu">
<li role="menuitemradio" aria-checked="true"></li>
</ul>
```

## role="none", role="presentation" (these are identical roles)

What it does: removes the semantics of an element but does not hide it from assistive technologies.

Use it when: you need to remove semantics from legacy markup (i.e., table layouts) or other nonsemantic layouts. Alternatively, use it if you need to progressively enhance javascript-free markup for certain ARIA patterns.

### aria-role="presentation" for a progressively enhanced tablist

```
<ul role="tablist">
  <li role="presentation">
    <a href="#panel_1"
      role="tab"
      aria-selected="true/false"
      aria-controls="panel_1">
      ...
    </a>
  </li>
  <!-- etc. -->
</ul>
```

### References

- [https://www.scottohara.me/blog/2018/05/05/hidden-vs-none.html]
- [https://www.w3.org/TR/wai-aria-1.1/#none]
