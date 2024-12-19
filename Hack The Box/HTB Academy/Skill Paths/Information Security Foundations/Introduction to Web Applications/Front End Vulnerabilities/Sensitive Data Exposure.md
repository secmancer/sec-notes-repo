### TLDR
- **Front-End Vulnerabilities**: While front-end components interact with the client-side and typically don't directly affect the back end, they can expose end users to attacks, potentially leading to unauthorized access or service disruptions if exploited, especially if admins are targeted.
- **Importance of Front-End Testing**: Even though back-end vulnerabilities are often the focus of web application penetration testing, front-end components should also be tested, as they can sometimes provide access to sensitive functionality, like admin panels.
- **Sensitive Data Exposure**: Sensitive data may be exposed in the HTML source code of a web page, visible through "View Page Source" in the browser. This could include credentials, hashes, or links that could aid attackers in exploiting the application or its infrastructure.
- **Accessing Page Source**: The page source can be viewed via browser options or tools like Burp Suite, even if right-click is disabled. It’s essential to inspect the page source for exposed sensitive data.
- **Reviewing Source Code**: When assessing a web application, reviewing the page source should be a primary step to identify low-hanging fruit, such as exposed credentials or hidden links, which could facilitate further exploitation.



### Example
-  At first glance, this login form does not look like anything out of the ordinary.
![HTML Example](https://academy.hackthebox.com/storage/modules/75/web_apps_login_form_.png)
- Let's take a look at at the page source.
```html
<form action="action_page.php" method="post">

    <div class="container">
        <label for="uname"><b>Username</b></label>
        <input type="text" required>

        <label for="psw"><b>Password</b></label>
        <input type="password" required>

        <!-- TODO: remove test credentials test:test -->

        <button type="submit">Login</button>
    </div>
</form>

</html>
```
- We see that the developers added some comments that they forgot to remove, which contain test credentials.
```html
<!-- TODO: remove test credentials test:test -->
```
- The comment seems to be a reminder for the developers to remove the test credentials. Given that the comment has not been removed yet, these credentials may still be valid.
- Although it is not very common to find login credentials in developer comments, we can still find various bits of sensitive and valuable information when looking at the source code, such as test pages or directories, debugging parameters, or hidden functionality. 
- There are various automated tools that we can use to scan and analyze available page source code to identify potential paths or directories and other sensitive information.
- Leveraging these types of information can give us further access to the web application, which may help us attack the back end components to gain control over the server.



### Prevention
- Ideally, the front end source code should only contain the code necessary to run all of the web applications functions, without any extra code or comments that are not necessary for the web application to function properly. 
- It is always important to review the code that will be visible to end-users through the page source or run it through tools to check for exposed information.
- It is also important to classify data types within the source code and apply controls on what can or cannot be exposed on the client-side. 
- Developers should also review client-side code to ensure that no unnecessary comments or hidden links are left behind. 
- Furthermore, front end developers may want to use `JavaScript` code packing or obfuscation to reduce the chances of exposing sensitive data through `JavaScript code`. These techniques may prevent automated tools from locating these types of data.


### Questions
- Check the above login form for exposed passwords. Submit the password as the answer.
	- HiddenInPlainSight