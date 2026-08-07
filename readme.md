# What is the Window Object?

The **`window` object** is the **global object** provided by the web browser for every web page. It represents the browser window (or tab) where a page is running and serves as the **root object** of the browser's JavaScript environment.

When a browser loads a web page, it automatically creates a `window` object before executing any JavaScript code. This object provides access to the **Browser Object Model (BOM)**, the **Document Object Model (DOM)**, and many built-in **Web APIs**.

## Definition

> **The `window` object is the global object of the browser environment. It represents the current browser window or tab and provides access to browser features, the DOM, and Web APIs.**



# How Are the Properties of the `window` Object Created?

## Question

**How are the properties of the `window` object created?**

## Answer

The properties of the `window` object are created **by the browser**, not by JavaScript.

When a web page is loaded, the browser initializes a JavaScript environment and creates the `window` object. It then creates or exposes various built-in browser objects, functions, constructors, and values, attaching them as properties of `window`.


## How Are the Built-in Properties and Methods of the `window` Object Created and Attached Internally?

### Answer

The built-in members of the `window` object are provided by the **browser's native implementation**, not created by JavaScript code.

These members can generally be divided into two categories:

1. **Object properties** — such as `document`, `location`, `history`, and `navigator`
2. **Methods** — such as `alert()`, `confirm()`, `prompt()`, `print()`, and `setTimeout()`

---

### 1. Object Properties

For many browser objects, the browser internally creates an object using its native implementation and then exposes that object through the `window` object.

Examples include:

* `Document`
* `Location`
* `History`
* `Navigator`
* `Screen`
* `Storage`

Conceptually:

```text
Internal Native Classes
│
├── Document
├── Location
├── History
├── Navigator
├── Screen
└── Storage
        │
        ▼
Create Object Instances
        │
        ▼
Expose Objects through Window
```

Conceptually, this can be represented as:

```javascript
const document = new Document();
const location = new Location();
const history = new History();
const navigator = new Navigator();

window.document = document;
window.location = location;
window.history = history;
window.navigator = navigator;
```

The actual browser implementation is much more complex and does **not necessarily use JavaScript `new` expressions** like the example above. The example only demonstrates the relationship between the internal object instances and their `window` properties.

---

### 2. Window Methods

Some members of `window` are functions rather than objects.

Examples:

```javascript
window.alert();
window.confirm();
window.prompt();
window.print();
window.open();
window.close();
window.setTimeout();
window.setInterval();
window.requestAnimationFrame();
```

These methods are implemented by the browser's **native code** and exposed to JavaScript as methods of the `Window` interface.

Importantly, there is generally **no separate JavaScript class such as `Alert`, `Confirm`, or `Prompt`** whose instances provide these methods.

It is therefore incorrect to think of them like this:

```javascript
const alertObject = new Alert();      // ❌
const confirmObject = new Confirm();  // ❌

window.alert = alertObject.alert;
window.confirm = confirmObject.confirm;
```

Instead, conceptually, they are exposed as native functions belonging to the `Window` interface:

```text
Browser Native Implementation
        │
        ▼
      Window
        │
        ├── alert()              ← native method
        ├── confirm()            ← native method
        ├── prompt()             ← native method
        ├── print()              ← native method
        ├── open()               ← native method
        ├── close()              ← native method
        ├── setTimeout()         ← native method
        └── requestAnimationFrame()
```

From JavaScript, they are accessed as:

```javascript
window.alert("Hello");
window.confirm("Are you sure?");
window.prompt("Enter your name");
```

Because `window` is the global object, the `window.` prefix can usually be omitted:

```javascript
alert("Hello");

confirm("Are you sure?");

prompt("Enter your name");
```

---

## Important Distinction

```text
Window
│
├── Object Properties
│   │
│   ├── document   → Document object
│   ├── location   → Location object
│   ├── history    → History object
│   ├── navigator  → Navigator object
│   └── screen     → Screen object
│
└── Methods
    │
    ├── alert()              → native Window method
    ├── confirm()            → native Window method
    ├── prompt()             → native Window method
    ├── print()              → native Window method
    ├── open()               → native Window method
    ├── close()              → native Window method
    └── setTimeout()         → browser-provided function
```

### Summary

The browser does not create every `window` member in the same way.

**Object properties** such as `document`, `location`, and `history` represent browser-created objects that are exposed through `window`.

**Methods** such as `alert()`, `confirm()`, and `prompt()` are browser-provided native functions exposed through the `Window` interface. They do not require separate JavaScript classes such as `Alert`, `Confirm`, or `Prompt`.

> **Note:** The exact internal implementation differs between browser engines. The `new Class()` examples above are conceptual models used to explain the relationship; they should not be interpreted as the browser's actual source code.



## Question

**What is the prototype chain of the `window` object?**

## Answer

Like every JavaScript object, the `window` object inherits properties and methods through a **prototype chain**.

The prototype chain of the `window` object is:

```text
window
   │
   ▼
Window.prototype
   │
   ▼
EventTarget.prototype
   │
   ▼
Object.prototype
   │
   ▼
null
```

### Explanation

* **`window`** is the actual global object created by the browser.
* **`Window.prototype`** contains methods and properties shared by all `Window` objects.
* **`EventTarget.prototype`** allows the `window` object to dispatch and listen for events, such as `click`, `load`, and `resize`, using methods like `addEventListener()` and `removeEventListener()`.
* **`Object.prototype`** provides the standard JavaScript object methods, such as `toString()`, `hasOwnProperty()`, and `valueOf()`.
* **`null`** marks the end of the prototype chain.

