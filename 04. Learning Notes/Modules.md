
---

## ✅ What are Modules in [[JavaScript]]?

**Modules** are reusable pieces of code that are split into files and can be imported/exported between files. They help organize your code by splitting it into smaller, manageable parts.

There are two types of modules in JavaScript:

1. **ES Modules (ESM)** – Modern JavaScript module system using `import/export`.
    
2. **CommonJS** – Used mostly in Node.js with `require/module.exports`.
    

---

## 🧠 Why Use Modules?

|Benefit|Description|
|---|---|
|✅ Reusability|Use the same code (e.g., a function or class) in multiple places|
|✅ Maintainability|Easier to debug and update code in smaller files|
|✅ Separation of Concerns|Keeps logic (e.g., API calls, UI, utilities) separate and organized|
|✅ Scope Isolation|Variables and functions in one module won't pollute global scope|
|✅ Better collaboration|Teams can work on different modules without conflicts|

---

## 🛠️ How to Use Modules

### 1. **ES Modules (Browser or Node >= v14 with `"type": "module"`)**

#### ➕ Exporting

```js
// utils.js
export const sum = (a, b) => a + b;
export const multiply = (a, b) => a * b;
```

#### ➕ Importing

```js
// app.js
import { sum, multiply } from './utils.js';

console.log(sum(2, 3)); // 5
```

#### ➕ Default Export

```js
// math.js
export default function subtract(a, b) {
  return a - b;
}
```

```js
// app.js
import subtract from './math.js';
console.log(subtract(10, 3)); // 7
```

---

### 2. **CommonJS (Used in Node.js)**

#### ➕ Exporting

```js
// utils.js
function sum(a, b) {
  return a + b;
}

module.exports = { sum };
```

#### ➕ Importing

```js
// app.js
const { sum } = require('./utils');
console.log(sum(2, 3)); // 5
```

---

## 💡 Best Practices

- Use **ESM** (`import/export`) for modern apps and browser compatibility.
    
- Use **default exports** when there's one main thing to export.
    
- Group utilities into files like `auth.js`, `db.js`, `utils.js`, etc.
    
- Always use relative or absolute paths properly (`./`, `../`, or aliases if configured).
    
