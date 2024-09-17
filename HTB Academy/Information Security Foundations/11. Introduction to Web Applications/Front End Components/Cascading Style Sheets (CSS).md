**CSS Overview:**
- **Purpose:** CSS is used to format and style HTML elements, such as setting font styles, colors, layout, and more.
- **Versions:** There are several versions of CSS, with each version introducing new capabilities and features. Browsers are updated to support these new features.



**Basic Example:**
```
body {
  background-color: black;
}

h1 {
  color: white;
  text-align: center;
}

p {
  font-family: helvetica;
  font-size: 10px;
}
```
**Explanation:**
- **`body`:** Sets the background color to black.
- **`h1`:** Sets the text color to white and centers the text.
- **`p`:** Sets the font family to Helvetica and the font size to 10px.



**CSS Syntax:**
- **Structure:** CSS uses curly brackets `{}` to define styles for HTML elements or classes. Properties are specified as `property: value;` within these brackets.
    - **Example Syntax:**
```
element {
  property: value;
}
```
- **Properties:** CSS allows setting various properties for HTML elements, including height, position, border, margin, padding, color, text alignment, font size, and more.


**Advanced Features:**
- **Animations:** CSS supports advanced animations using properties like `@keyframes`, `animation`, `animation-duration`, and `animation-direction`. These can be used to create complex animations and effects.
    - **Example:**
```
@keyframes example {
  from { opacity: 0; }
  to { opacity: 1; }
}

.animated-element {
  animation: example 2s ease-in-out;
}
```




**Usage:**
- **Integration with JavaScript:** CSS can be dynamically adjusted with JavaScript to create interactive and responsive web pages. For example, you can change styles based on user input or events.
- **Parallax Effects:** CSS can be used to create visual effects such as parallax scrolling and depth cards, enhancing user experience on web pages.



**Frameworks:**
- **Purpose:** CSS frameworks provide pre-designed style sheets and components to streamline and simplify the process of creating visually appealing web pages. They offer reusable design elements and are optimized for use with JavaScript.
- **Popular Frameworks:**
    - **Bootstrap:** A popular framework for responsive design and UI components.
    - **SASS (Syntactically Awesome Style Sheets):** A preprocessor that extends CSS with variables, nested rules, and more.
    - **Foundation:** A responsive front-end framework for creating flexible and adaptive web layouts.
    - **Bulma:** A modern CSS framework based on Flexbox, offering a range of responsive design components.
    - **Pure:** A minimalistic CSS framework designed to be small and modular.



**Additional Usage:**
- **XML and SVG:** CSS can also be used to style XML documents and SVG graphics.
- **Mobile Development:** CSS is essential for designing mobile application user interfaces (UI), providing a consistent and attractive layout across devices.


## Questions
- What is the CSS "property: value" used to make an HTML element's text aligned to the left?
	- text-align: left;