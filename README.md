# ARIA Role Lowdown:

- aria roles are used like so: role=""
- aria roles - like aria attributes - provide contextual information for users with accessibility needs.
- aria roles take precedence in the accessibility tree.
- If you're using semantic HTML4 elements you shouldn't need to put aria roles on them except in some browser-specific edge cases.
- If you're using semantic HTML5 elements sometimes you'll need to put aria roles on them depending on browser/VO support for the element.

## role="figure"

What it does: identifies a semantic figure element.

### figure element with role="figure" + aria-label for optimal screen reader support

```
<figure role="figure" aria-label="repeat figcaption content here">
  <!-- figure content. if an image, provide alt text -->
  <figcaption>
    Caption for the figure.
  </figcaption>
</figure>

<!--
  aria-label for macOS VoiceOver + Chrome
  role="figure" for IE11.

  IE11 needs an accessible name (provided by aria-label).
  If not for the fact VO + Chrome doesn't support an
  accessible name from aria-labelledby, that attribute
  would have been preferred / pointed to an ID on
  the <figcaption>.
-->
```

### References

- [https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/Figure_Role]
- [https://www.scottohara.me/blog/2019/01/21/how-do-you-figure.html]

## role="grid"

What it does: identifies a widget/markup group with more than one row of cells.

Use it when: you need to designate a widget/markup group that is like a table but its individual cells are interactive and keyboard navigable.

### Notes:

- Tables are not interactive by default.
- By default, aria-role="grid" is considered editable and needs to have aria-readonly="true" set to be considered otherwise.
- role="grid" on a `<table>` element will make the accessibility tree auto-populate the native child roles through its structure. This is unreliable though, it's safer to explicitly add roles.
- If a table maintains a selection state, has two-dimensional navigation, or allows the user to rearrange cell order use grid or treegrid instead.
- This role is useful if your table-esque element has interactive elements in its grid cells (buttons, checkboxes, etc.)

### Keyboard Interaction Requirements

```
<table class="standard-table">
 <thead>
  <tr>
   <th scope="col">Key</th>
   <th scope="col">Action</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><kbd>→</kbd></td>
   <td>Moves focus one cell to the right.&nbsp;If focus is on the right-most cell in the row, focus does not move.</td>
  </tr>
  <tr>
   <td><kbd>←</kbd></td>
   <td>Moves focus one cell to the left. If focus is on the left-most cell in the row, focus does not move.</td>
  </tr>
  <tr>
   <td><kbd>↓</kbd></td>
   <td>Moves focus one cell down. If focus is on the bottom cell in the column, focus does not move.</td>
  </tr>
  <tr>
   <td><kbd>↑</kbd></td>
   <td>Moves focus one cell up. If focus is on the top cell in the column, focus does not move.</td>
  </tr>
  <tr>
   <td><kbd>Page Down</kbd></td>
   <td>Moves focus down an author-determined number of rows, typically scrolling so the bottom row in the currently visible set of rows becomes one of the first visible rows. If focus is in the last row of the grid, focus does not move.</td>
  </tr>
  <tr>
   <td><kbd>Page Up</kbd></td>
   <td>Moves focus up an author-determined number of rows, typically scrolling so the top row in the currently visible set of rows becomes one of the last visible rows. If focus is in the first row of the grid, focus does not move.</td>
  </tr>
  <tr>
   <td><kbd>Home</kbd></td>
   <td>Moves focus to the first cell in the row that contains focus.</td>
  </tr>
  <tr>
   <td><kbd>End</kbd></td>
   <td>Moves focus to the last cell in the row that contains focus.</td>
  </tr>
  <tr>
   <td><kbd>ctrl</kbd> + <kbd>Home</kbd></td>
   <td>Moves focus to the first cell in the first row.</td>
  </tr>
  <tr>
   <td><kbd>ctrl</kbd> + <kbd>End</kbd></td>
   <td>Moves focus to the last cell in the last row.</td>
  </tr>
 </tbody>
</table>
```

### Keyboard Interaction Requirements - Selectable Rows or Columns

```
<table class="standard-table">
 <thead>
  <tr>
   <th scope="col">Key combination</th>
   <th scope="col">Action</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><kbd>ctrl</kbd> + <kbd>Space</kbd></td>
   <td>Select the column that contains the focus.</td>
  </tr>
  <tr>
   <td><kbd>shift</kbd> + <kbd>Space</kbd></td>
   <td>Selects the row that contains the focus. If the grid includes a column with checkboxes to select rows, this key combination can be used to check that box even if the focus is not on the checkbox.</td>
  </tr>
  <tr>
   <td><kbd>ctrl</kbd> + <kbd>A</kbd></td>
   <td>Selects all cells.</td>
  </tr>
  <tr>
   <td><kbd>shift</kbd> + <kbd>→</kbd></td>
   <td>Extends selection one cell to the right.</td>
  </tr>
  <tr>
   <td><kbd>shift</kbd> + <kbd>←</kbd></td>
   <td>Extends selection one cell to the left.</td>
  </tr>
  <tr>
   <td><kbd>shift</kbd> + <kbd>↓</kbd></td>
   <td>Extends selection one cell down.</td>
  </tr>
  <tr>
   <td><kbd>shift</kbd> + <kbd>↑</kbd></td>
   <td>Extends selection one cell up.</td>
  </tr>
 </tbody>
</table>
```

### role="grid" example

```
<div role="grid" aria-colcount="6">
  <div role="rowgroup">
    <div role="row">
      <div role="columnheader" aria-colindex="1">First name</div>
      <div role="columnheader" aria-colindex="2">Last name</div>
      <div role="columnheader" aria-colindex="5">City</div>
      <div role="columnheader" aria-colindex="6">Zip</div>
    </div>
  </div>
  <div role="rowgroup">
    <div role="row">
      <div role="gridcell" aria-colindex="1">Debra</div>
      <div role="gridcell" aria-colindex="2">Burks</div>
      <div role="gridcell" aria-colindex="5">New York</div>
      <div role="gridcell" aria-colindex="6">14127</div>
    </div>
  </div>
</div>
```

### References

- [https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/Grid_Role]
- [https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/Gridcell_role]

## role="list"

What it does: identifies a semantic list element.

### Notes:

- Setting `list-style: none;` on a list element triggers a bugfeature (new word courtesy of frontend development in 2020) of Webkit where its semantics are removed for VO screenreader.

### list with "list-style: none" set and role="list" fix applied for Safari

```
<style>
.list-no-style {
    list-style: none;
}
</style>
<ul class="list-no-style" role="list"> <!-- add the list role to the <ul> -->
  <li>...</li>
  <li>...</li>
  <li>...</li>
  <!-- etc. -->
</ul>
```

### References:

- [https://bugs.webkit.org/show_bug.cgi?id=170179]
- [https://www.scottohara.me/blog/2019/01/12/lists-and-safari.html]
- [https://www.scottohara.me/blog/2018/05/26/aria-lists.html]
- [https://unfetteredthoughts.net/2017/09/26/voiceover-and-list-style-type-none/]

## role="menu"

What it does: acts as a container for an expanded set of menuitems.

### Notes:

- This role is not the same as the `<nav>` element and has it's own operating system-esque requirements for keyboard functionality (see [https://www.w3.org/TR/wai-aria-practices-1.1/#menu].)
- The children roles for menu items that correspond with `<input type="checkbox">` and `<input type="radio">` are: `role="menuitemcheckbox"` and `role="menuitemradio"`.

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
