### What is an Exercise?
- In addition to the examples and demos demonstrated within interactive sections, most also end with exercises to test that knowledge.
- An exercise will usually have an accompanying `Docker target` or `VM target(s)`. A target can be started by clicking on `Click here to spawn the target system!`, which will be populated with its access details, in the format `http://<ip>:<port>`.
- It may also provide authentication details, in the form of a `username` and `password`.

> **Note:** Only a single target per user can be active at any one time. Each target has a timer that shows how much time is left before it is terminated, but it can be manually extended or re-spawned by clicking on the appropriate buttons.


### Docker Targets
- Most exercises, especially in web modules, utilize Docker targets, which are faster to spawn and can be accessed without any additional setup.
- Once a docker target is active, you can simply click on the IP/PORT to copy it, and then access the target (e.g. in a web browser for web modules). 
- Most docker targets are ready to use instantly, although some may take up to a minute after the IP/PORT are shown.

> **Note:** You can spot a docker target by its lack of a VPN button, as no VPN connection is required to access it.


### VM Targets
- Certain modules have advanced requirements for their exercises, like a Windows target, an Active Directory (AD) target, or a network environment target. 
- Such modules utilize a Virtual Machine (VM) as their target, which can be spawned like docker targets, but may take a little longer to start.
- If you use your `Workstation`, then you can start accessing the VM once its IP is shown. 
- Otherwise, if you prefer to use your own machine, then the VM can be accessed by connecting to the provided VPN key, which can be downloaded by clicking on the `Download VPN Connection File` button.

> **Note:** To find out more about connecting to the HTB Academy VPN, check out [this help article](https://help.hackthebox.com/en/articles/9297532-connecting-to-academy-vpn).


### Completing an Exercise
- Some questions have a `Hint` button, which may point you in the right direction if you are struggling with them. 
- Once you obtain the answer or the flag, you can type it in the field and hit `Submit` to complete the exercise/question.
- Solving a question correctly will reward you a certain amount of cubes, which may be collected to unlock other modules in HTB Academy, as we will discuss in the next section.
- Most questions are required to complete the section, but any questions marked as `Optional Exercises` may be solved by clicking the `Reveal Answer` button, and the section may be completed without solving them.

> **Note:** You can always use the exercise targets to practice what was shown in the section. However, solving the exercise will not always match the exact commands shown in the section, as they will have some variance to test your understanding and gradually build your skills. Exercises in easier modules will have a minor variance from the shown demo, while harder modules will be more challenging.


### Questions
- Start the above target, copy the shown IP:PORT by clicking on them, and then paste them in your browser. What's the proof shown in the page?
	- t4rg3ts