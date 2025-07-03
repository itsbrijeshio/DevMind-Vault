---
tags:
  - JS
---
### 🔍What is the Event-Loop?
---
The **Event-Loop** is the mechanism that handles **[[Asynchronous||asynchronous]]** operations in JavaScript.
[[JavaScript]] is the **[[single-threaded]]** language, that means it can only do one thing at a time.

The Event Loop handles them by managing **callbacks**, **promises**, and other async tasks behind the scenes without blocking the main thread.

### 🤔 Why Do We Need the Event Loop?

---

JavaScript runs in environments like **[[browsers]]** and **[[NodeJS]]** where:
- Users might click something
- Data comes from a server
- You want to run a task **after a delay**

We can't block the main thread. The event loop lets **async tasks** finish **in the background** and then puts their results back in the queue to execute **when the thread is free**.

---
### 🧠 Execution Order in JavaScript (with Event Loop)

1. **🔁 Synchronous Code First**
    
    - All normal code runs **first** — top to bottom.
        
    
    ```js
    console.log("A");
    ```
    
2. **🌐 Web APIs Handle Async Tasks**
    
    - Things like:
        
        - `setTimeout`
            
        - `setInterval`
            
        - `fetch`
            
        - `event listeners`
            
    - Are **registered** and handled outside the main thread.
        
3. **🧪 Promises / async-await → Microtasks**
    
    - `Promise.then`, `catch`, `finally`, and `await` go to **Microtask Queue**.
        
    - These run **immediately after** synchronous code but **before** any `setTimeout`.
        
4. **⏱️ Macrotasks (like setTimeout) Come After Microtasks**
    
    - Even if you write `setTimeout(..., 0)` — it waits until:
        
        - All synchronous code ✅
            
        - All microtasks ✅
            
        - Then enters the **Callback Queue**
            

---
### 🔁 Example with Output

```js
console.log("1");

setTimeout(() => {
  console.log("2");
}, 0);

Promise.resolve().then(() => {
  console.log("3");
});

console.log("4");
```

### ✅ Output:

```
1
4
3
2
```

---

### 🧾 Final Flow Summary:

| Step | What Runs                           |
| ---- | ----------------------------------- |
| 1    | Synchronous code (call stack)       |
| 2    | Microtask Queue (Promises, `await`) |
| 3    | Macrotask Queue (setTimeout, etc)   |

---

### 📦 JavaScript Call Stack Handling

```js
function a(){
  console.log("Function A");
}

function b(){
  console.log("Function B");
  a();
}

function c(){
  console.log("Function C");
  b();
}

function d(){
  console.log("Function D");
  c();
}

function e(){
  console.log("Function E");
  d();
}

e();
```

---

### ✅ **Output:**

```
Function E
Function D
Function C
Function B
Function A
```

---

### 🧠 Behind the Scenes — Call Stack

#### **Push Phase (Execution starts)**

1. `e()` is called → stack: `[e]`
    
2. inside `e()`, `d()` is called → stack: `[e, d]`
    
3. inside `d()`, `c()` is called → stack: `[e, d, c]`
    
4. inside `c()`, `b()` is called → stack: `[e, d, c, b]`
    
5. inside `b()`, `a()` is called → stack: `[e, d, c, b, a]`
    
6. `a()` logs "Function A" → finishes → stack: `[e, d, c, b]`
    

#### **Pop Phase (Returning)**

Now functions return one by one:

- `a()` finishes ➝ `b()` finishes ➝ `c()` ➝ `d()` ➝ `e()`
    
- Stack becomes empty
    

```
POP → a
POP → b
POP → c
POP → d
POP → e
```

---

### 🔁 Final Summary:

|Order|What Happens|
|---|---|
|Push Stack|`e()` → `d()` → `c()` → `b()` → `a()`|
|Print Logs|E → D → C → B → A|
|Pop Stack|a → b → c → d → e|
