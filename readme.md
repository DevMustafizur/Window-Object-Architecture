# window object

## 1. What is the Window Object?

**Answer:**
The `window` object is the global object of the **Browser JavaScript Runtime**. It represents the browser window/tab and provides access to browser features such as `document`, `location`, `history`, and `navigator`.

---

## 2. What are the main components of Browser JavaScript Runtime?

**Answer:**

```text
Browser JavaScript Runtime
│
├── Window Object
├── Web APIs
├── JavaScript Engine
│   └── V8
├── Call Stack
├── Microtask Queue
├── Task Queue
├── Event Loop
└── Rendering System
```

---

## 3. What is a JavaScript Engine?

**Answer:**
A JavaScript Engine parses, compiles, and executes JavaScript code. Chrome uses the **V8 JavaScript Engine**.

---

## 4. Where does the Window Object exist?

**Answer:**
The Window Object exists as part of the **Browser JavaScript Runtime** and acts as the global object of a browser page.

---

## 5. What is the relationship between Window Object and V8?

**Answer:**
The Window Object is provided by the browser runtime, while V8 executes the JavaScript code that accesses the Window Object.

### Relationship

```text
Browser JavaScript Runtime
│
├── Window Object
│
├── Web APIs
│
└── JavaScript Engine
    └── V8
```

### Flow

```text
JavaScript Code
      ↓
     V8
      ↓
Access Window Object
      ↓
Browser-provided Window
```

---

## 6. Is the Window Object part of V8?

**Answer:**
No. The Window Object is provided by the browser. V8 is the JavaScript engine that executes JavaScript.

```text
Browser JavaScript Runtime
│
├── Window Object     ← Browser-provided
├── Web APIs          ← Browser-provided
│
└── JavaScript Engine
    └── V8            ← JavaScript Engine
```

---

## 7. Who creates the Window Object?

**Answer:**
The browser creates and manages the Window Object through its native implementation and exposes it to JavaScript.

---

## 8. Why can JavaScript directly use `window`?

**Answer:**
Because the browser exposes the Window Object as the global object of the browser's JavaScript environment.

```javascript
console.log(window);
console.log(window.document);
console.log(window.location);
```

---

## 9. What is the architecture of the Window Object?

**Answer:**

```text
Browser JavaScript Runtime
│
├── JavaScript Engine
│   └── V8
│       ├── Parser
│       ├── Compiler
│       ├── Heap
│       ├── Call Stack
│       └── JavaScript Execution
│
├── Window Object
│   ├── DOM
│   │   └── document
│   │
│   ├── BOM
│   │   ├── location
│   │   ├── history
│   │   ├── navigator
│   │   └── screen
│   │
│   └── Storage
│       ├── localStorage
│       └── sessionStorage
│
├── Web APIs
│   ├── Timers
│   ├── Fetch
│   ├── WebSocket
│   └── Other APIs
│
├── Task Queue
├── Microtask Queue
├── Event Loop
└── Rendering System
```

---

## 10. What are some important properties and APIs available through Window?

**Answer:**
Some important examples include:

```text
window
├── document
├── location
├── history
├── navigator
├── screen
├── localStorage
├── sessionStorage
├── console
├── innerWidth
├── innerHeight
├── setTimeout()
├── setInterval()
└── requestAnimationFrame()
```

---

## 11. Is `document` the same object as `window`?

**Answer:**
No. They are different objects.

`window` is the global browser object, while `document` represents the current HTML document.

```text
Window
│
└── document
    │
    └── DOM Tree
```

---

## 12. What is the relationship between Window and DOM?

**Answer:**
The browser creates the DOM and exposes the `document` object through the Window Object.

```text
Browser JavaScript Runtime
│
└── Window Object
    │
    └── document
        │
        └── DOM Tree
            ├── html
            ├── head
            └── body
```

---

## 13. What is the relationship between Window and BOM?

**Answer:**
BOM means **Browser Object Model**. It refers to browser-related objects and features such as `location`, `history`, `navigator`, and `screen`.

```text
Window Object
│
├── location
├── history
├── navigator
└── screen
```

---

## 14. Is `setTimeout()` implemented by V8?

**Answer:**
No. The browser provides the timer API, while V8 executes the JavaScript code that calls it.

