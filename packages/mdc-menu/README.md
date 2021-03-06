<!--docs:
title: "Menus"
layout: detail
section: components
excerpt: "Non-cascading Material Design menus."
iconId: menu
path: /catalog/menus/
-->

# Menus

<!--<div class="article__asset">
  <a class="article__asset-link"
     href="https://material-components-web.appspot.com/simple-menu.html">
    <img src="{{ site.rootpath }}/images/mdc_web_screenshots/menus.png" width="178" alt="Menus screenshot">
  </a>
</div>-->

The MDC Menu component is a spec-aligned menu component adhering to the
[Material Design menu specification](https://material.io/guidelines/components/menus.html).
It implements simple menus. Menus require JavaScript to work correctly, but the open and closed states are correct on
first render.

## Design & API Documentation

<ul class="icon-list">
  <li class="icon-list-item icon-list-item--spec">
    <a href="https://material.io/guidelines/components/menus.html">Material Design guidelines: Menus</a>
  </li>
  <li class="icon-list-item icon-list-item--link">
    <a href="https://material-components-web.appspot.com/simple-menu.html">Demo</a>
  </li>
</ul>

## Installation

```
npm install --save @material/menu
```

## Simple menu usage

A simple menu is usually closed, appearing when opened. It is appropriate for any display size.

```html
<div class="mdc-simple-menu" tabindex="-1">
  <ul class="mdc-simple-menu__items mdc-list" role="menu" aria-hidden="true">
    <li class="mdc-list-item" role="menuitem" tabindex="0">
      A Menu Item
    </li>
    <li class="mdc-list-item" role="menuitem" tabindex="0">
      Another Menu Item
    </li>
  </ul>
</div>
```
> Note: adding a `tabindex` of `0` to the menu items places them in the tab order.
  Adding a `tabindex` of `-1` to the root element makes it programmatically focusable, without
  placing it in the tab order. This allows the menu to be focused on open, so that the next Tab
  keypress moves to the first menu item. If you would like the first menu item to be automatically
  focused instead, remove `tabindex="-1"` from the root element.

```js
let menu = new mdc.menu.MDCSimpleMenu(document.querySelector('.mdc-simple-menu'));
// Add event listener to some button to toggle the menu on and off.
document.querySelector('.some-button').addEventListener('click', () => menu.open = !menu.open);
```

You can start the menu in its open state by adding the `mdc-simple-menu--open` class to your HTML:

```html
<div class="mdc-simple-menu mdc-simple-menu--open">
...
</div>
```

### Positioning the menu

The menu can either be positioned manually, or automatically, by anchoring it to an element.

#### Automatic Positioning

The menu understands the concept of an anchor, which it can use to determine how to position itself, and which corner
to open from.

The anchor can either be a visible element that the menu is a child of:

```html
<div class="toolbar mdc-menu-anchor">
  <div class="mdc-simple-menu">
  ...
  </div>
</div>
```

or a wrapper element that contains the actual visible element to attach to:

```html
<div class="mdc-menu-anchor">
  <button>Open Menu</button>
  <div class="mdc-simple-menu">
  ...
  </div>
</div>
```

> Note: `overflow: visible` and `position: relative` will be set on the element with `mdc-menu-anchor` to ensure that
the menu is positioned and displayed correctly.

The menu will check if its parent element has the `mdc-menu-anchor` class set, and if so, it will automatically position
itself relative to this anchor element. Unless anchor corner is specified, menu will open from the top left
(top right in RTL) corner of the anchor by default, but will choose an appropriate different corner if close
to the edge of the screen.

#### Manual Positioning

The menu is `position: absolute` by default, and must be positioned by the user when doing manual positioning.

```html
<div class="container">
  <div class="mdc-simple-menu" style="top:0; left: 0;">
  ...
  </div>
</div>
```

The menu will open from the top left by default (top right in RTL). Depending on how you've positioned your button, you
may want to change the point it opens from.
To override the opening point, you can style `transform-origin` directly, or use one of the following convenience
classes:

| class name                                | description                          |
| ----------------------------------------- | ------------------------------------ |
| `mdc-simple-menu--open-from-top-left`     | Open the menu from the top left.     |
| `mdc-simple-menu--open-from-top-right`    | Open the menu from the top right.    |
| `mdc-simple-menu--open-from-bottom-left`  | Open the menu from the bottom left.  |
| `mdc-simple-menu--open-from-bottom-right` | Open the menu from the bottom right. |


#### Disabled menu items

When used in components such as MDC Menu, `mdc-list-item`'s can be disabled.
To disable a list item, set `aria-disabled` to `"true"`, and set `tabindex` to `"-1"`.

```html
<div class="mdc-simple-menu" tabindex="-1">
  <ul class="mdc-simple-menu__items mdc-list" role="menu" aria-hidden="true">
    <li class="mdc-list-item" role="menuitem" tabindex="0">
      A Menu Item
    </li>
    <li class="mdc-list-item" role="menuitem" tabindex="-1" aria-disabled="true">
      Disabled Menu Item
    </li>
  </ul>
</div>
```

### Using the JS Component

MDC Simple Menu ships with a Component / Foundation combo which allows for frameworks to richly integrate the
correct menu behaviors into idiomatic components.

The component has a read-write property, `open`, which keeps track of the visual state of the component.

```js
// Analyse current state.
console.log('The menu is ' + (menu.open ? 'open' : 'closed'));
// Open menu.
menu.open = true;
// Close menu.
menu.open = false;
```

It also has two lower level methods, which control the menu directly, by showing (opening) and
hiding (closing) it:

```js
// Show (open) menu.
menu.show();
// Hide (close) menu.
menu.hide();
// Show (open) menu, and focus the menu item at index 1.
menu.show({focusIndex: 1});
```

You can still use the `open` getter property even if showing and hiding directly:

```js
menu.show();
console.log(`Menu is ${menu.open ? 'open' : 'closed'}.`);
```


#### Including in code

##### ES2015

```javascript
import {MDCSimpleMenu, MDCSimpleMenuFoundation, util} from '@material/menu';
```

##### CommonJS

```javascript
const mdcMenu = require('mdc-menu');
const MDCSimpleMenu = mdcMenu.MDCSimpleMenu;
const MDCSimpleMenuFoundation = mdcMenu.MDCSimpleMenuFoundation;
const util = mdcMenu.util;
```

##### AMD

```javascript
require(['path/to/mdc-menu'], mdcMenu => {
  const MDCSimpleMenu = mdcMenu.MDCSimpleMenu;
  const MDCSimpleMenuFoundation = mdcMenu.MDCSimpleMenuFoundation;
  const util = mdcMenu.util;
});
```

##### Global

```javascript
const MDCSimpleMenu = mdc.Menu.MDCSimpleMenu;
const MDCSimpleMenuFoundation = mdc.Menu.MDCSimpleMenuFoundation;
const util = mdc.menu.util;
```

#### Automatic Instantiation

If you do not care about retaining the component instance for the simple menu, simply call `attachTo()` and pass it a
DOM element.

```javascript
mdc.MDCSimpleMenu.attachTo(document.querySelector('.mdc-simple-menu'));
```

#### Manual Instantiation

Simple menus can easily be initialized using their default constructors as well, similar to `attachTo`.

```javascript
import {MDCSimpleMenu} from '@material/menu';

const menu = new MDCSimpleMenu(document.querySelector('.mdc-simple-menu'));
```

#### Handling selection events

When a menu item is selected, the menu component will emit a `MDCSimpleMenu:selected` custom event
with the following `detail` data:

| property name | type | description |
| --- | --- | --- |
| `item` | `HTMLElement` | The DOM element for the selected item |
| `index` | `number` | The index of the selected item |

If the menu is closed with no selection made (for example, if the user hits `Escape` while it's open), a `MDCSimpleMenu:cancel` custom event is emitted instead, with no data attached.

### Using the Foundation Class

MDC Simple Menu ships with an `MDCSimpleMenuFoundation` class that external frameworks and libraries can use to
integrate the component. As with all foundation classes, an adapter object must be provided.
The adapter for simple menu must provide the following functions, with correct signatures:

| Method Signature | Description |
| --- | --- |
| `addClass(className: string) => void` | Adds a class to the root element. |
| `removeClass(className: string) => void` | Removes a class from the root element. |
| `hasClass(className: string) => boolean` | Returns boolean indicating whether element has a given class. |
| `hasNecessaryDom() => boolean` | Returns boolean indicating whether the necessary DOM is present (namely, the `mdc-simple-menu__items` container). |
| `getAttributeForEventTarget(target: EventTarget, attributeName: string) => string` | Returns the value of a given attribute on an event target. |
| `eventTargetHasClass: (target: EventTarget, className: string) => boolean` | Returns true if the event target has a given class. |
| `getInnerDimensions() => {width: number, height: number}` | Returns an object with the items container width and height |
| `hasAnchor: () => boolean` | Returns whether the menu has an anchor for positioning. |
| `getAnchorDimensions() => { width: number, height: number, top: number, right: number, bottom: number, left: number }` | Returns an object with the dimensions and position of the anchor (same semantics as `DOMRect`). |
| `getWindowDimensions() => {width: number, height: number}` | Returns an object with width and height of the page, in pixels. |
| `getNumberOfItems() => numbers` | Returns the number of _item_ elements inside the items container. In our vanilla component, we determine this by counting the number of list items whose `role` attribute corresponds to the correct child role of the role present on the menu list element. For example, if the list element has a role of `menu` this queries for all elements that have a role of `menuitem`. |
| `registerInteractionHandler(type: string, handler: EventListener) => void` | Adds an event listener `handler` for event type `type`. |
| `deregisterInteractionHandler(type: string, handler: EventListener) => void` | Removes an event listener `handler` for event type `type`. |
| `registerBodyClickHandler(handler: EventListener) => void` | Adds an event listener `handler` for event type 'click'. |
| `deregisterBodyClickHandler(handler: EventListener) => void` | Removes an event listener `handler` for event type 'click'. |
| `getIndexForEventTarget(target: EventTarget) => number` | Checks to see if the `target` of an event pertains to one of the menu items, and if so returns the index of that item. Returns -1 if the target is not one of the menu items. The same notice for `index` applies here as above. |
| `notifySelected(evtData: {index: number}) => void` | Dispatches an event notifying listeners that a menu item has been selected. The function should accept an `evtData` parameter containing the an object with an `index` property representing the index of the selected item. Implementations may choose to supplement this data with additional data, such as the item itself. |
| `notifyCancel() => void` | Dispatches an event notifying listeners that the menu has been closed with no selection made. |
| `saveFocus() => void` | Stores the currently focused element on the document, for restoring with `restoreFocus`. |
| `restoreFocus() => void` | Restores the previously saved focus state, by making the previously focused element the active focus again. |
| `isFocused() => boolean` | Returns a boolean value indicating whether the root element of the simple menu is focused. |
| `focus() => void` | Focuses the root element of the simple menu. |
| `getFocusedItemIndex() => number` | Returns the index of the currently focused menu item (-1 if none). |
| `focusItemAtIndex(index: number) => void` | Focuses the menu item with the provided index. |
| `isRtl() => boolean` | Returns boolean indicating whether the current environment is RTL. |
| `setTransformOrigin(value: string) => void` | Sets the transform origin for the menu element. |
| `setPosition(position: { top: string, right: string, bottom: string, left: string }) => void` | Sets the position of the menu element. |
| `setMaxHeight(value: string) => void` | Sets `max-height` style for the menu element. |

### The full foundation API

#### MDCSimpleMenuFoundation.open({focusIndex: number} = {}) => void

Opens the menu. Takes an options object containing a `focusIndex` property that specifies the index of the menu item to be focused. If the options object or `focusIndex` is omitted, no menu item will be focused.

#### MDCSimpleMenuFoundation.close() => void

Closes the menu.

#### MDCSimpleMenuFoundation.isOpen() => boolean

Returns whether or not the menu is open.

#### MDCSimpleMenuFoundation.setAnchorCorner(Corner = Corner.TOP_START) => void

Specifies the anchor corner to which top start of the menu (top left in ltr, top right in rtl) should align given there
is enough space to show the full menu.
When menu display is constrained by viewport edge, `TOP` can be flipped to `BOTTOM`. Similarly `START` can flip to `END`.
Specifying `BOTTOM_START` and `BOTTOM_END` positions, indicates that the menu displayed either fully below or
above the anchor. In such cases maximum height of the menu is enforced.
When specifying `TOP_START` and `TOP_END` positions, the menu is allowed to be taller if it does not fit below
or above the anchor.

#### MDCSimpleMenuFoundation.setAnchorMargin({top: number, right: number, bottom: number, left: number}) => void

Specifies pixel margins that the menu should be offset from all four sides of an anchor. When menu overlaps an
anchor (default anchor corner) and menu is taller than would fit (not extending beyond viewport edges), margin is
ignored and menu allowed to display fully overlapping the anchor. In such cases menu is not strictly aligned to an
anchor corner, also maximum height of the menu in such cases is constrained by the viewport height.


### The util API
External frameworks and libraries can use the following utility methods when integrating a component.

#### util.getTransformPropertyName(globalObj, forceRefresh = false) => String

Returns the name of the correct transform property to use on the current browser.

#### util.clamp(value, min = 0, max = 1) => Number

Clamps a value between the minimum and the maximum, returning the clamped value.

#### util.bezierProgress(time, x1, y1, x2, y2) => Number

Returns the easing value to apply at time t, for a given cubic bezier curve.

```
Control points P0 and P3 are assumed to be (0,0) and (1,1), respectively.
Parameters are as follows:
 - time: The current time in the animation, scaled between 0 and 1.
 - x1: The x value of control point P1.
 - y1: The y value of control point P1.
 - x2: The x value of control point P2.
 - y2: The y value of control point P2.
```
