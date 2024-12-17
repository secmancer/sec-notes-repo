### Introduction
- Websites primarily use JavaScript for functionality, while HTML and CSS define structure and design.
- The source code, though client-side, is executed in browsers and often hidden from view.
- Understanding a website’s client-side functions requires looking at its source code.
- This section explains how to uncover and analyze the source code for better understanding.

### HTML
- Visiting any website, we can press `[CTRL + U]` on our browser to open the browser's source code viewer.
- This allows us to view the code of the website, specifically, the `HTML` portion of it.

### CSS
- `CSS` code is can either:
	- be defined `internally` within the same `HTML` file between `<style>` elements
	- be defined `externally` in a separate `.css` file and referenced within the `HTML` code.
- In this case, we see that the `CSS` is internally defined.
```html
    <style>
        *,
        html {
            margin: 0;
            padding: 0;
            border: 0;
        }
        ...SNIP...
        h1 {
            font-size: 144px;
        }
        p {
            font-size: 64px;
        }
    </style>
```
- If a page `CSS` style is externally defined, the external `.css` file is referred to with the `<link>` tag within the HTML head.
```html
<head>
    <link rel="stylesheet" href="style.css">
</head>
```


### JavaScript
- The same concept applies to `JavaScript`. 
- It can be internally written between `<script>` elements.
- However, it can also be written into a separate `.js` file and referenced within the `HTML` code.
- We can see in our `HTML` source that the `.js` file is referenced externally:
```html
<script src="secret.js"></script>
```
- We can check out the script by clicking on `secret.js`, which should take us directly into the script. When we visit it, we see that the code is very complicated and cannot be comprehended:
```javascript
eval(function (p, a, c, k, e, d) { e = function (c) { '...SNIP... |true|function'.split('|'), 0, {}))
```
- The reason behind this is `code obfuscation`. What is it? How is it done? Where is it used?


### Questions
- Repeat what you learned in this section, and you should find a secret flag, what is it?
	- HTB{4lw4y5_r34d_7h3_50urc3}