# dot-js Framework

**dot-js** is a high-performance, pure JavaScript ESM framework designed for building modern web applications without the overhead.

> [!IMPORTANT]
> **No Build Step Required.** dot-js runs directly in the browser via ES Modules.

## 📚 Documentation

We have moved our documentation to a dedicated section for better organization.

### [👉 Go to Documentation](./docs/README.md)

### Quick Links

*   [Getting Started](./docs/getting-started.md)
*   [Architecture & Concepts](./docs/architecture.md)
*   [API Reference](./docs/api/reactivity.md)

## Example

```javascript
import { h, createSignal, div, button } from './index.js';

function App() {
    const [count, setCount] = createSignal(0);
    return div({}, 
        "Count: ", count,
        button({ onClick: () => setCount(c => c + 1) }, "+1")
    );
}
```

*Built with ❤️ by Mika and Pavel.*
