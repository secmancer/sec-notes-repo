### Introduction
- Code obfuscation is hard to do manually, so plenty of tools exist for us to use instead.
- While many exist freely online, many malicious actors or even profession developers make their own suite of tools to make it much more difficult to deobfuscate.

### Running code
- Let's attempt to obfuscate this:
```javascript
console.log('HTB JavaScript Deobfuscation Module');
```
- First, we'll test this code in cleartext to see how it works.
	- We can use [JSConsole](https://jsconsole.com) to do that.
- Running it, this line of code prints`HTB JavaScript Deobfuscation Module`.

### Minifying code
- JavaScript minification reduces code readability by placing everything in a single line.
- Tools like `javascript-minifier` simplify minifying code by removing whitespace and reducing variable names.
- Minified code can still function correctly and is often saved with a `.min.js` extension.
- We can test minified code using tools like JSConsole.

> Note: Code minification is not exclusive to JavaScript, and can be applied to many other languages, as can be seen on [javascript-minifier](https://javascript-minifier.com/).

### Packing code
-  Now, let us obfuscate our line of code to make it more obscure and difficult to read.
- First, we will try [BeautifyTools](http://beautifytools.com/javascript-obfuscator.php) to obfuscate our code.
```javascript
eval(function(p,a,c,k,e,d){e=function(c){return c};if(!''.replace(/^/,String)){while(c--){d[c]=k[c]||c}k=[function(e){return d[e]}];e=function(){return'\\w+'};c=1};while(c--){if(k[c]){p=p.replace(new RegExp('\\b'+e(c)+'\\b','g'),k[c])}}return p}('5.4(\'3 2 1 0\');',6,6,'Module|Deobfuscation|JavaScript|HTB|log|console'.split('|'),0,{}))
```
- We see that our code became much more obfuscated and difficult to read. 
- We can copy this code into [https://jsconsole.com](https://jsconsole.com), to verify that it still does its main function.
- We see that we get the same output.

> Note: The above type of obfuscation is known as "packing", which is usually recognizable from the six function arguments used in the initial function "function(p,a,c,k,e,d)".

- Packer obfuscation tools convert code into a packed format using functions like `(p,a,c,k,e,d)` to rebuild it during execution.
- The `(p,a,c,k,e,d)` sequence can vary between different packers but follows a specific order to decode.
- Despite reducing readability, some main strings may still be visible, revealing functionality.
- For stronger obfuscation, alternative methods may be required.

