# Reactivity API

These functions form the core of the **dot-js** reactive system.

## Signals & Effects

### `createSignal(initialValue)`
Creates a reactive signal.

**Parameters:**
- `initialValue` *(any)*: The starting value of the signal.

**Returns:** `[getter, setter]`
- `getter` *(function)*: Call to read the current value. Subscribe the current effect if running.
- `setter` *(function)*: Call to update the value. Triggers dependent effects.

**Example:**
```javascript
const [count, setCount] = createSignal(0);
console.log(count()); // 0
setCount(5);
setCount(c => c + 1); // Functional update
```

### `createEffect(fn)`
Creates a side effect that automatically re-runs when its dependencies change.

**Parameters:**
- `fn` *(function)*: The function to execute. It runs immediately and tracks any signals read during execution.

**Returns:**
- `effect` *(object)*: The effect object (internal use).

**Example:**
```javascript
createEffect(() => {
    console.log("The count is:", count());
});
```

### `createMemo(fn)`
Creates a readonly signal that derives its value from other signals. It only re-evaluates when dependencies change.

**Parameters:**
- `fn` *(function)*: The computation function.

**Returns:**
- `getter` *(function)*: A signal getter for the derived value.

**Example:**
```javascript
const doubleCount = createMemo(() => count() * 2);
```

### `onMount(fn)`
Schedules a function to run after the current microtask queue (usually after DOM rendering).

**Parameters:**
- `fn` *(function)*: The callback to run.

## Store

### `createStore(initialState)`
Creates a reactive store object where properties are automatically wrapped in signals.

**Parameters:**
- `initialState` *(object)*: An object containing initial values.

**Returns:**
- `proxy` *(object)*: A proxy object.
    - Read properties normally: `store.user()`
    - Write properties using the special `set` method: `store.set('user', 'New Name')`

**Example:**
```javascript
const store = createStore({ user: 'Alice', theme: 'dark' });
console.log(store.user()); // 'Alice'
store.set('user', 'Bob');
```

## Persistence

### `createPersistedSignal(key, initialValue)`
Creates a signal that automatically syncs with `localStorage`.

**Parameters:**
- `key` *(string)*: The localStorage key.
- `initialValue` *(any)*: Default value if storage is empty.

**Returns:** `[getter, setter]` (Same as `createSignal`)

### `clearPersistedSignal(key)`
Removes the value from `localStorage`.

### `hasPersistedSignal(key)`
Checks if a key exists in `localStorage`.
