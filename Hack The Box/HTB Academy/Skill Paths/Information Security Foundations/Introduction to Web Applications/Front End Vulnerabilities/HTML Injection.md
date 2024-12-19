### Introduction
- **Dual Validation & Sanitization**: Validate and sanitize user input on both the front end and back end, as some input may only be processed and rendered on the front end.
- **HTML Injection Risk**: Unfiltered user input displayed on the page can lead to HTML injection, whether from back-end-retrieved data or directly processed input via JavaScript on the front end.
- **Malicious Input Examples**: Attackers can inject malicious HTML, such as fake login forms, to steal user credentials or perform phishing attacks.
- **Web Page Defacement**: HTML injection can be used to alter the page's appearance, insert malicious ads, or completely change the page, causing reputational harm to the host organization.
- **Critical Need for Input Control**: Effective validation and sanitization reduce the risk of such attacks, protecting users and the organization's reputation.



### Example
- The following example is a very basic web page with a single button "`Click to enter your name`." 
- When we click on the button, it prompts us to input our name and then displays our name as "`Your name is ...`".
![HTML Example](https://academy.hackthebox.com/storage/modules/75/web_apps_html_injection_5.jpg)
- If no input sanitization is in place, this is potentially an easy target for `HTML Injection` and `Cross-Site Scripting (XSS)` attacks. 
- We take a look at the page source code and see no input sanitization in place whatsoever, as the page takes user input and directly displays it.
```html
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
- To test for `HTML Injection`, we can simply input a small snippet of `HTML` code as our name, and see if it is displayed as part of the page.
- We will test the following code, which changes the background image of the web page/
```html
<style> body { background-image: url('https://academy.hackthebox.com/images/logo.svg'); } </style>
```
- Once we input it, we see that the web page's background image changes instantly:
![HTML Example](https://academy.hackthebox.com/storage/modules/75/web_apps_html_injection_6.jpg)
- In this example, as everything is being carried out on the front end, refreshing the web page would reset everything back to normal.



## Questions
- What text would be displayed on the page if we use the following payload as our input: <a href="http://www.hackthebox.com">Click Me</a>
	- Your name is Click Me