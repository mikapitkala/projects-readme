# Getting Started with dot-js

## 🚀 Installation

Simply import the framework directly in your HTML. No Webpack, no Vite, no hassle.

```javascript
import { h, createSignal, onMount } from '../index.js'; // Adjust path as needed
// Start building!
```

## ⚡ Hello World

Here is the "Hello World" of reactivity: The Counter.

```javascript
import { h, createSignal, div, button, p } from '../index.js';

function Counter() {
    const [count, setCount] = createSignal(0);

    return div({ class: 'p-4 border rounded' },
        h('h2', {}, 'Reactivity in Action'),
        p({}, 'Current count: ', count), // Pass the function itself!
        button({
            class: 'btn-primary',
            onClick: () => setCount(c => c + 1)
        }, 'Increment')
    );
}

document.body.appendChild(Counter());
```

## 💎 Best Practices

1.  **Granularity is King**: Create signals for specific values, not giant objects.
    *   ✅ `const [name, setName] = createSignal('Alice')`
    *   ❌ `const [state, setState] = createSignal({ name: 'Alice', age: 25 })`
2.  **Pass Signals, Don't Read Them**: When rendering, pass the signal function (`count`) instead of the value (`count()`). This allows the framework to subscribe to future updates.
3.  **Component Reusability**: Build small, atomic components (`Button`, `Card`) and compose them.
