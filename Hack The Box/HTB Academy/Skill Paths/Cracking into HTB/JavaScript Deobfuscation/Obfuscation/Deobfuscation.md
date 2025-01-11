### Overview
- Deobfuscation is the process of reversing code obfuscation to make it readable and understandable.
- Tools and methods are available for automatic code beautification and deobfuscation.



### **1. Beautification**
- #### Minified JavaScript
	- **Minified code**: A single-line JavaScript code optimized for size and performance.
	- **Beautification**: The process of formatting the code into a human-readable format.
- #### Browser Dev Tools Example:
	1. **Firefox Steps**:
	    - Open the debugger: `[CTRL + SHIFT + Z]`.
	    - Select the script (e.g., `secret.js`).
	    - Click the `{ }` button to **Pretty Print** the script.
- #### Tools for Beautification:
	- **Browser Dev Tools**.
	- **Online Tools**: Websites like Beautifier.
	- **Code Editor Plugins**: Prettier or Beautifier.
- ##### Example of Minified Code:
```javascript
eval(function (p, a, c, k, e, d) { ... });
```
- #### Outcome:
	- Beautified code is easier to read but may still be obfuscated.



### **2. Deobfuscation**
- Beautification alone may not suffice for heavily obfuscated code.
- Specialized tools or manual intervention may be required.
- #### Tools for Deobfuscation:
	- **UnPacker**: A tool to deobfuscate packed JavaScript code.
- ##### Example Workflow:
	1. Copy the obfuscated script into UnPacker.
	2. Click the **UnPack** button.
	3. Ensure no empty lines exist before the script to avoid errors.
- ##### Example Output:
```javascript
function generateSerial() {
  var xhr = new XMLHttpRequest;
  var url = "/serial.php";
  xhr.open("POST", url, true);
  xhr.send(null);
};
```



### **3. Manual Reverse Engineering**
- Required for **custom obfuscation** or highly encoded scripts.
- Use techniques such as:
    - Identifying the return values at the end of obfuscated scripts.
    - Using `console.log` to analyze intermediate steps.
- #### Advanced Topics:
	- Advanced deobfuscation may require understanding:
	    - How the code was obfuscated.
	    - Custom obfuscation techniques.
	- Resources: **Secure Coding 101 module** for in-depth learning.



### Key Takeaways
1. Start with beautification tools for basic readability.
2. Use deobfuscation tools like UnPacker for packed code.
3. Resort to manual reverse engineering for custom or advanced obfuscation.



### Questions
- Using what you learned in this section, try to deobfuscate 'secret.js' in order to get the content of the flag. What is the flag?
	- HTB{1_4m_7h3_53r14l_g3n3r470r!}