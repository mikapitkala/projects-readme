# Router API

A lightweight, hash-based router for client-side navigation.

## Usage

### `router`
The exported singleton instance of the `Router` class.

### `router.add(path, component)`
Registers a route.

**Parameters:**
- `path` *(string)*: The URL hash path (e.g., '/', '/about').
- `component` *(function)*: A function that returns a DOM element (the component).

**Example:**
```javascript
router.add('/', HomeComponent);
router.add('/about', AboutComponent);
```

### `router.navigate(path)`
Programmatically navigates to a new path.

**Parameters:**
- `path` *(string)*: The path to navigate to.

**Example:**
```javascript
router.navigate('/dashboard');
```

### `router.resolve()`
Renders the component matching the current URL hash.

**Returns:**
- `HTMLElement`: The component's DOM element.

**Example:**
```javascript
document.body.appendChild(router.resolve());
```

## How it works
The router listens to the `hashchange` event. To link to a route, simply use standard anchor tags with hash hrefs:

```javascript
a({ href: '#/about' }, 'Go to About')
```
