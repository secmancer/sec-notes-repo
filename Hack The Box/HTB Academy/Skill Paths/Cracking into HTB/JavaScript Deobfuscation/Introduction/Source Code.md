### **Understanding the Components of Source Code**
- Modern websites use a combination of **HTML**, **CSS**, and **JavaScript** to create their structure, design, and functionality. 
- This section focuses on understanding how to locate, view, and analyze these components, culminating in the identification of **JavaScript obfuscation**, a technique used to obscure code functionality.

### **1. HTML - The Structure**
- **Purpose**: Defines the basic structure and content of a webpage (e.g., headings, paragraphs, input fields).
- **How to View**:
    - In the browser, press **`CTRL + U`** to open the source view.
    - Alternatively, use the browser's **Inspect Element** feature (**`CTRL + SHIFT + I`**) to analyze specific elements interactively.
- **Example**:
    ```html
    <h1>Secret Serial Generator</h1>
    <script src="secret.js"></script>
    ```
    - The HTML snippet shows the structure and references an external JavaScript file (`secret.js`).



### **2. CSS - The Styling**
- **Purpose**: Defines the visual appearance and layout of HTML elements.
- **Types**:
    - **Inline CSS**: Written within individual HTML elements.
        ```html
        <h1 style="color: blue;">Hello, World!</h1>
        ```
    - **Internal CSS**: Written inside a `<style>` block within the HTML file.
        ```html
        <style>
            h1 {
                font-size: 144px;
                color: blue;
            }
        </style>
        ```
    - **External CSS**: Linked as a separate file.
        ```html
        <head>
            <link rel="stylesheet" href="style.css">
        </head>
        ```



### **3. JavaScript - The Functionality**
- **Purpose**: Adds dynamic functionality to the webpage, such as input validation, animations, or API interactions.
- **Types**:
    - **Inline JavaScript**: Embedded directly within HTML elements.
        ```html
        <button onclick="alert('Hello!')">Click Me</button>
        ```
    - **Internal JavaScript**: Written within a `<script>` block in the HTML file.
        ```html
        <script>
            function greet() {
                alert('Welcome!');
            }
        </script>
        ```
    - **External JavaScript**: Linked as a separate `.js` file.
        ```html
        <script src="script.js"></script>
        ```



### **4. Analyzing External JavaScript**
- In the given example, the webpage references an external JavaScript file:
    ```html
    <script src="secret.js"></script>
    ```
- **How to View**:
    - Click the link to `secret.js` in the source code or navigate to it directly in the browser.



### **5. Encountering Obfuscated JavaScript**
- **What It Looks Like**:
    - The `secret.js` file contains code that is **obfuscated** to obscure its functionality.
    - Example:
        ```javascript
        eval(function (p, a, c, k, e, d) { e = function (c) { ... |true|function'.split('|'), 0, {}))
        ```
    - This unreadable code is typical of obfuscation techniques designed to:
        - Protect intellectual property.
        - Hide malicious intent.
        - Reduce readability for reverse engineering.



### **Next Steps**
- **Understanding Obfuscation**:
    - Learn what code obfuscation is, its common techniques, and its legitimate and malicious use cases.
    - Explore how to deobfuscate and analyze such code.



### Questions
- Repeat what you learned in this section, and you should find a secret flag, what is it?
	- HTB{4lw4y5_r34d_7h3_50urc3}