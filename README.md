# ARIA Role Lowdown:

- aria roles are used like so: role=""
- aria roles - like labels - provide contextual information for users with accessibility needs.

## role="menu"

What it does: acts as a container for an expanded set of menuitems.

### Notes:

- This role is not the same as the `<nav>` element and has it's own operating system-esque requirements for keyboard functionality (see [https://www.w3.org/TR/wai-aria-practices-1.1/#menu].)
- 99.999999999% of the time you'll be using a `<nav>` instead of this in modern frontend development.

### role="menu" with role="menuitem" and role="separator"

```
<ul role="menu">
<li role="menuitem"></li>
<li role="separator"></li>
<li role="menuitem"></li>
</ul>
```
