### Beautify
- The current code is minified, written in a single line.
- To format it properly, we need to beautify the code.
- Browser Dev Tools (e.g., Firefox) can be used to pretty-print the script by opening the debugger (`CTRL+SHIFT+Z`) and clicking the `{ }` button to format it.
- Alternatively, online tools like Prettier or Beautifier can also be used to beautify the script.
- Let’s copy and process the `secret.js` script.
```javascript
eval(function (p, a, c, k, e, d) { e = function (c) { return c.toString(36) }; if (!''.replace(/^/, String)) { while (c--) { d[c.toString(a)] = k[c] || c.toString(a) } k = [function (e) { return d[e] }]; e = function () { return '\\w+' }; c = 1 }; while (c--) { if (k[c]) { p = p.replace(new RegExp('\\b' + e(c) + '\\b', 'g'), k[c]) } } return p }('g 4(){0 5="6{7!}";0 1=8 a();0 2="/9.c";1.d("e",2,f);1.b(3)}', 17, 17, 'var|xhr|url|null|generateSerial|flag|HTB|flag|new|serial|XMLHttpRequest|send|php|open|POST|true|function'.split('|'), 0, {}))
```
- Both websites format the code well, but it’s still hard to read due to minification and obfuscation.
- Beautifying the code alone isn’t sufficient since the code is also obfuscated.
- Deobfuscation tools are needed to make the code readable.

### Deobfuscate
- We can find many good online tools to deobfuscate JavaScript code.
- That way, we can turn it into something we can understand. 
- One such tool is [UnPacker](https://matthewfl.com/unPacker.html).
- Copying our above-obfuscated code, we can run it in UnPacker by clicking the `UnPack` button.

> Tip: Ensure you do not leave any empty lines before the script, as it may affect the deobfuscation process and give inaccurate results.

- The tool gives us this in return:
```javascript
function generateSerial() {
  ...SNIP...
  var xhr = new XMLHttpRequest;
  var url = "/serial.php";
  xhr.open("POST", url, true);
  xhr.send(null);
};
```
- As previously mentioned, the above-used method of obfuscation is `packing`. 
- Another way of `unpacking` such code is to find the `return` value at the end and use `console.log` to print it instead of executing it.

### Reverse Engineering
- Though these tools help us clear up the code into something we can at least understand, more obfuscated and encoded code can become more difficult for these tools to work effectively.
- This is true with code obfuscated with custom obfuscation tools.
- Therefore, having a good background in reverse engineering helps out in further deobfuscating code in places where the automated tools have trouble doing.

### Questions
- Using what you learned in this section, try to deobfuscate 'secret.js' in order to get the content of the flag. What is the flag?
	- HTB{1_4m_7h3_53r14l_g3n3r470r!}