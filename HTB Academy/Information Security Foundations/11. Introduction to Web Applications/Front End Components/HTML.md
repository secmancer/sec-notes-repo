**HTML (HyperText Markup Language):**
- **Core Component:** HTML forms the foundation of web pages, defining the structure and content visible in a web browser.
- **Basic Example:**
```
<!DOCTYPE html>
<html>
    <head>
        <title>Page Title</title>
    </head>
    <body>
        <h1>A Heading</h1>
        <p>A Paragraph</p>
    </body>
</html>
```
**Displays:**
- A heading ("A Heading")
- A paragraph ("A Paragraph")


**HTML Structure:**
- HTML elements are organized in a tree structure, similar to XML.
    - Example:
```
document
 - html
   -- head
      --- title
   -- body
      --- h1
      --- p
```
**Tags:**
- HTML elements are enclosed in opening and closing tags (e.g., `<p>...</p>` for paragraphs).
- Tags can include attributes like `id` or `class` for styling (e.g., `<p id='para1'>`).


**URL Encoding (Percent-Encoding):**
- **Purpose:** Converts unsafe ASCII characters in URLs into a format that browsers can interpret.
- **Encoding:** Replaces characters with a `%` followed by two hexadecimal digits.
    - **Examples:**
        - Single-quote (`'`) becomes `%27`
        - Space becomes `%20` or `+`
- **Common Encodings:**
    - Space: `%20`
    - Exclamation mark (`!`): `%21`
    - Double quote (`"`): `%22`
    - Hash (`#`): `%23`
    - Dollar sign (`$`): `%24`
    - Percent (`%`): `%25`
    - Ampersand (`&`): `%26`
    - Single quote (`'`): `%27`
    - Parentheses: `(` becomes `%28`, `)` becomes `%29`



**DOM (Document Object Model):**
- **Definition:** A platform and language-neutral interface that allows programs and scripts to dynamically access and update the content, structure, and style of a document.
- **DOM Types:**
    - **Core DOM:** Standard model for all document types.
    - **XML DOM:** Standard model for XML documents.
    - **HTML DOM:** Standard model for HTML documents.
- **Elements in HTML DOM:**
    - `<head>`: Contains elements like `<title>`, `<style>`, and `<script>` (not displayed on the page).
    - `<body>`: Contains main content elements like `<h1>`, `<p>`, etc.
- **Usage:**
    - **Accessing Elements:** Use `document.head`, `document.h1`, etc., to interact with elements.
    - **Understanding Structure:** Helps locate elements, view source code, and identify potential issues.
    - **Front-End Vulnerabilities:** Understanding DOM is useful for exploiting vulnerabilities like XSS to manipulate or create elements.



**Tools:**
- **URL Encoding/Decoding Tools:** Online tools and Burp Suite for encoding/decoding characters and strings.
- **Viewing HTML Source:** Inspect element features in browsers to view and manipulate HTML DOM.


## Questions
- What is the HTML tag used to show an image?
	- "< img >"