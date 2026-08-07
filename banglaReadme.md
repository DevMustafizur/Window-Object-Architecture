# Window Object কী?

**`window` object** হলো **Browser** কর্তৃক প্রতিটি Web Page-এর জন্য প্রদান করা **Global Object**। এটি বর্তমান Browser Window (অথবা Tab)-কে প্রতিনিধিত্ব করে এবং Browser-এর JavaScript Environment-এর **Root Object** হিসেবে কাজ করে।

যখন Browser একটি Web Page লোড করে, তখন JavaScript Code চালানোর আগেই Browser স্বয়ংক্রিয়ভাবে একটি `window` object তৈরি করে। এই Object-এর মাধ্যমেই JavaScript **Browser Object Model (BOM)**, **Document Object Model (DOM)** এবং বিভিন্ন **Web API**-তে প্রবেশাধিকার পায়।

## সংজ্ঞা

> **`window` object হলো Browser Environment-এর Global Object। এটি বর্তমান Browser Window বা Tab-কে প্রতিনিধিত্ব করে এবং Browser-এর বিভিন্ন Feature, DOM এবং Web API-তে প্রবেশাধিকার প্রদান করে।**

---

# `window` Object-এর Property গুলো কীভাবে তৈরি হয়?

## প্রশ্ন

**`window` object-এর Property গুলো কীভাবে তৈরি হয়?**

## উত্তর

`window` object-এর Property গুলো **JavaScript দ্বারা নয়**, বরং **Browser** দ্বারা তৈরি হয়।

যখন একটি Web Page লোড হয়, তখন Browser প্রথমে একটি JavaScript Environment তৈরি করে এবং এরপর `window` object তৈরি করে। তারপর Browser বিভিন্ন Built-in Object, Function, Constructor এবং Value তৈরি বা প্রকাশ (Expose) করে এবং সেগুলোকে `window` object-এর Property হিসেবে যুক্ত করে।

---

## প্রশ্ন

**`window` object-এর Built-in Property গুলো Browser-এর ভিতরে (Internally) কীভাবে তৈরি ও যুক্ত করা হয়?**

## উত্তর

`window` object-এর Built-in Property গুলো Browser-এর **Native Implementation** দ্বারা তৈরি হয়, JavaScript দ্বারা নয়।

Browser-এর Engine (যেমন Chromium, Gecko বা WebKit) অভ্যন্তরীণভাবে **Native Class** ব্যবহার করে বিভিন্ন Object তৈরি করে। এই Native Class-গুলো সাধারণত C++ বা Rust-এর মতো Language-এ Implement করা হয়।

উদাহরণস্বরূপ Browser-এর অভ্যন্তরে নিচের মতো Class থাকে—

* `Document`
* `Location`
* `History`
* `Navigator`
* `Screen`
* `Storage`

Browser এই Class-গুলোর Instance তৈরি করে।

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
Object Instance তৈরি
```

Object তৈরি হওয়ার পরে Browser সেগুলোকে `window` object-এর Property হিসেবে Expose করে।

কিছু Property **Data Property** হিসেবে যুক্ত হয়, আবার কিছু Property **Getter** এবং **Setter** Function (Accessor Property) ব্যবহার করে Expose করা হয়।

ধারণাগতভাবে পুরো Processটি এমন—

```text
Browser
    │
    ▼
Window Object তৈরি
    │
    ▼
Internal Native Class-এর Instance তৈরি
    │
    ├── new Document()
    ├── new Location()
    ├── new History()
    ├── new Navigator()
    ├── new Screen()
    └── new Storage()
    │
    ▼
Window Object-এর Property হিসেবে যুক্ত বা Expose করা
(Data Property অথবা Getter/Setter-এর মাধ্যমে)
    │
    ▼
JavaScript থেকে Access করা যায়

window.document
window.location
window.history
window.navigator
```

উদাহরণ—

```javascript
window.document;
window.location;
window.history;
window.navigator;
```

JavaScript-এর দৃষ্টিকোণ থেকে এগুলো সাধারণ Property মনে হলেও, বাস্তবে এগুলো Browser-এর Native Class থেকে তৈরি হয় এবং JavaScript Code চালু হওয়ার আগেই `window` object-এর সাথে যুক্ত হয়ে যায়।

---

# `window` Object-এর Prototype Chain কী?

## প্রশ্ন

**`window` object-এর Prototype Chain কী?**

## উত্তর

JavaScript-এর অন্যান্য Object-এর মতো `window` object-ও একটি **Prototype Chain** অনুসরণ করে।

`window` object-এর Prototype Chain হলো—

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

### ব্যাখ্যা

* **`window`** হলো Browser দ্বারা তৈরি প্রকৃত Global Object।
* **`Window.prototype`**-এ এমন Method এবং Property থাকে, যেগুলো সকল `Window` Object-এর জন্য Shared।
* **`EventTarget.prototype`** থেকে `window` Event System-এর সুবিধা পায়। এর মাধ্যমে `addEventListener()` এবং `removeEventListener()` ব্যবহার করে `click`, `load`, `resize` ইত্যাদি Event Handle করা যায়।
* **`Object.prototype`** JavaScript-এর সাধারণ Object Method যেমন `toString()`, `hasOwnProperty()` এবং `valueOf()` প্রদান করে।
* **`null`** হলো Prototype Chain-এর শেষ ধাপ।

### উদাহরণ

```javascript
window instanceof Window;      // true
window instanceof EventTarget; // true
window instanceof Object;      // true

Object.getPrototypeOf(window) === Window.prototype; // true
```

অর্থাৎ, `window` object প্রথমে `Window.prototype` থেকে, এরপর `EventTarget.prototype` থেকে এবং সবশেষে `Object.prototype` থেকে Property ও Method Inherit করে।
