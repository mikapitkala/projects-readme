<div align="center">

![dot-js Banner](docs/images/banner.png)

# The Reactive Framework for the Modern Web

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-1.0.0-green.svg)](https://semver.org)
[![Build Size](https://img.shields.io/badge/size-2kb-orange.svg)]()

**Speed. Simplicity. Scalability.**
dot-js abandons the Virtual DOM for O(1) fine-grained reactivity. No build steps, no complex tooling—just pure performance.

[**Explore Documentation**](framework/docs/README.md) &nbsp; | &nbsp; [**View Live Demo**](example/showcase/index.html)

</div>

---

## 🚀 Why dot-js?

### ⚡ Zero Overheard
We use **Reactive Markers** to update the DOM directly. No diffing, no wasted cycles.

### 🛠️ No Build Step
Import via ES Modules and run. It works in the browser, instantly.

### 🧠 Intelligent Architecture
Features a built-in **Scheduler** for batched updates, **Global Event Delegation**, and a dedicated **Router**.

---

## 👁️ How to Run Examples

To view the examples, you need to run the included development server (this fixes browser security restrictions):

1. **Open your terminal** to the project folder.
2. **Run the server**:
   ```bash
   cd example
   node server.js
   ```
3. **Open the link**: The terminal will show a link (usually `http://localhost:3001/example/index.html`). Click it to view the examples.

### No Installation Needed
The server uses only built-in Node.js modules, so you don't need to run `npm install`.

*Note: For development, we still recommend using the standard `index.html` with a local server.*

---

## 📂 Project Structure

| Directory | Description |
| :--- | :--- |
| **[`framework/`](framework/docs/README.md)** | **Core Engine & API Docs.** The source code and detailed documentation. |
| **[`example/timer_tutorial/`](example/timer_tutorial/README.md)** | **Tutorial.** Learn dot-js by building a timer in 16 simple steps. |
| **[`example/design_system/`](example/design_system/index.html)** | **Design System.** Showcase of the classless CSS framework. |
| **[`example/todo/`](example/todo/index.html)** | **Simple Todo.** Basic todo app demonstrating core concepts. |
| **[`example/vanilla_todo/`](example/vanilla_todo/index.html)** | **Vanilla Comparison.** Same todo app in vanilla JS for performance and code comparison. |
| **[`example/showcase/`](example/showcase/index.html)** | **Advanced Demo.** Full-featured app with Routing, Async Data, and Performance tests. |
| **[`docs/`](docs/)** | **Project Assignment.** The task description and review requirements for this project. |
---

## ⚡ Getting Started

Here is the "Hello World" of reactivity: The Counter.

```javascript
import { h, createSignal, div, button, p } from './index.js';

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

[👉 **Read the Full Getting Started Guide**](framework/docs/getting-started.md)

---


<div align="center">
    <i>Built with ❤️ by Mika and Pavel.</i>
</div>
