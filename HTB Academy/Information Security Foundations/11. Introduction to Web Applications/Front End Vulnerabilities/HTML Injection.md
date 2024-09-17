**Importance of Validation and Sanitization**:
- **Front End vs. Back End**: User input validation and sanitization should be performed on both the front end and back end. Some user inputs are processed and rendered entirely on the front end, making it crucial to validate and sanitize these inputs to prevent vulnerabilities.



**HTML Injection**:
- **Definition**: Occurs when unfiltered user input is displayed on the web page, either by retrieving previously submitted data (e.g., user comments from a database) or by directly displaying unfiltered input through JavaScript.
- **Risks**:
    - **Malicious HTML Code**: Users can inject HTML or JavaScript code that may trick others or perform malicious actions (e.g., sending login credentials to a malicious server).
    - **Web Page Defacing**: Attackers can inject HTML to alter the page’s appearance, insert malicious ads, or completely change the content, leading to reputational damage.


**Example of HTML Injection**:
- **Scenario**: A basic web page prompts for user input and displays it:
```
<!DOCTYPE html>
<html>
<body>
    <button onclick="inputFunction()">Click to enter your name</button>
    <p id="output"></p>

    <script>
        function inputFunction() {
            var input = prompt("Please enter your name", "");

            if (input != null) {
                document.getElementById("output").innerHTML = "Your name is " + input;
            }
        }
    </script>
</body>
</html>
```
- **Test for HTML Injection**: If no input sanitization is present, entering HTML code such as:
```
<style> body { background-image: url('https://academy.hackthebox.com/images/logo.svg'); } </style>
```
will change the web page's background image.



**Consequences and Mitigation**:
- **Immediate Effect**: Changes made through HTML injection are only temporary and will reset upon refreshing the page.
- **Mitigation**:
    - **Sanitize Inputs**: Always sanitize user inputs to remove or escape any potentially harmful code before displaying it on the page.
    - **Use Safe Methods**: For user input, prefer using methods that automatically handle escaping, such as textContent instead of innerHTML.


## Questions
- What text would be displayed on the page if we use the following payload as our input: "<"a href="http://www.hackthebox.com">Click Me<"/a">
	- Your name is Click Me