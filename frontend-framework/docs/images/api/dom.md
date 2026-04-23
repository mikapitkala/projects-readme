# DOM API

Functions for creating and managing DOM elements.

## Element Creation

### `h(tag, props, ...children)`
The core hyperscript function to create DOM elements.

**Parameters:**
- `tag` *(string)*: The HTML tag name (e.g., 'div', 'button').
- `props` *(object)*: Attributes and properties.
    - Event handlers: `onClick`, `onInput`, etc.
    - Dynamic attributes: Pass a signal function to automatically update.
    - `class`, `style`: Support string, object, or signal.
- `...children` *(Node | string | function | Array)*: Child elements.
    - Pass a function to create a reactive text node or conditional render.

**Returns:**
- `element` *(HTMLElement)*: The created DOM node.

**Example:**
```javascript
h('div', { class: 'container' },
    h('h1', {}, 'Title'),
    () => show() ? 'Visible' : 'Hidden'
)
```

### Element Helpers
Shortcuts for common HTML headers are exported for convenience:
`div`, `span`, `p`, `button`, `input`, `h1`-`h6`, `ul`, `li`, `table`, etc.

**Example:**
```javascript
import { div, button } from '../index.js';

div({}, button({}, 'Click me'))
```

## Event Delegation

### `delegate(parent, eventType, selector, handler)`
Attaches a delegated event listener to a parent element.

**Parameters:**
- `parent` *(HTMLElement)*: The root element to listen on.
- `eventType` *(string)*: The event name (e.g., 'click').
- `selector` *(string)*: CSS selector to match target elements.
- `handler` *(function)*: The callback `(e) => void`. `this` is bound to the matching target.

### `withDelegation(element, events)`
Helper to attach multiple delegated events to an element.

**Parameters:**
- `element` *(HTMLElement)*: The parent element.
- `events` *(object)*: Map of `eventType -> { selector: handler }`.

**Example:**
```javascript
withDelegation(list, {
    click: {
        '.delete-btn': (e) => handleDelete(e),
        '.edit-btn': (e) => handleEdit(e)
    }
})
```

### `delegateList(listElement, itemSelector, handlers)`
Specific helper for lists where you want to handle events on items.

**Parameters:**
- `listElement` *(HTMLElement)*: The `<ul>` or `<ol>`.
- `itemSelector` *(string)*: Selector for list items (e.g., 'li').
- `handlers` *(object)*: Map of `eventType -> handler`.