### Example

```javascript
window instanceof Window;      // true
window instanceof EventTarget; // true
window instanceof Object;      // true

Object.getPrototypeOf(window) === Window.prototype; // true
```

Therefore, the `window` object inherits functionality from `Window.prototype`, which in turn inherits from `EventTarget.prototype`, and finally from `Object.prototype`.


# What Properties Does the `window` Object Contain?

The `window` object is the **root object** of the browser's JavaScript environment. It contains **hundreds of built-in properties** that expose the browser's features, JavaScript built-in objects, DOM, BOM, Web APIs, global methods, constructors, and global values.

These properties are created and exposed by the browser before your JavaScript code begins executing.

## Categories of `window` Properties

The properties of the `window` object can be grouped into the following categories.

### 1. DOM Properties

These properties provide access to the Document Object Model (DOM).

**Examples**

* `document`
* `customElements`

---

### 2. Browser Object Model (BOM) Properties

These properties provide access to browser-specific objects.

**Examples**

* `location`
* `history`
* `navigator`
* `screen`

---

### 3. Window Relationship Properties

These properties describe the relationship between browser windows, tabs, and frames.

**Examples**

* `parent`
* `top`
* `self`
* `frames`
* `opener`
* `length`

---

### 4. Storage Properties

These properties provide access to browser storage.

**Examples**

* `localStorage`
* `sessionStorage`
* `indexedDB`
* `caches`

---

### 5. Performance and Security Properties

These properties expose browser performance and security features.

**Examples**

* `performance`
* `crypto`
* `origin`
* `trustedTypes`
* `isSecureContext`
* `crossOriginIsolated`

---

### 6. Global Methods

These are built-in browser functions that are available globally.

**Examples**

* `fetch()`
* `alert()`
* `confirm()`
* `prompt()`
* `print()`
* `open()`
* `close()`
* `setTimeout()`
* `clearTimeout()`
* `setInterval()`
* `clearInterval()`
* `requestAnimationFrame()`

---

### 7. JavaScript Constructors

The browser exposes JavaScript's built-in constructors through the `window` object.

**Examples**

* `Object`
* `Array`
* `String`
* `Number`
* `Boolean`
* `Date`
* `Math`
* `JSON`
* `Map`
* `Set`
* `WeakMap`
* `WeakSet`
* `Promise`
* `Symbol`
* `BigInt`
* `Error`

---

### 8. DOM Constructors

The browser also exposes DOM-related constructors.

**Examples**

* `Node`
* `Element`
* `Attr`
* `Text`
* `Comment`
* `Document`
* `DocumentFragment`
* `HTMLElement`
* `HTMLDivElement`
* `HTMLImageElement`
* `HTMLAnchorElement`

---

### 9. Event Constructors

These constructors are used to create browser events.

**Examples**

* `Event`
* `UIEvent`
* `MouseEvent`
* `KeyboardEvent`
* `PointerEvent`
* `FocusEvent`
* `InputEvent`
* `CustomEvent`

---

### 10. Network and Communication APIs

These properties expose networking features.

**Examples**

* `fetch`
* `XMLHttpRequest`
* `WebSocket`
* `EventSource`
* `BroadcastChannel`
* `MessageChannel`

---

### 11. Global Values

These are built-in JavaScript global values.

**Examples**

* `Infinity`
* `NaN`
* `undefined`

---

### 12. Global Utility Functions

These are built-in JavaScript utility functions.

**Examples**

* `parseInt()`
* `parseFloat()`
* `isNaN()`
* `isFinite()`
* `encodeURI()`
* `decodeURI()`
* `encodeURIComponent()`
* `decodeURIComponent()`
* `atob()`
* `btoa()`
* `structuredClone()`

---

## Conceptual Structure

```text
Window
│
├── DOM
│   ├── document
│   └── customElements
│
├── Browser Object Model (BOM)
│   ├── location
│   ├── history
│   ├── navigator
│   └── screen
│
├── Window Relationships
│   ├── parent
│   ├── top
│   ├── self
│   └── opener
│
├── Storage
│   ├── localStorage
│   ├── sessionStorage
│   └── indexedDB
│
├── Performance & Security
│   ├── performance
│   ├── crypto
│   └── isSecureContext
│
├── Global Methods
│   ├── fetch()
│   ├── alert()
│   ├── setTimeout()
│   └── requestAnimationFrame()
│
├── JavaScript Constructors
│   ├── Object
│   ├── Array
│   ├── Promise
│   └── Map
│
├── DOM Constructors
│   ├── Node
│   ├── Element
│   ├── Document
│   └── HTMLElement
│
├── Event Constructors
│   ├── Event
│   ├── MouseEvent
│   └── KeyboardEvent
│
├── Network APIs
│   ├── fetch
│   ├── XMLHttpRequest
│   └── WebSocket
│
└── Global Values & Utilities
    ├── Infinity
    ├── NaN
    ├── parseInt()
    └── encodeURI()
```

## Summary

The `window` object acts as the **central access point** to the browser environment. Almost everything provided by the browser—such as the DOM, Browser Object Model (BOM), Web APIs, JavaScript constructors, event constructors, global methods, storage, networking, and browser information—is exposed through the `window` object as its properties. Because of this, the `window` object is considered the **entry point to the browser's JavaScript environment**.