```text
JavaScript
    ↓
V8
    ↓
Browser Timer API
    ↓
Task Queue
    ↓
Event Loop
    ↓
Call Stack
```

---

## 15. Where does the Task Queue exist?

**Answer:**
The Task Queue is part of the **Browser JavaScript Runtime's event-loop system**. It stores tasks that are ready to be processed by JavaScript.

```text
Browser JavaScript Runtime
│
├── JavaScript Engine
│   └── V8
│       └── Call Stack
│
├── Task Queue
├── Microtask Queue
└── Event Loop
```

---

## 16. Where does the Microtask Queue exist?

**Answer:**
The Microtask Queue is part of the JavaScript asynchronous execution model. It contains jobs such as Promise callbacks and is processed by the event-loop mechanism.

Examples:

* Promise callbacks
* `queueMicrotask()`
* `MutationObserver` callbacks

```text
Browser JavaScript Runtime
│
├── JavaScript Engine
│   └── V8
│
├── Microtask Queue
│
└── Event Loop
```

---

## 17. Where does the Event Loop exist?

**Answer:**
The Event Loop is part of the **Browser JavaScript Runtime**. It coordinates the Call Stack, Task Queue, Microtask Queue, and browser processing.

```text
Browser JavaScript Runtime
│
├── JavaScript Engine
│   └── V8
│       └── Call Stack
│
├── Task Queue
├── Microtask Queue
└── Event Loop
```

---

## 18. What happens when JavaScript accesses `window.document`?

**Answer:**
V8 executes the JavaScript expression, and the browser-provided Window Object provides access to the `document` object.

```text
JavaScript Code
      ↓
     V8
      ↓
window.document
      ↓
Window Object
      ↓
document
      ↓
DOM
```

---

## 19. Do all Window properties come from V8?

**Answer:**
No. Browser-specific properties and APIs are provided by the browser, while V8 provides JavaScript language features and built-in objects.

```text
Browser JavaScript Runtime
│
├── JavaScript Engine
│   └── V8
│       ├── Object
│       ├── Array
│       ├── Promise
│       ├── Map
│       └── Function
│
└── Window Object
    ├── document
    ├── location
    ├── history
    ├── navigator
    └── localStorage
```

---

## 20. How does the browser expose native browser features to JavaScript?

**Answer:**
The browser implements browser features natively and exposes JavaScript-accessible interfaces for those features.

```text
Browser JavaScript Runtime
│
├── Browser Native Implementation
│   ├── Window
│   ├── Document
│   ├── Location
│   ├── History
│   └── Navigator
│
├── Web APIs
│
└── JavaScript Engine
    └── V8
        └── JavaScript Code
```

---

# Complete Browser JavaScript Runtime Architecture

This is the **main architecture** of the entire topic. It should be kept once at the end instead of repeating the complete structure throughout the README.

```text
Browser JavaScript Runtime
│
├── Window Object
│   ├── document
│   ├── location
│   ├── history
│   ├── navigator
│   ├── screen
│   ├── localStorage
│   └── sessionStorage
│
├── Web APIs
│   ├── DOM APIs
│   ├── Timer APIs
│   ├── Fetch API
│   ├── WebSocket
│   └── Other Web APIs
│
├── JavaScript Engine
│   └── V8
│       ├── Parser
│       ├── Compiler
│       ├── Heap
│       ├── Call Stack
│       └── JavaScript Execution
│
├── Microtask Queue
├── Task Queue
├── Event Loop
└── Rendering System
```

## Core Relationships

```text
Window Object
     │
     ├── document ──→ DOM
     ├── location
     ├── history
     ├── navigator
     └── storage


Web APIs
     │
     ├── Timers
     ├── Fetch
     ├── WebSocket
     └── DOM APIs


JavaScript Engine
     │
     └── V8
         └── Executes JavaScript


Asynchronous Flow
     │
     ├── Web APIs
     │
     ├── Task Queue
     ├── Microtask Queue
     │
     └── Event Loop
             ↓
         Call Stack
             ↓
            V8
```

## Core Idea

> **V8 executes JavaScript.**

> **Window provides the browser's global object.**

> **Web APIs provide browser capabilities.**

> **Task Queue and Microtask Queue hold asynchronous work.**

> **Event Loop coordinates when queued work can enter the Call Stack.**

> **The Browser JavaScript Runtime is the complete environment that brings these pieces together.**
